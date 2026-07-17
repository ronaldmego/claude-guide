---
name: revisar-diff
description: Revisa los cambios staged antes de un commit — busca secretos filtrados y archivos sensibles, y resume qué cambiará. Úsala después de hacer git add y antes de commitear.
---

# revisar-diff

Revisión rápida y repetible de lo que está por entrar a un commit. Es un ejemplo
mínimo de skill: una tarea que repites, empaquetada como runbook en vez de reescrita
cada vez.

## Cuándo usarla

Después de hacer `git add` y antes de un commit, o cuando el usuario pida revisar
exactamente lo que está staged.

## Procedimiento

1. Confirma el estado del árbol:
   ```bash
   git status --short --branch
   ```
   Si no hay cambios staged, dilo claramente; no reportes que el commit está limpio.
2. Mira qué está staged:
   ```bash
   git diff --staged --stat
   ```
3. Revisa el contenido en busca de secretos o archivos que no deberían ir:
   ```bash
   git diff --staged
   ```
   Señales de alerta: `.env`, `*.key`, `*credentials*`, tokens o API keys en texto,
   credenciales embebidas en URLs (`usuario:secreto@host`).
4. Si aparece un secreto o un archivo sensible: **PARA** y avísalo antes de commitear.
   No imprimas el valor — nómbralo por archivo y línea.
5. Si está limpio, resume en 1-3 líneas qué cambió y por qué (para el mensaje de commit).

## Notas

- Es una red de señal, no un escáner: para escaneo serio usa gitleaks o trufflehog.
- Revisa sólo lo staged. Para auditar un push, compara también los commits locales con
  el upstream; no presentes esta skill como una revisión de lo que se va a subir.
- Esta skill no necesita archivos de apoyo. Cuando una skill sí los necesite (un
  script, una plantilla), ponlos junto a este `SKILL.md` y referéncialos por ruta
  relativa.
