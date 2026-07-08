# Seguridad — prácticas probadas

> La seguridad es de lo más recurrente cuando empiezas con Claude. Esta es la
> **sección dedicada**: primero el principio común a todos, y luego las prácticas
> técnicas **ya probadas en producción** para quien usa código. Todo genérico y
> público-safe (sin secretos ni rutas propietarias).

## El principio (ambos tracks)

**Mínimo privilegio + humano en las decisiones irreversibles.** No importa el track:

- Dale a Claude el **acceso mínimo** que la tarea necesita, no "todo por si acaso".
- Las acciones que **no se pueden deshacer** (borrar, enviar, pagar, publicar) pasan por
  **confirmación humana**.
- Los **secretos** (tokens, API keys, contraseñas) viven **solo** en un `.env`
  gitignored. Nunca en código, commits, issues, logs, ni en la respuesta del asistente.

Mismo concepto, distinto vocabulario por audiencia:

| | Sin código (Cowork/Chat) | Con código |
|---|---|---|
| Riesgo principal | **Acceso y acciones** (qué ve, qué ejecuta/envía) | **Secretos, permisos y ejecución** |
| Cómo se expresa | Carpeta acotada + confirmación | Permisos, reglas `deny`, hooks |
| Detalle | [guía sin código → Seguridad](../sin-codigo/guia-sin-codigo.md#seguridad--el-riesgo-es-acceso-y-acciones-no-codigo) | [guía con código → Seguridad](../code-data/guia-code.md#seguridad--el-riesgo-es-secretos-permisos-y-ejecucion) |

## Sin código (Cowork/Chat) — acceso y acciones (resumen)

- **Carpeta acotada**: el proyecto/folder al que Claude accede, no toda la máquina.
- **Confirmar lo irreversible**: enviar correos, borrar, publicar → revisión humana.
- **Datos sensibles**: no subir a un proyecto lo que no debe salir de su ámbito.

Detalle y preguntas típicas: [guía sin código → Seguridad](../sin-codigo/guia-sin-codigo.md#seguridad--el-riesgo-es-acceso-y-acciones-no-codigo).

## Con código — guardrails técnicos (probados)

> Prácticas que corren en producción en setups reales. Genéricas y reutilizables.

### 1. `settings.json` con `deny` para secretos

Bloquea que el agente lea `.env` / archivos de secretos. Ver
[`settings-json.md`](settings-json.md).

### 2. Hooks como guardrails **deterministas**

Un **hook** es código que el harness ejecuta — no el modelo — así que es **determinista**
(no depende de que el agente "recuerde" portarse bien). Dos eventos útiles:

- **`PreToolUse`** — inspecciona un comando/acción **antes** de correr; puede **avisar**
  (inyectar contexto) o **bloquear**.
- **`SessionStart`** — corre chequeos al iniciar sesión (p. ej. drift de la config
  global, o paridad del setup entre máquinas).

> Regla mental: *el determinismo vive en los hooks; los procedimientos repetibles, en
> skills.*

### 3. Recipe probado — guard anti-fuga-de-secretos (`PreToolUse`, modo aviso)

**Footgun real:** chequear si un secreto existe con `${VAR:-AUSENTE}` **imprime el
valor** (la forma `:-` expande al valor cuando la variable está seteada). Este hook
**avisa** (no bloquea) cuando un comando expande una variable con **nombre de secreto**
(`*_API_KEY`, `*TOKEN*`, `*SECRET*`, `*PASSWORD*`, `*CREDENTIAL*`) usando `:-` o `:=`.

`scripts/guard-secret-print.py`:

```python
#!/usr/bin/env python3
# PreToolUse hook (Bash) — RED DE SEGURIDAD, NO BLOQUEA.
# Avisa si un comando expandiría una variable con nombre de secreto con ':-'/':=',
# que imprime el VALOR. Para chequear presencia usar solo ${VAR:+PRESENTE}.
import sys, json, re
try:
    data = json.load(sys.stdin)
except Exception:
    sys.exit(0)
cmd = (data.get("tool_input") or {}).get("command", "") or ""
PAT = re.compile(
    r"\$\{\s*[A-Za-z0-9_]*(KEY|TOKEN|SECRET|PASSWORD|CREDENTIAL|PRIVATE)[A-Za-z0-9_]*\s*:[-=]",
    re.IGNORECASE,
)
if cmd and PAT.search(cmd):
    warn = ("⚠️ Posible fuga de secreto: el comando expande una variable con nombre de "
            "secreto usando ':-' o ':=', que IMPRIME el valor. Para verificar presencia "
            "usa SOLO ${VAR:+PRESENTE}. Revisa antes de continuar.")
    print(json.dumps({"hookSpecificOutput": {"hookEventName": "PreToolUse", "additionalContext": warn}}))
sys.exit(0)
```

Cablearlo en `settings.json`:

```json
"hooks": {
  "PreToolUse": [
    {
      "matcher": "Bash",
      "hooks": [
        { "type": "command", "command": "python3 \"$CLAUDE_PROJECT_DIR/scripts/guard-secret-print.py\" 2>/dev/null" }
      ]
    }
  ]
}
```

**Regla de oro:** para verificar presencia de un secreto, usa **solo** `${VAR:+PRESENTE}`
— **nunca** `${VAR:-...}` (imprime el valor). Doble rama segura:
`[ -n "$VAR" ] && echo PRESENTE || echo AUSENTE`.

**Notas honestas:**
- Es una red de **señal alta, no un escáner universal** — detectar una fuga de secreto en
  salida arbitraria es indecidible. Cubre este patrón concreto, con casi cero falsos
  positivos.
- **No marca** el patrón legítimo `echo "$TOKEN" | sudo -S …` ni `${VAR:+PRESENTE}`.
- **Modo aviso** (`additionalContext`): inyecta la advertencia, no impide correr el
  comando — menos fricción. Si prefieres frenar, un hook PreToolUse puede **bloquear**
  con `exit 2`.

### 4. (Opcional) Self-checks al iniciar (`SessionStart`)

Mismo mecanismo, para flotas de máquinas: un hook que **avisa** si la config global
driftó (un symlink roto, ediciones sin commitear) o si una máquina quedó **desnivelada**
en plugins/skills vs un baseline declarado. Determinístico, no-mutante.

### 5. Dónde viven las credenciales (`.env` no siempre alcanza)

El `.env` gitignored por repo es el **piso**. Dos casos donde conviene un segundo nivel:

- **Credencial cross-project** (el mismo token en varios repos): copiar el `.env` a
  cada repo **multiplica las copias en texto plano** — más superficie para filtrar. Más
  seguro es una **bóveda cifrada del sistema operativo**: Keychain (macOS), Secret
  Service / libsecret (Linux), Credential Manager (Windows). Una sola fuente, cifrada en
  reposo; el proyecto lee la variable **en runtime**, no la deja escrita en N sitios.
- **Footgun token-en-URL:** nunca incrustar una credencial en una **URL** ni en un
  **remote de git** (`https://usuario:TOKEN@host/...`). Se filtra por `git remote -v`, el
  historial del shell, los logs de CI y los mensajes de error — sitios que nadie trata
  como secretos. En su lugar: un **credential helper** de git, un `.netrc` **fuera** del
  repo, o el token por variable de entorno consumida en el comando.

> Regla: **las credenciales nunca van en URLs, remotes, configs versionadas ni en un
> `.env` copiado a cada repo.** Una fuente, cifrada, leída en runtime.

### 6. Recipe probado — guard token-en-URL (`PreToolUse`, modo bloqueo)

Complementa el guard anti-fuga-de-secretos (§3, modo *aviso*). Este **detiene** (modo
`ask`: pide confirmación humana) cuando un comando **incrusta una credencial en una URL o
en un remote de git** — el footgun de §5.

`scripts/guard-token-in-url.py`:

```python
#!/usr/bin/env python3
# PreToolUse hook (Bash) — MODO BLOQUEO (ask). Pide confirmación humana si un comando
# incrusta credenciales en una URL (scheme://usuario:secreto@host), que se filtran por
# git remote -v, el historial y los logs de CI.
import sys, json, re
try:
    data = json.load(sys.stdin)
except Exception:
    sys.exit(0)
cmd = (data.get("tool_input") or {}).get("command", "") or ""
# scheme://algo:algo@host  — credenciales embebidas en el userinfo de una URL
PAT = re.compile(r"[a-zA-Z][a-zA-Z0-9+.\-]*://[^/\s:@]+:[^/\s@]+@", re.IGNORECASE)
if cmd and PAT.search(cmd):
    reason = ("⛔ Credencial embebida en una URL/remote (usuario:secreto@host). Se filtra "
              "por 'git remote -v', el historial y los logs de CI. Usa un credential "
              "helper, un .netrc fuera del repo, o el token por variable de entorno.")
    print(json.dumps({"hookSpecificOutput": {
        "hookEventName": "PreToolUse",
        "permissionDecision": "ask",
        "permissionDecisionReason": reason,
    }}))
sys.exit(0)
```

Cablearlo junto al guard de §3 (mismo `matcher` Bash, dos hooks):

```json
"hooks": {
  "PreToolUse": [
    {
      "matcher": "Bash",
      "hooks": [
        { "type": "command", "command": "python3 \"$CLAUDE_PROJECT_DIR/scripts/guard-secret-print.py\" 2>/dev/null" },
        { "type": "command", "command": "python3 \"$CLAUDE_PROJECT_DIR/scripts/guard-token-in-url.py\" 2>/dev/null" }
      ]
    }
  ]
}
```

**Notas honestas:**
- Cubre el patrón `usuario:secreto@host` dentro de una URL — el caso concreto y de alta
  señal. Puede marcar un `user:pass@` legítimo (raro en línea de comandos); por eso es
  `ask` (pregunta), no `deny` a secas.
- **No** cubre credenciales pasadas por otros medios (flags, stdin) — es una red para
  *este* footgun, no un escáner universal.

### 7. Denylist en CI — proteger el **repo**, no solo la máquina

Los hooks protegen la máquina **de quien los tiene instalados**. Un job de CI que
grep-ea patrones prohibidos y **falla el PR/MR** protege el **repo para todos** — incluido
quien nunca instaló los hooks. Defensa en profundidad: **disciplina → hooks (por máquina)
→ CI (por repo)**.

Ejemplo mínimo (GitHub Actions) que falla si se commiteó un `.env` o un token embebido:

```yaml
# .github/workflows/secret-denylist.yml
name: secret-denylist
on: [push, pull_request]
jobs:
  grep:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Reglas prohibidas
        run: |
          set -e
          # 1) archivos .env versionados (deberían estar en .gitignore)
          if git ls-files | grep -E '(^|/)\.env($|\.)' ; then
            echo "::error::Hay archivos .env versionados"; exit 1
          fi
          # 2) credencial embebida en una URL (usuario:secreto@host)
          if git grep -nE '[a-zA-Z][a-zA-Z0-9+.-]*://[^/[:space:]:@]+:[^/[:space:]@]+@' -- . ; then
            echo "::error::Credencial embebida en una URL"; exit 1
          fi
```

**Nota honesta:** un `grep` es una **red de señal, no un escáner**. Para escaneo serio
usa herramientas dedicadas (gitleaks, trufflehog, GitHub secret scanning). El grep es el
**piso barato** que corre en cualquier repo sin configurar nada.

### 8. Skills compartidas: auto-protegidas por defecto

Asumir **adopción parcial**: alguien se lleva *solo* tu skill, **sin** tu hook ni tu
`settings.json`. Una skill compartida es superficie de ejecución que **viaja sin sus
guardrails**, así que el método seguro tiene que viajar **dentro** de la skill:

1. **Enseña el método seguro por defecto** (p. ej. presencia con `${VAR:+PRESENTE}`,
   nunca `${VAR:-...}`; consumir el secreto dentro del comando sin imprimirlo).
2. **No incluye comandos peligrosos copiables** — token-en-URL, `cat .env`,
   `curl https://x:$TOKEN@...`. Lo que está en la skill se copia tal cual.
3. **Apunta al backstop** (hook/CI de §6-7) para que quien la adopte lo instale también.

## Resumen

- **Secretos solo en `.env`**, nunca impresos. Presencia con `${VAR:+PRESENTE}`.
- **Credenciales cross-project** → bóveda cifrada del SO (keychain), no un `.env`
  copiado a cada repo. **Nunca token-en-URL** (se filtra por `git remote -v` y logs).
- **`deny` en `settings.json`** para que el agente no lea secretos.
- **Hooks = guardrails deterministas** (avisar/bloquear) que no dependen de recordar.
- **Defensa en profundidad:** disciplina → hooks (por máquina) → CI (por repo).
- **Skills compartidas auto-protegidas:** el método seguro viaja dentro de la skill.
- **Mínimo privilegio + humano en lo irreversible** — en los dos tracks.
