---
name: revisar-diff
description: Revisa los cambios staged antes de un commit — busca secretos filtrados y archivos que no deberían ir (.env, claves), y resume qué cambió. Úsala cuando vayas a commitear o el usuario diga "revisa antes de commitear", "prepara el commit" o "¿qué estoy por subir?".
---

# revisar-diff

Revisión rápida y repetible de lo que está por entrar a un commit. Es un ejemplo
mínimo de skill: una tarea que repites, empaquetada como runbook en vez de reescrita
cada vez.

## Cuándo usarla

Antes de cualquier commit, o cuando el usuario diga "revisa el diff", "prepara el
commit" o "¿qué voy a subir?".

## Procedimiento

1. Mira qué está staged:
   ```bash
   git diff --staged --stat
   ```
2. Revisa el contenido en busca de secretos o archivos que no deberían ir:
   ```bash
   git diff --staged
   ```
   Señales de alerta: `.env`, `*.key`, `*credentials*`, tokens o API keys en texto,
   credenciales embebidas en URLs (`usuario:secreto@host`).
3. Si aparece un secreto o un archivo sensible: **PARA** y avísalo antes de commitear.
   No imprimas el valor — nómbralo por archivo y línea.
4. Si está limpio, resume en 1-3 líneas qué cambió y por qué (para el mensaje de commit).

## Notas

- Es una red de señal, no un escáner: para escaneo serio usa gitleaks o trufflehog.
- Esta skill no necesita archivos de apoyo. Cuando una skill sí los necesite (un
  script, una plantilla), ponlos junto a este `SKILL.md` y referéncialos por ruta
  relativa.
