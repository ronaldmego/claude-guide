# Changelog

Todos los cambios relevantes de este proyecto se documentan aquí.
Formato basado en [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Corregido
- Sustituida una receta insegura que ejecutaba `.env` y pasaba secretos como argumentos;
  la guía ahora prioriza keychain, gestores de secretos e interfaces nativas seguras.
- Alineados README, `.gitignore`, `settings.json` y la skill de ejemplo con el alcance
  real de sus controles, manteniendo `.env.example` legible.

### Cambiado
- Rediseño de `main` como kit personal mínimo para Claude Code: una sola portada,
  diagrama visible, quick start y plantillas copiables ([#2](https://github.com/ronaldmego/claude-kit/issues/2)).
- El contexto estable vive en `CLAUDE.md`; lo repetible en skills; lo determinístico
  en hooks; los secretos quedan fuera del contexto del modelo.
- La biblioteca anterior queda preservada en el tag `v0.1.0`, no duplicada dentro
  de la navegación actual.

### Eliminado
- Índices duplicados, track independiente de Cowork/Chat y catálogos extensos de
  videos, posts, registries y repositorios de discovery.

## [0.1.0] — 2026-07-08

### Añadido
- Guía en español para usar Claude bien y seguro, en dos tracks: **con código**
  (Claude Code — `code-data/guia-code.md`) y **sin código** (Cowork/Chat —
  `sin-codigo/guia-sin-codigo.md`).
- Núcleo común (`comun/`): sección de seguridad, plantillas `CLAUDE.md` (global y por
  proyecto), `settings.json` de ejemplo y diagrama del modelo en capas.
- Router `claude-kit.md`: fuentes de skills/plugins curadas, lectura mínima cross-track
  y nota de seguridad.
