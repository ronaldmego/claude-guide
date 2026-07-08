# Diagrama — Claude en tu máquina: cómo se construye tu setup en capas

> **Track con código.** Material visual (estilo infográfico). Explica el modelo en
> **capas** de `CLAUDE.md` + `settings.json`, de lo más general (todos tus proyectos)
> a lo más específico (un proyecto). Genérico y sanitizado: sin secretos ni rutas
> propias. Acompaña a `proyecto-claude-md.md` (capa por proyecto) y se explica en
> [`guia-code.md`](../code-data/guia-code.md).

```
╔══════════════════════════════════════════════════════════════════════════╗
║                   C L A U D E   E N   T U   M Á Q U I N A                  ║
║                    Cómo se construye tu setup en capas                     ║
╚══════════════════════════════════════════════════════════════════════════╝

  Idea central: UNA identidad + reglas tuyas, en CAPAS.
  De lo más general (todo) a lo más específico (un proyecto).


┌───────────────────────────────────────────────────────────────────────────┐
│ CAPA 1 ·  GLOBAL  ·  aplica a TODOS tus proyectos                            │
└───────────────────────────────────────────────────────────────────────────┘

  ~/.claude/                          ◀── vive en la máquina, NO en un repo
  │
  ├── 📄 CLAUDE.md  ───────────────▶  TU IDENTIDAD + CÓMO TRABAJAS
  │                                   • Quién es el asistente y cómo trabaja
  │                                   • Seguridad: secretos solo en .env;
  │                                     datos sensibles/PII nunca al agente
  │                                   • Boris genérico: planifica, prueba,
  │                                     humano aprueba lo irreversible
  │                                   • CERO secretos, CERO rutas de un repo
  │
  └── ⚙️ settings.json  ───────────▶  RED DE SEGURIDAD (toda la máquina)
                                      • deny de lectura de .env / secrets/**
                                      • permisos base

        ┌──────────────────────────────────────────────────────────────┐
        │  Mismo CONTENIDO, dos SUPERFICIES de entrega:                  │
        │   • Usas código (Claude Code)  → este ~/.claude/CLAUDE.md      │
        │   • Cowork / Desktop / web     → Project instructions          │
        └──────────────────────────────────────────────────────────────┘


┌───────────────────────────────────────────────────────────────────────────┐
│ CAPA 2 ·  POR PROYECTO  ·  estándar recomendado (proyectos de código)       │
└───────────────────────────────────────────────────────────────────────────┘

  <mi-proyecto>/                      ◀── vive en el repo, se combina con la Capa 1
  │
  ├── 📄 CLAUDE.md  ───────────────▶  MANUAL DEL PROYECTO
  │                                   • Contexto + stack en 1-3 frases
  │                                   • Quick Start y comandos comunes
  │                                   • Convenciones, remotes (GitHub…)
  │                                   • Aquí SÍ van detalles del repo
  │
  ├── 📄 .env.example  ────────────▶  Plantilla de credenciales (.env va en .gitignore)
  ├── 🔌 .mcp.json  ───────────────▶  Integraciones MCP (GitHub, Jira, DBs)
  │
  └── 📁 .claude/
      ├── ⚙️ settings.json  ───────▶  Permisos, hooks, modelo (versionado)
      ├── ⚙️ settings.local.json ──▶  Overrides locales (no se commitea)
      ├── 📁 skills/  ─────────────▶  Runbooks de tareas repetibles (3+ veces)
      ├── 📁 commands/  ───────────▶  Slash commands (/review, /fix-issue)
      ├── 📁 agents/  ─────────────▶  Sub-agentes con rol (code-reviewer, security)
      └── 📁 hooks/  ──────────────▶  Scripts por evento: validan, bloquean lo inseguro


┌───────────────────────────────────────────────────────────────────────────┐
│ CAPA 1.5 ·  SKILLS GLOBALES  ·  reutilizables entre tus proyectos           │
└───────────────────────────────────────────────────────────────────────────┘

  📦 tu-repo-hub-de-skills            ◀── versionado; symlink a ~/.claude/skills/
  │
  └── skills/ versionadas ───────────▶  Un git pull actualiza la skill en TODOS
                                        tus proyectos; no reinventas cada vez


   REGLA DE ORO
   ──────────────────────────────────────────────────────────────────────────
   Lo ESTABLE (identidad, seguridad, arquitectura) → CLAUDE.md
   Lo REPETIBLE (procedimientos)                   → skills/
   Lo DETERMINÍSTICO (validar, bloquear)           → hooks/ vía settings.json
   Lo SECRETO                                      → .env  (NUNCA en git ni en chat)
```

## Cómo leerlo

- **Capa 1 (global)** = tu identidad y forma de trabajar, que aplica a todo. Si usas
  código se entrega como `~/.claude/CLAUDE.md`; si usas Cowork/Desktop, el mismo
  contenido va como *Project instructions* (no como archivo).
- **Capa 2 (por proyecto)** = el estándar recomendado para repos de código; aquí sí
  entran detalles del proyecto (comandos, remotes, convenciones). Es lo que cubre
  `proyecto-claude-md.md`.
- **Capa 1.5 (skills globales)** = skills que sirven en varios proyectos, versionadas en
  un repo hub tuyo y enlazadas a `~/.claude/skills/`.

## Nota sobre el sufijo `.local`

Es la "capa personal que no se versiona" (va en `.gitignore`): p. ej.
`settings.local.json` para permisos/hooks que solo aplican en tu máquina.
