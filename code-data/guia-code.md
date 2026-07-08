# Guía Claude Code — si programas o trabajas con datos

> Track **con código**: **Claude Code** — skills, `CLAUDE.md`, hooks, subagents y
> MCP. Configuras tu entorno para que Claude sea confiable, reproducible y seguro:
> mueves lo importante del prompt al entorno.
>
> Esta guía es autocontenida: si solo te interesa la parte técnica, lees esto y no
> necesitas el otro track. Para el índice general y el track no técnico, ver
> [`claude-kit.md`](../claude-kit.md) (central) y
> [`guia-sin-codigo.md`](../sin-codigo/guia-sin-codigo.md) (Cowork/Chat, sin código).

## Lectura mínima (si solo hay tiempo para 4 piezas)

| Prioridad | Fuente | Por qué importa |
|---|---|---|
| 1 | [How Anthropic enables self-service data analytics with Claude](https://claude.com/blog/how-anthropic-enables-self-service-data-analytics-with-claude) | Caso real de Anthropic: cómo estructuran skills, fuentes de verdad, validación y mantenimiento para que el análisis sea confiable. Aplica igual si trabajas con datos por tu cuenta. |
| 2 | [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices) | Guía oficial: contexto, iteración, verificación, hooks. |
| 3 | [Extend Claude Code](https://code.claude.com/docs/en/features-overview) | Mapa oficial de cuándo usar `CLAUDE.md`, skills, subagents, hooks, MCP y plugins. |
| 4 | [Don't Build Agents, Build Skills Instead](https://www.youtube.com/watch?v=CEvIs9y1uog) | Charla clave: skills > agents genéricos. Marco mental de arquitectura de skills. |

## Guía oficial principal

| Fuente | Qué sacar |
|---|---|
| [How Anthropic enables self-service data analytics with Claude](https://claude.com/blog/how-anthropic-enables-self-service-data-analytics-with-claude) | Lectura central si trabajas con datos. Anthropic reporta 95% de consultas de business analytics automatizadas con ~95% accuracy agregada. La tesis: la precisión en analytics es problema de contexto/verificación, no solo de generar SQL. |
| [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices) | Buenas prácticas oficiales: contexto, iteración, verificación, hooks para acciones obligatorias. |
| [Extend Claude Code](https://code.claude.com/docs/en/features-overview) | Mapa para decidir entre `CLAUDE.md`, skills, subagents, hooks, MCP y plugins. |
| [How Claude remembers your project](https://code.claude.com/docs/en/memory) | Explica `CLAUDE.md`, memoria del proyecto y auto-memory. |
| [Explore the .claude directory](https://code.claude.com/docs/en/claude-directory) | Estructura oficial: instrucciones, settings, skills, subagents y memoria. |
| [Extend Claude with skills](https://code.claude.com/docs/en/skills) | Cómo crear, administrar y compartir skills en Claude Code. |
| [Create custom subagents](https://code.claude.com/docs/en/sub-agents) | Para code review, validación de datos, debugging y separación de contexto. |
| [Automate actions with hooks](https://code.claude.com/docs/en/hooks-guide) | Para reglas determinísticas: tests, lint, bloqueos de comandos, seguridad. |
| [Hooks reference](https://code.claude.com/docs/en/hooks) | Referencia técnica de eventos y configuración de hooks. |

## Qué aprender si trabajas con datos (resumen de la guía de Anthropic)

Fuente: [How Anthropic enables self-service data analytics with Claude](https://claude.com/blog/how-anthropic-enables-self-service-data-analytics-with-claude).

Aunque el caso es de un equipo, las lecciones aplican igual si eres un analista o
dev que trabaja con datos por tu cuenta. Lo que conviene interiorizar:

1. **Data is not software**: en analytics suele haber una respuesta correcta,
   una fuente correcta y muchas formas de equivocarte sin darte cuenta.
2. **Tres fallas principales**:
   - ambigüedad concepto-entidad: el agente elige mal tabla, métrica, columna o
     definición;
   - staleness: schemas, fuentes y definiciones cambian;
   - retrieval failure: la información existe pero el agente no la encuentra.
3. **Data foundations**: modelos canónicos, datasets confiables, metadata,
   ownership, freshness, tests y docs siguen siendo la base.
4. **Sources of truth**: semantic layer, lineage, transformation graph,
   referencia estructurada y contexto de negocio.
5. **Skills como conocimiento procedimental**: no solo docs; una skill define
   qué fuentes consultar, en qué orden, cómo resolver ambigüedad y cómo validar.
6. **Pairwise skills**: una skill router + skills/domain docs especializadas.
   Esto reduce la búsqueda desde "todo el warehouse" hacia fuentes curadas.
7. **Mantenimiento de skills**: si el modelo de datos cambia y la skill no, la
   precisión cae. Trata el mantenimiento de skills como trabajo de ingeniería.
8. **Validación**: offline evals, online validation, revisión adversarial y
   métricas de efectividad.

Cómo lo aplicas tú:

- Para tus datos: cada dominio importante con el que trabajas seguido merece una
  skill que apunte a tablas canónicas, grain, filtros, owners, gotchas y ejemplos.
- Para no equivocarte: no le sueltes al agente el warehouse crudo; dale dominios
  acotados, ejemplos y rutas para escalar cuando algo no calza.
- Para contexto: OpenMetadata/lineage/glosarios pueden ser tu capa de contexto,
  pero solo si están mantenidos y la skill sabe consultarlos.

## Cómo se ve un proyecto bien configurado

> Este es el corazón del track: cómo debería lucir un proyecto tuyo bien armado.
> Dos piezas: (a) los 4 hábitos que lo hacen confiable, (b) la estructura de
> archivos `.claude/`. La idea de fondo es "sacar lo correcto del prompt y meterlo
> en el entorno".

### Los 4 hábitos (modelo mental)

El cambio de mentalidad, en cuatro reglas:

1. **No conviertas `CLAUDE.md` en un volcado de instrucciones.** Solo lo
   **estable**: contexto del proyecto, arquitectura, convenciones, comandos
   importantes. Si algo es un *procedimiento repetible / checklist / playbook*,
   va en otro lado (una **skill**), no en `CLAUDE.md`.
2. **Usa Plan Mode antes de cambios grandes.** Multi-file, refactors o algo
   "desordenado": es más seguro dejar que Claude inspeccione y planifique antes de
   tocar código.
3. **Convierte prompts repetidos en skills.** Si tecleas seguido "review this",
   "debug this" o "prepara esto para deploy", esa es la señal de que el workflow
   debe volverse reutilizable, no reescrito cada vez.
4. **Usa hooks para lo que debe pasar siempre.** Formato, validación, guardrails,
   notificaciones — cualquier cosa **determinística** la maneja mejor el sistema
   que "esperar a que el modelo se acuerde".

> **La idea de fondo (one-liner):** *mover las cosas correctas fuera del prompt y
> dentro del entorno.* `CLAUDE.md` para lo estable, skills para lo repetible,
> hooks para lo determinístico, permisos para lo peligroso.

### Estructura de un proyecto (oficial)

```
mi-proyecto/
├── CLAUDE.md               # instrucciones del proyecto; se cargan cada sesión
├── .mcp.json               # conectores MCP del proyecto (GitHub, DB, Slack…); versionado
└── .claude/
    ├── settings.json       # permisos (allow/deny), hooks, modelo — versionado
    ├── settings.local.json # overrides personales — gitignored
    ├── skills/             # runbooks reutilizables (/nombre); se cargan on-demand
    │   └── deploy/SKILL.md
    ├── commands/           # slash-commands simples (mismo mecanismo que skills)
    ├── agents/             # subagentes especializados (contexto aislado, p.ej. code-reviewer)
    ├── rules/              # reglas modulares por tema (style, testing, api-design)
    └── hooks/              # scripts disparados por evento (los CONFIGURA settings.json)

~/.claude/                  # GLOBAL — transversal a todos tus proyectos (avanzado)
├── CLAUDE.md               # convenciones que aplican a TODA la máquina
└── settings.json           # permisos/deny globales (p.ej. proteger .env en todos lados)
```

Notas de precisión (correcciones a infográficos que circulan):
- Es `.mcp.json` (no `.mcp.jason`).
- `CLAUDE.local.md` es **legacy**; hoy los overrides van en `settings.local.json`.
- Los **hooks se configuran en `settings.json`**; la carpeta `hooks/` solo guarda
  los scripts. No es un directorio "mágico" por sí solo.
- `commands/` y `skills/` son el mismo mecanismo (`/nombre`); para workflows nuevos,
  preferir **skills** (permiten empaquetar archivos de apoyo).

### Cómo conviene dejar la configuración

1. **Un `CLAUDE.md` por proyecto — siempre.** Es lo primero que lee Claude. Solo
   lo estable (hábito #1). Es el equivalente técnico de las instrucciones que en el
   track sin código pones en Cowork.
2. **`CLAUDE.md` global (`~/.claude/CLAUDE.md`) — cuando ya tienes rodaje.**
   Convenciones transversales a todos tus proyectos (tu estilo de trabajo, reglas
   que no quieres repetir por repo). Se combina con el del proyecto.
3. **`settings.json` con `deny` para proteger secretos.** Ejemplo recomendado
   (genérico — bloquea que el agente *lea* archivos de secretos a contexto):

   ```json
   {
     "permissions": {
       "deny": [
         "Read(./.env)",
         "Read(./.env.*)",
         "Read(./**/.env)",
         "Read(./secrets/**)"
       ]
     }
   }
   ```

   **Gotcha clave (verificado en pruebas):** `deny: Read(.env)` bloquea **solo la
   herramienta `Read`** — el agente ya no puede abrir el `.env` a la conversación.
   **No** bloquea un `cat .env` en Bash. Por eso este `deny` es una **red de
   seguridad** que se suma a la disciplina de *consumir el secreto dentro del
   comando sin imprimirlo* (ver "Seguridad" más abajo); no la reemplaza. Y
   por lo mismo **no rompe** flujos que cargan secretos vía `source` en Bash.
4. **Hooks para reglas no negociables** (hábito #4) y **skills para lo repetible**
   (hábito #3): el `CLAUDE.md` no debe cargar con eso.

### Plantillas listas para copiar

El modelo es en **dos capas** (ver el diagrama
[`diagrama-capas.md`](../comun/diagrama-capas.md)). Hay un **archivo listo para
copiar por cada capa** — sanitizados (sin identidades ni datos de nadie), solo
reemplazar placeholders y borrar lo que no aplique:

- **Capa 1 · global** → [`global-claude-md.md`](../comun/global-claude-md.md):
  quién eres tú + principios de trabajo + seguridad. Su cuerpo **es** el
  `CLAUDE.md`; se copia a `~/.claude/CLAUDE.md`.
- **Capa 2 · por proyecto** → [`proyecto-claude-md.md`](../comun/proyecto-claude-md.md):
  contexto + quick start + comandos + convenciones + seguridad del repo. Se copia a
  un `CLAUDE.md` en la raíz del proyecto; se combina con el global.
- **Settings** → [`settings-json.md`](../comun/settings-json.md): `settings.json`
  con `deny` para proteger secretos. Acompaña a las plantillas (global o por proyecto).

Estos son los **archivos** (copiar tal cual); esta guía explica el **por qué**.

## Buenas prácticas Code / data

1. **`CLAUDE.md` primero**: contexto de repo, comandos, arquitectura, permisos,
   fuentes de verdad y criterios de done.
2. **Skills para dominios repetibles**: no pidas "analiza ventas"; crea una skill
   por dominio con tablas canónicas, grain, filtros, owners, gotchas y ejemplos.
3. **Hooks para reglas no negociables**: tests, lint, secrets scan, blocklists,
   protección de carpetas críticas.
4. **Subagents para revisión independiente**: code review, validación de datos,
   chequeo de alucinaciones, security review.
5. **Fuentes de verdad antes que SQL creativo**: semantic layer, lineage,
   OpenMetadata, dashboards canónicos, docs de métricas.
6. **Mantenimiento como parte del PR**: si cambia un modelo, métrica o tabla, debe
   cambiar la skill/doc correspondiente.
7. **Evals de analytics**: mide accuracy con preguntas conocidas, no solo el demo
   feliz. La guía de Anthropic muestra que sin skills la precisión se degrada.

## Seguridad — el riesgo es **secretos, permisos y ejecucion**

> Fuente oficial: [Settings / permissions](https://code.claude.com/docs/en/settings).
>
> 🔒 **Prácticas probadas (recipe completo):** [`comun/seguridad.md`](../comun/seguridad.md)
> — deny en `settings.json`, hooks como guardrails, y el guard anti-fuga-de-secretos
> (`${VAR:+PRESENTE}`, nunca `${VAR:-}`).

Aquí sí hay que entrar a `.env`, permisos y hooks. Las preguntas típicas:

1. **"¿Cómo evito que filtre secretos / API keys?"** Tres capas, defensa en
   profundidad (no son alternativas):
   - **Disciplina (lo más importante):** consumir el secreto **dentro del comando**
     (`set -a; source .env; set +a; tool --token "$VAR"`), **nunca** `echo`/`cat`
     del valor a la salida. Esto tapa el vector Bash, que es el real.
   - **`deny` en settings (backstop gratis):** `Read(./.env)`, `Read(./.env.*)`,
     `Read(./secrets/**)`. Bloquea que el agente **lea** el archivo a contexto.
     **Ojo (gotcha clave):** el `deny: Read` **solo** afecta la herramienta `Read`;
     **no** bloquea `cat .env` en Bash. Por eso no sustituye a la disciplina —
     la complementa. Y por eso **no rompe** flujos que hacen `source` en Bash.
   - **Hook PreToolUse (opcional):** inspecciona el comando y bloquea/redacta
     patrones peligrosos (`cat *secret*`, `echo $TOKEN`). Potente pero con costo de
     mantenimiento; útil si operas mucho o compartes tu setup, overkill para uso casual.
2. **"¿`.env` en el repo?"** Nunca. `.gitignore` cubre `.env`, `*.key`,
   `*credentials*`; verifica `git diff --staged` antes de commitear. Usa
   `.env.example` con placeholders para no perder la referencia.
3. **"¿Cómo limito que ejecute cosas peligrosas?"** `permissions` allow/deny en
   `settings.json` (ej. `deny: Bash(curl *)`), y **hooks** para reglas no
   negociables (tests/lint/secrets-scan antes de actuar, bloquear comandos).
4. **"¿Los subagentes/MCP ven mis credenciales?"** Dale a cada agente/conector solo
   el scope que necesita; los MCP heredan permisos — revisa que un conector no
   exponga más de lo necesario.

**Mensaje de una línea para Code/Data:** *"El agente no necesita VER el secreto;
lo usa dentro del comando sin imprimirlo. `deny: Read(.env)` es red de seguridad,
no reemplaza la disciplina de no imprimir."*

> **Principio común con el track sin código:** mínimo privilegio + tú en las
> decisiones irreversibles. En Code se expresa como permisos, `deny` y hooks; en
> Cowork/Chat como carpeta acotada y confirmación. Mismo concepto, distinto
> vocabulario.

## Videos YouTube recomendados para Code/skills

Datos consultados con YouTube Data API el 2026-06-19. Los conteos cambian.

| Prioridad | Video | Canal | Duración | Views | Likes | Cuándo verlo |
|---|---|---:|---:|---:|---:|---|
| 1 | [What are skills?](https://www.youtube.com/watch?v=bjdBVZa66oU) | Claude | 2:54 | 1.24M | 16.0K | Video corto para entender skills de una. |
| 2 | [Mastering Claude Code in 30 minutes](https://www.youtube.com/watch?v=6eBSHbLKuN0) | Anthropic | 28:07 | 1.41M | 26.8K | El video oficial principal para arrancar. |
| 3 | [Don't Build Agents, Build Skills Instead](https://www.youtube.com/watch?v=CEvIs9y1uog) | AI Engineer | 16:22 | 1.43M | 29.1K | Charla clave: skills > agents genéricos. Muy útil para pensar tu arquitectura de skills. |
| 4 | [Full Walkthrough: Workflow for AI Coding — Matt Pocock](https://www.youtube.com/watch?v=-QFHIoCo-Ko) | AI Engineer | 1:36:30 | 982K | 20.6K | Walkthrough largo y a fondo; cuando quieras profundizar de verdad. |
| 5 | [Claude Code best practices](https://www.youtube.com/watch?v=gv0WHhKelSE) | Anthropic | 25:53 | 505K | 9.1K | Buen material oficial de engineering practices. |
| 6 | [How AI agents & Claude skills work](https://www.youtube.com/watch?v=S_oN3vlzpMw) | Greg Isenberg | 35:26 | 537K | 13.6K | Buena explicación divulgativa de skills/agents. |
| 7 | [How to 10x your Claude with 4 .md files](https://www.youtube.com/watch?v=ovLAIhbk3ek) | Greg Isenberg | 0:47 | 661K | 32.0K | Micro-video viral para captar la idea de `CLAUDE.md`/markdown context. |
| 8 | [5 Claude Code skills I use every single day](https://www.youtube.com/watch?v=EJyuu6zlQCg) | Matt Pocock | 16:42 | 413K | 10.4K | Práctico: skills reales en uso diario. |
| 9 | [Claude Code Essentials](https://www.youtube.com/watch?v=brLhhkUqcn4) | freeCodeCamp | 12:20:10 | 429K | 14.6K | Curso largo; para referencia profunda, no de una sentada. |
| 10 | [The 7 phases of AI-driven development](https://www.youtube.com/watch?v=Ah9p7v7nJWg) | Matt Pocock | 8:27 | 56.0K | 1.9K | Framework conciso de 7 fases (idea→research→prototype→PRD→kanban→execution→QA). Marco mental rápido del flujo AI-driven; complementa el walkthrough largo (#4). |

## Posts X/LinkedIn útiles para Code/data

| Fuente | Tema | Por qué sirve |
|---|---|---|
| [@_catwu - self-service data analytics post](https://x.com/_catwu/status/2062408623565984209) | Link original/social del blog de analytics. | Buen punto de entrada al caso interno de Anthropic. |
| [@sh_reya - skill docs/data model changing daily](https://x.com/sh_reya/status/2062347411511746874) | Mantenimiento de skill docs. | Refuerza que las skills son assets vivos, no docs muertos. |
| [@Mnilax - Don't build agents, build skills instead](https://x.com/Mnilax/status/2060422436370210922) | Skills vs agents. | Frase potente: encapsular el procedimiento. |
| [@cyrilXBT - Anthropic skills talk](https://x.com/cyrilXBT/status/2054033707296547043) | Skills y mantenimiento. | Complementa el video de AI Engineer. |
| [Brij Kishore Pandey - Claude Code project structure](https://www.linkedin.com/posts/brijpandeyji_the-claude-code-project-structure-i-wish-activity-7441293017766051840-oMkH) | Estructura `.claude/`, skills, commands, agents, hooks. | Buena referencia visual de la estructura `.claude/`. |
| Los 4 hábitos de un Claude Code confiable | `CLAUDE.md` estable (no dump), Plan Mode, prompts→skills, hooks para lo determinístico. | Resumen del modelo mental del track (ver "Cómo se ve un proyecto bien configurado"). |

## Skills/plugins que vale la pena conocer (Code / data)

| Recurso | Fuente | Qué mirar |
|---|---|---|
| Claude Code skills | [Extend Claude with skills](https://code.claude.com/docs/en/skills) | Skills como runbooks versionados. |
| `.claude` directory | [Explore the .claude directory](https://code.claude.com/docs/en/claude-directory) | Estructura de memoria, settings, skills, subagents. |
| Claude memory | [How Claude remembers your project](https://code.claude.com/docs/en/memory) | `CLAUDE.md` como contexto persistente. |
| Subagents | [Create custom subagents](https://code.claude.com/docs/en/sub-agents) | Code review, validación de datos, debugging, research. |
| Hooks | [Automate actions with hooks](https://code.claude.com/docs/en/hooks-guide) | Tests/lint/security determinístico. |
| Official plugins directory | [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) | Directorio de plugins; confía pero revisa antes de instalar. |

Las **fuentes de discovery de skills/plugins** (repos públicos de alta señal,
registries como `skills.sh`) son compartidas entre tracks y viven en el central:
ver [`claude-kit.md` → Fuentes de skills/plugins](../claude-kit.md#fuentes-de-skillsplugins-discovery).

## Ruta de aprendizaje sugerida

Si empiezas de cero, un orden que funciona:

1. **Lee** [How Anthropic enables self-service data analytics with Claude](https://claude.com/blog/how-anthropic-enables-self-service-data-analytics-with-claude)
   y las [best practices oficiales](https://code.claude.com/docs/en/best-practices) — para el marco mental.
2. **Mira** [Mastering Claude Code in 30 minutes](https://www.youtube.com/watch?v=6eBSHbLKuN0)
   y [Don't Build Agents, Build Skills Instead](https://www.youtube.com/watch?v=CEvIs9y1uog).
3. **Arma tu primer `CLAUDE.md`** en un repo real, copiando la plantilla
   [`proyecto-claude-md.md`](../comun/proyecto-claude-md.md) y aplicando los 4 hábitos
   (solo lo estable; lo repetible va a skills).
4. **Crea tu primera skill** de un dominio con el que trabajas seguido (tablas
   canónicas, grain, filtros, gotchas, ejemplos) y protege tus secretos con el
   `deny` de [`settings-json.md`](../comun/settings-json.md).
