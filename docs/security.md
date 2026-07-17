# Seguridad: defensa en profundidad

Claude Code puede leer archivos, ejecutar comandos y modificar un repositorio. Ningún ajuste aislado reemplaza una política clara: **mínimo privilegio, secretos fuera del contexto y aprobación humana para lo irreversible**.

## 1. Mantén los secretos fuera del repo y del contexto

- Prefiere un keychain o gestor de secretos con integración nativa para la herramienta.
- Usa `.env` sólo como alternativa local cuando el proyecto lo requiera; trátalo como
  material sensible y mantenlo fuera de Git.
- Incluye `.env` y archivos equivalentes en `.gitignore`.
- Versiona sólo `.env.example`, con nombres y placeholders, nunca valores reales.
- Antes de cada commit, revisa `git diff --staged` y usa un secrets scanner cuando el riesgo lo amerite.

## 2. Usa `deny` como red de seguridad

[`templates/settings.json`](../templates/settings.json) bloquea la herramienta `Read` sobre patrones comunes de secretos.

La distinción es importante:

> `deny: Read(./.env)` evita que Claude abra el archivo mediante la herramienta `Read`; **no garantiza que Bash no pueda ejecutar** `cat .env`, `source .env` u otro comando equivalente.

Por eso el `deny` complementa la disciplina operativa; no es una sandbox completa.

El starter enumera variantes sensibles comunes en vez de bloquear todo `.env.*`, para
que Claude pueda leer `.env.example`. Añade al `deny` los nombres sensibles propios de
tu proyecto si usas otra convención.

## 3. Consume secretos por una interfaz segura

Usa, en este orden, una interfaz que la herramienta documente: integración con un
gestor de secretos o keychain; variable de entorno inyectada por el launcher; o
entrada por `stdin`/file descriptor cuando esté soportada.

- No uses `source .env` como receta genérica: `source` **ejecuta** el contenido como
  shell y sólo es aceptable si controlas y confías en ese archivo.
- No pases credenciales como argumentos (`--token ...`) ni en URLs: pueden aparecer en
  `ps`, telemetría, historial o logs.
- No uses `echo` para inspeccionarlas y desactiva trazas como `set -x` durante su uso.
- No pegues secretos en prompts ni pidas al agente que construya comandos que los
  incluyan. Consulta la interfaz segura específica de cada herramienta.

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
