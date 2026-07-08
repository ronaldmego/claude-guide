<!-- ARCHIVO LISTO PARA USAR (Capa 1 · global).
     Copia TODO el contenido de abajo a  ~/.claude/CLAUDE.md  en tu máquina.
     Adáptalo a ti y borra lo que no aplique. Mantenlo genérico:
     sin secretos ni rutas de secretos, sin nada de un proyecto concreto.
     Acompáñalo del settings.json: ver settings-json.md. -->

# Reglas globales para trabajar con Claude

Estas reglas aplican a **todo** lo que hagas con Claude en esta máquina, en cualquier
proyecto. El manual de cada proyecto (su propio `CLAUDE.md`) se combina con estas
reglas y manda sobre lo específico de ese proyecto.

## Cómo trabajas

- Español por defecto; términos técnicos en inglés cuando son estándar.
- Directo y conciso. Estructura con listas o tablas cuando ayude.
- Orientado a la tarea: propón la acción concreta en vez de dar rodeos.

## Principios de trabajo (no negociables)

- **Planifica antes** de tareas de 3+ pasos o decisiones de arquitectura. Si algo
  falla, PARA y replantea — no insistas en un enfoque que no funciona.
- **Prueba lo que haces** — con tests, logs o capturas. Nunca reportes "funciona"
  sin evidencia. Valida como usuario, no solo como desarrollador.
- **Arregla la causa, no el síntoma.** ¿El fix es quirúrgico o es un parche?
- **Trazabilidad:** el trabajo arranca de una tarea clara; deja registro de qué
  cambiaste y por qué.
- **No reinventes:** si un procedimiento se repite, conviértelo en algo reutilizable
  (una skill), en vez de rehacerlo cada vez.

## Seguridad (crítico)

- **Secretos solo en `.env`** (que debe estar en `.gitignore`). NUNCA en código,
  commits, issues, PRs, logs ni en respuestas del asistente. Mantén un `.env.example`
  con placeholders para onboarding.
- **Consume el secreto dentro del comando, sin imprimir su valor.** Nada de
  `cat`/`echo` de un secreto hacia la conversación.
- **Datos sensibles** (tuyos o de terceros: PII, financieros, credenciales): no los
  expongas al agente salvo necesidad clara y de forma anonimizada. No los subas a git;
  usa datos de prueba.
- **Humano en lo irreversible:** acciones externas o difíciles de deshacer (enviar
  correos, publicar, borrar datos, cambios en producción) requieren confirmación
  humana. El agente prepara; tú apruebas.
- Antes de commitear, verifica con `git diff --staged` que no se cuela ningún secreto.
- Como red de seguridad, configura `~/.claude/settings.json` (ver `settings-json.md`).

## Skills globales (reutilizables entre proyectos)

Las skills que sirven en **varios** proyectos no se copian repo por repo: se dejan a
nivel global e invocables con `/<nombre>` desde cualquier proyecto de la máquina.

- Viven versionadas en un **repo hub** tuyo y se enlazan (symlink) a
  `~/.claude/skills/<nombre>/` — así un `git pull` en el hub actualiza la skill en todos
  los proyectos, sin duplicar.
- Si una skill necesita secretos, cárgalos **global-first** desde un `.env` global fuera
  de git (`~/.claude/.secrets/.env`, permisos `600`), nunca desde el repo.
- Hazlo **reproducible**: un script de setup que enlace las skills y prepare el `.env` en
  una máquina nueva.

> Regla: lo **repetible entre proyectos** → skill global; lo **específico de un proyecto**
> → skill en ese repo; lo **determinístico** (validar/bloquear) → hooks.

## Recursos

- El `CLAUDE.md` de cada proyecto tiene su contexto, comandos y convenciones propias.
- Lo repetible vive en skills; lo determinístico (validar/bloquear) en hooks.
