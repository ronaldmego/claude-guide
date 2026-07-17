# Capas avanzadas — sólo cuando las necesites

Empieza con un `CLAUDE.md` corto por proyecto, una configuración conservadora y una skill cuando aparezca una tarea repetible. Añade las capas siguientes únicamente cuando resuelvan un problema observado.

## `CLAUDE.md` global

Ubicación habitual: `~/.claude/CLAUDE.md`.

Úsalo para unas pocas preferencias que aplican a todos tus proyectos, por ejemplo:

- idioma o formato de respuesta;
- principio de planificar y verificar;
- política transversal sobre secretos;
- convenciones personales realmente universales.

No copies allí el manual de cada repo, el estado de proyectos ni procedimientos largos. El contexto específico sigue viviendo en el `CLAUDE.md` del proyecto.

## Skills globales

Una skill global tiene sentido cuando el mismo procedimiento funciona en varios repos: revisión antes de commit, preparación de una entrega o un formato documental estable.

Versiona tus skills en un repo controlado y enlázalas o instálalas en `~/.claude/skills/`. Antes de instalar una skill de terceros, revisa su `SKILL.md` y cualquier script: una skill puede inducir ejecución de código.

## Agents

Usa un agente especializado cuando necesites:

- una revisión independiente;
- herramientas más restringidas;
- un rol claro, como seguridad o calidad de datos;
- aislar una investigación del contexto principal.

No crees agentes sólo para cambiar el nombre de una tarea. Si el trabajo es un procedimiento repetible, suele pertenecer a una skill.

## MCP

MCP conecta Claude con servicios como GitHub, bases de datos o herramientas internas. Cada servidor amplía la superficie de permisos y contexto.

Antes de activarlo:

1. define el caso de uso;
2. limita credenciales y scopes;
3. revisa qué herramientas y datos expone;
4. prueba con datos no sensibles;
5. elimina conectores que no uses.

## Trabajo en equipo

Cuando varias personas comparten el repo:

- versiona el `CLAUDE.md`, skills y settings del proyecto;
- deja preferencias personales en archivos locales ignorados por Git;
- revisa cambios de instrucciones como cambios de código;
- exige tests o validaciones independientes para acciones críticas;
- documenta quién puede aprobar deploys, borrados y cambios de permisos.

Más capas no equivalen a un sistema más maduro. Añade una capa cuando reduzca repetición, ambigüedad o riesgo; elimínala cuando sólo aumente mantenimiento.
