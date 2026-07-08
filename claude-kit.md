# Guía Claude — recursos y fuentes curadas (con código + sin código)

> Índice curado de fuentes oficiales para usar Claude bien y seguro. Las ordena
> según cómo trabajas; no reemplaza las guías oficiales. El contenido detallado vive en dos guías separadas —
> abre solo la que te aplica.

## Las dos guías (empieza aquí)

Hay **dos tracks** según cómo trabajas y cada uno tiene su propia guía autocontenida.
Abre solo el que te interesa — no necesitas leer el otro.

| Track | Guía | Para ti si… | Superficie |
|---|---|---|---|
| **Con código** ◆ | **[`guia-code.md`](code-data/guia-code.md)** | Escribes código o trabajas con datos | Claude Code + skills + `CLAUDE.md` + hooks + subagents + MCP |
| **Sin código** ◇ | **[`guia-sin-codigo.md`](sin-codigo/guia-sin-codigo.md)** | No programas y quieres delegar trabajo real | Claude Cowork + Chat + skills/plugins/conectores |

## Materiales de este repo

Además de las dos guías, hay entregables visuales y plantillas listas para copiar.
Todas pertenecen al modelo en capas de `CLAUDE.md` + `settings.json` (track **con
código**); **el cómo y el porqué** se explican en
[`guia-code.md` → Cómo se ve un proyecto bien configurado](code-data/guia-code.md#cómo-se-ve-un-proyecto-bien-configurado)
y en su sección [Plantillas listas para copiar](code-data/guia-code.md#plantillas-listas-para-copiar).
Aquí van solo como índice:

- 📊 **Diagrama de capas** — [`diagrama-capas.md`](comun/diagrama-capas.md):
  infográfico ASCII del modelo en capas. Ideal como referencia visual.
- 📄 **Plantilla global lista** — [`global-claude-md.md`](comun/global-claude-md.md):
  `CLAUDE.md` para `~/.claude/` (capa 1, aplica a toda tu máquina).
- 📄 **Plantilla por proyecto lista** — [`proyecto-claude-md.md`](comun/proyecto-claude-md.md):
  `CLAUDE.md` para la raíz de un proyecto (capa 2).
- ⚙️ **Settings sample** — [`settings-json.md`](comun/settings-json.md):
  `settings.json` con `deny` para proteger secretos (acompaña a las plantillas).

> El track **sin código** no usa archivos `CLAUDE.md`/`settings.json`: su equivalente
> son las *Project instructions* dentro de Cowork (ver [`guia-sin-codigo.md`](sin-codigo/guia-sin-codigo.md)).

Apóyate en fuentes existentes, en este orden de confianza:

- **Oficial Anthropic/Claude**: fuente normativa.
- **Repos oficiales Anthropic**: ejemplos reutilizables de skills/plugins.
- **YouTube**: material complementario; priorizado por views/likes y relevancia.
- **X/LinkedIn**: ejemplos virales o visuales para explicar conceptos.

## Fuentes de skills/plugins (discovery)

Fuentes **compartidas por ambos tracks** para descubrir skills/plugins. Úsalas como
referencia o discovery, **no** como instalación automática.

| Repo / fuente | Señal | Uso potencial |
|---|---:|---|
| [anthropics/skills](https://github.com/anthropics/skills) | Oficial Anthropic; ~139K stars al 2026-06 | Fuente first-party de Agent Skills. Revisar primero cuando busques skills oficiales. |
| [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) | Oficial Anthropic; ~25K stars | Directorio oficial de plugins Claude. |
| [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Oficial Anthropic | Plugins/skills legales listos como ejemplo: commercial legal, employment, privacy/compliance, litigation support. |
| [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | Oficial Anthropic | Plugins para trabajo de conocimiento (legal, finanzas, ops, soporte). |
| [mattpocock/skills](https://github.com/mattpocock/skills) | Repo público de Matt Pocock; ~136K stars | Skills reales desde la carpeta `.claude` de un engineer avanzado. Buenísimo para ver calidad; no instalar sin revisar. |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | Awesome-list; ~61K stars | Discovery de skills Claude. No instalar sin vetting. |
| [hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Awesome-list; ~44K stars | Lista amplia de skills, hooks, slash-commands, orchestrators y plugins para Claude Code. |
| [BehiSecc/awesome-claude-skills](https://github.com/BehiSecc/awesome-claude-skills) | Awesome-list; ~9K stars | Otra lista de discovery; usar solo como entrada para evaluar. |
| [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | Skills sectoriales; ~25K stars | Skills de research, ciencia, ingeniería, análisis y finanzas; revisar antes. |
| [midudev/autoskills](https://github.com/midudev/autoskills) | Instalador/stack; ~5.6K stars | Interesante por SHA/lockfile; no usar en producción sin revisión de seguridad. |
| [skills.sh](https://www.skills.sh/) | Registry/buscador de skills (no un repo) | Directorio web para descubrir skills por caso de uso. Revisar `SKILL.md` y scripts antes de instalar. |
| [jdepoix/youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api) | Utilidad popular; ~7.6K stars | Alternativa técnica para transcripts de YouTube si necesitas auditar videos públicos. |

Regla práctica: usa repos oficiales como referencia; usa awesome-lists/registries solo
para descubrir ideas. **Antes de instalar o ejecutar una skill, lee `SKILL.md` y
cualquier script incluido** (una skill = instrucciones + scripts que el agente ejecuta;
es superficie de code-execution / prompt-injection).

## Lectura mínima cross-track (si solo hay tiempo para 6 piezas)

| Prioridad | Fuente | Track | Por qué importa |
|---|---|---|---|
| 1 | [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices) | Con código | Guía oficial: contexto, iteración, verificación, hooks. |
| 2 | [Extend Claude Code](https://code.claude.com/docs/en/features-overview) | Con código | Mapa oficial de cuándo usar `CLAUDE.md`, skills, subagents, hooks, MCP y plugins. |
| 3 | [Don't Build Agents, Build Skills Instead](https://www.youtube.com/watch?v=CEvIs9y1uog) | Con código | Charla clave: skills > agents genéricos. Marco mental de arquitectura de skills. |
| 4 | [How Anthropic enables self-service data analytics with Claude](https://claude.com/blog/how-anthropic-enables-self-service-data-analytics-with-claude) | Con código / datos | Si trabajas con datos: skills, fuentes de verdad, validación y mantenimiento. |
| 5 | [Get started with Claude Cowork](https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork) | Sin código | Manual oficial: cómo empezar, permisos, proyectos y modos de operación. |
| 6 | [Use Claude Cowork safely](https://support.claude.com/en/articles/13364135-use-claude-cowork-safely) | Sin código | Base para guardrails: file access, scope creep, scheduled tasks, datos sensibles. |

## Seguridad — nota transversal

> 🔒 **Sección dedicada: [`comun/seguridad.md`](comun/seguridad.md)** — el principio
> común + las **prácticas técnicas probadas** (deny en `settings.json`, hooks como
> guardrails, el recipe del guard anti-fuga-de-secretos). La seguridad es de lo más
> recurrente cuando alguien empieza, así que tiene su propio bloque.

El detalle (preguntas típicas + respuestas) vive además en cada guía:
[Con código → secretos, permisos, ejecución](code-data/guia-code.md#seguridad--el-riesgo-es-secretos-permisos-y-ejecucion) ·
[Sin código → acceso y acciones](sin-codigo/guia-sin-codigo.md#seguridad--el-riesgo-es-acceso-y-acciones-no-codigo).

El principio común: **mínimo privilegio + humano en las decisiones irreversibles**.
Sin código se expresa como carpeta acotada y confirmación; con código como permisos,
`deny` y hooks. Mismo concepto, distinto vocabulario.

## Próximos pasos (para quien adapte esta guía)

- Prueba los plugins/skills oficiales en tu máquina antes de confiarles trabajo real.
- Valida las métricas actuales de los posts citados antes de usarlos (los conteos
  cambian con el tiempo).
