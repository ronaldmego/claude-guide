# claude-kit

**Kit de arranque en español para configurar Claude Code en tus repos** — código o
datos. El objetivo: que Claude sea confiable, reproducible y seguro **sin llenar el
prompt de instrucciones**.

La lección detrás del kit: fui agregando contexto, reglas y excepciones a mi setup
hasta que se volvió más difícil de entender, no más fácil — más instrucciones no
hacían a Claude más confiable, lo hacían más confuso. Lo que arregló el problema no
fue escribir más, sino **decidir qué pertenece a cada capa**: el contexto estable en
`CLAUDE.md`, los procedimientos repetibles en skills, la validación determinística en
hooks y los secretos fuera del contexto del modelo.

## La idea en un diagrama

![Claude Code: cada instrucción tiene un lugar — contexto en CLAUDE.md, planificación con Plan Mode, procedimientos en skills, validaciones con hooks y secretos fuera del contexto](assets/claude-kit-structure.svg)

```
claude-kit/
├── README.md                    ← empieza aquí
├── assets/
│   └── claude-kit-structure.svg ← diagrama embebido y reutilizable
├── templates/
│   ├── CLAUDE.md                ← contexto estable del proyecto (cópialo a tu repo)
│   ├── settings.json            ← deny de lectura para secretos
│   └── example-skill/SKILL.md   ← una skill mínima de ejemplo
└── docs/
    ├── security.md              ← defensa en profundidad para secretos
    └── advanced.md              ← capa global, skills globales, agents, MCP, equipo
```

## Las reglas

1. **`CLAUDE.md` = solo lo estable.** Qué es el proyecto, comandos, arquitectura,
   convenciones, fuentes de verdad. No lo conviertas en un volcado de instrucciones.
2. **Plan Mode antes de cambios grandes.** Multi-file, refactors o algo desordenado:
   deja que Claude inspeccione y planifique antes de tocar código.
3. **Lo repetible → skills.** Si tecleas seguido "review this" o "prepara esto para
   deploy", conviértelo en un runbook reutilizable en vez de reescribirlo cada vez.
4. **Lo determinístico → hooks.** Formato, tests, validación, guardrails: lo que debe
   pasar **siempre** lo maneja el sistema, no la memoria del modelo.
5. **Secretos solo en `.env`, consumidos sin imprimir.** El `deny: Read(.env)` es una
   red de seguridad, no un reemplazo de la disciplina — ver [docs/security.md](docs/security.md).

## Quick start (menos de 15 min)

```bash
git clone https://github.com/ronaldmego/claude-kit.git
```

1. Copia [`templates/CLAUDE.md`](templates/CLAUDE.md) a un `CLAUDE.md` en la raíz de
   tu repo. Rellena los `[placeholders]` y borra lo que no aplique. **Solo lo estable.**
2. Copia [`templates/settings.json`](templates/settings.json) a
   `<repo>/.claude/settings.json` para proteger tus secretos con `deny`.
3. (Opcional) Copia [`templates/example-skill/`](templates/example-skill/SKILL.md) a
   `<repo>/.claude/skills/` y adáptala a un procedimiento que repites.
4. Abre Claude Code en el repo y confirma que lee el `CLAUDE.md` (pídele que resuma el
   contexto del proyecto). Agrega una skill o un hook sólo cuando aparezca una tarea
   repetible o una validación que realmente deba ejecutarse siempre.

## Qué hay aquí

- **Plantillas** listas para copiar: [`CLAUDE.md`](templates/CLAUDE.md) ·
  [`settings.json`](templates/settings.json) ·
  [`example-skill/SKILL.md`](templates/example-skill/SKILL.md).
- **[docs/security.md](docs/security.md)** — defensa en profundidad para secretos:
  qué bloquea (y qué no) el `deny`, consumir secretos sin imprimirlos, cuándo usar
  hooks y aprobación humana en lo irreversible.
- **[docs/advanced.md](docs/advanced.md)** — capa opcional cuando ya tienes rodaje:
  `CLAUDE.md` global, skills globales, subagents, MCP y trabajo en equipo.

## Alcance

Es un **kit personal de arranque**, no una arquitectura enterprise ni una enciclopedia
de Claude. Reúne lo mínimo verificado para que un proyecto sea confiable y seguro. Las
fuentes normativas son los [docs oficiales de Claude Code](https://code.claude.com/docs);
este kit solo te ahorra las primeras decisiones.

## Licencia

MIT — ver [LICENSE](LICENSE).
