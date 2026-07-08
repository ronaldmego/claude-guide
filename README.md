# claude-kit

Guía en español para usar **Claude** bien y seguro.

Dos tracks, según cómo trabajas:

- **Con código** → Claude Code — [`code-data/guia-code.md`](code-data/guia-code.md)
- **Sin código** → Cowork / Chat — [`sin-codigo/guia-sin-codigo.md`](sin-codigo/guia-sin-codigo.md)

Más un núcleo común: sección de seguridad + plantillas `CLAUDE.md` / `settings.json` listas para copiar.

## Estructura del repo

```
claude-kit.md     ← router / índice curado — EMPIEZA AQUÍ
README.md         ← este archivo (estructura + índice)

comun/            ← núcleo común (lo usan ambos tracks)
  seguridad.md            🔒 sección de seguridad (prácticas probadas)
  global-claude-md.md     plantilla CLAUDE.md global (~/.claude/)
  proyecto-claude-md.md   plantilla CLAUDE.md por proyecto
  settings-json.md        settings.json de ejemplo (protege secretos)
  diagrama-capas.md       diagrama del setup en capas

code-data/        ← track "con código" — Claude Code (si programas o trabajas con datos)
  guia-code.md    Claude Code · skills · hooks · subagents · MCP

sin-codigo/       ← track "sin código" — Cowork / Chat (sin terminal)
  guia-sin-codigo.md   delegar trabajo real a Claude sin programar
```

## Índice

**▶ Empieza aquí:** [`claude-kit.md`](claude-kit.md) — router central: los dos
tracks, fuentes de skills/plugins, lectura mínima y la nota de seguridad.

**📚 Recursos / fuentes curadas:** los links a docs oficiales, repos y registries
viven curados dentro del índice y las guías (no en una página aparte):
- **Skills / plugins (discovery):** [`claude-kit.md` → Fuentes de skills/plugins](claude-kit.md#fuentes-de-skillsplugins-discovery)
  — repos oficiales de Anthropic + awesome-lists + registries, con señal (stars) y uso.
- **Lectura mínima (6 piezas):** [`claude-kit.md` → Lectura mínima cross-track](claude-kit.md#lectura-mínima-cross-track-si-solo-hay-tiempo-para-6-piezas)
  — la ruta corta si solo hay tiempo para lo esencial.
- **Docs oficiales por track:** [con código](code-data/guia-code.md#guía-oficial-principal)
  · [sin código](sin-codigo/guia-sin-codigo.md#guía-oficial-principal).

**🔒 Seguridad (transversal):** [`comun/seguridad.md`](comun/seguridad.md) — mínimo
privilegio + humano en lo irreversible, higiene de secretos y **guardrails técnicos
probados** (`deny` en `settings.json`, hooks, el guard anti-fuga-de-secretos).

**◆ Track "con código"** — Claude Code
- [`code-data/guia-code.md`](code-data/guia-code.md) — Claude Code, `CLAUDE.md`,
  skills / hooks / subagents / MCP, setup de proyecto, seguridad. Autocontenida.

**◇ Track "sin código"** — Cowork / Chat
- [`sin-codigo/guia-sin-codigo.md`](sin-codigo/guia-sin-codigo.md) — delegar trabajo
  real a Claude sin terminal (Cowork y Chat), con seguridad. Autocontenida.

**Núcleo común — `comun/`** (ambos tracks)
- 🔒 [`comun/seguridad.md`](comun/seguridad.md) — sección de seguridad: `deny` rules,
  hooks, el guard anti-fuga-de-secretos, almacenamiento de credenciales / keychain,
  un guard de token-en-URL y un denylist en CI.
- [`comun/diagrama-capas.md`](comun/diagrama-capas.md) — diagrama ASCII del setup en
  capas (global vs por proyecto).
- [`comun/global-claude-md.md`](comun/global-claude-md.md) — plantilla lista:
  `CLAUDE.md` **global** (va en `~/.claude/`).
- [`comun/proyecto-claude-md.md`](comun/proyecto-claude-md.md) — plantilla lista:
  `CLAUDE.md` **por proyecto** (raíz del repo).
- [`comun/settings-json.md`](comun/settings-json.md) — ejemplo listo: `settings.json`
  con `deny` para proteger secretos.

## Empezar

```bash
git clone https://github.com/ronaldmego/claude-kit.git
```

1. Lee **[`claude-kit.md`](claude-kit.md)** y elige tu track:
   - Programas / trabajas con datos → **[`code-data/guia-code.md`](code-data/guia-code.md)**.
   - No programas → **[`sin-codigo/guia-sin-codigo.md`](sin-codigo/guia-sin-codigo.md)**.
2. Copia [`comun/global-claude-md.md`](comun/global-claude-md.md) → `~/.claude/CLAUDE.md` y adáptalo.
3. Copia [`comun/proyecto-claude-md.md`](comun/proyecto-claude-md.md) → un `CLAUDE.md` en la raíz de cada proyecto.
4. Copia el `settings.json` de [`comun/settings-json.md`](comun/settings-json.md) (más útil en máquinas compartidas / menos confiables).

## Modelo en capas

El setup se arma en **capas**, de lo más general (todos tus proyectos) a lo más
específico (un proyecto). Diagrama completo en [`comun/diagrama-capas.md`](comun/diagrama-capas.md):

- **Capa 1 · global** (`~/.claude/CLAUDE.md` + `settings.json`) — tu identidad,
  seguridad y principios de trabajo. Aplica a toda la máquina.
- **Capa 1.5 · skills globales** (`~/.claude/skills/`) — skills invocables como
  `/<nombre>` desde cualquier proyecto, enlazadas desde un repo hub versionado.
- **Capa 2 · por proyecto** (`<repo>/CLAUDE.md`) — contexto, comandos, convenciones.
- Lo **determinístico** vive en hooks; lo **repetible**, en skills.

## Licencia

MIT — ver [LICENSE](LICENSE).
