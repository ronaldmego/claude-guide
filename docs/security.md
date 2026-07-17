# Seguridad: defensa en profundidad

Claude Code puede leer archivos, ejecutar comandos y modificar un repositorio. Ningún ajuste aislado reemplaza una política clara: **mínimo privilegio, secretos fuera del contexto y aprobación humana para lo irreversible**.

## 1. Mantén los secretos fuera del repo

- Guarda valores reales en `.env`, un keychain o un gestor de secretos.
- Incluye `.env` y archivos equivalentes en `.gitignore`.
- Versiona sólo `.env.example`, con nombres y placeholders, nunca valores reales.
- Antes de cada commit, revisa `git diff --staged` y usa un secrets scanner cuando el riesgo lo amerite.

## 2. Usa `deny` como red de seguridad

[`templates/settings.json`](../templates/settings.json) bloquea la herramienta `Read` sobre patrones comunes de secretos.

La distinción es importante:

> `deny: Read(./.env)` evita que Claude abra el archivo mediante la herramienta `Read`; **no garantiza que Bash no pueda ejecutar** `cat .env`, `source .env` u otro comando equivalente.

Por eso el `deny` complementa la disciplina operativa; no es una sandbox completa.

## 3. Consume secretos sin imprimirlos

Cuando una herramienta necesita una credencial, cárgala dentro del comando y evita devolver su valor al chat o al log:

```bash
set -a
source .env
set +a
mi-comando --token "$API_TOKEN"
```

No uses `echo "$API_TOKEN"`, no pegues credenciales en prompts y no las incluyas en URLs que puedan terminar en logs.

## 4. Automatiza sólo controles simples y verificables

Los hooks sirven para reglas determinísticas como:

- ejecutar formato o lint después de editar;
- correr tests antes de terminar;
- bloquear un patrón de comando claramente peligroso;
- escanear el diff antes de un commit.

Un hook de seguridad mal diseñado puede bloquear trabajo legítimo o crear una falsa sensación de protección. Empieza sin hooks, agrega uno cuando puedas probarlo y mantenlo pequeño.

## 5. Conserva a una persona en las decisiones irreversibles

Claude puede preparar una acción, pero debe pedir aprobación antes de:

- publicar o enviar contenido;
- desplegar a producción;
- borrar datos o recursos;
- cambiar permisos o credenciales;
- pagar, comprar o modificar cuentas;
- hacer `push --force` o reescribir historial compartido.

La automatización ayuda a ejecutar. La responsabilidad de autorizar sigue siendo humana.
