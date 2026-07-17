# Changelog

All notable changes to this project are documented here.
Format based on [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Changed
- Rediseño de `main` como kit personal mínimo para Claude Code: una sola portada,
  diagrama visible, quick start y plantillas copiables ([#2](https://github.com/ronaldmego/claude-kit/issues/2)).
- El contexto estable vive en `CLAUDE.md`; lo repetible en skills; lo determinístico
  en hooks; los secretos quedan fuera del contexto del modelo.
- La biblioteca anterior queda preservada en el tag `v0.1.0`, no duplicada dentro
  de la navegación actual.

### Removed
- Índices duplicados, track independiente de Cowork/Chat y catálogos extensos de
  videos, posts, registries y repositorios de discovery.

## [0.1.0] — 2026-07-08

### Added
- Guía en español para usar Claude bien y seguro, en dos tracks: **con código**
  (Claude Code — `code-data/guia-code.md`) y **sin código** (Cowork/Chat —
  `sin-codigo/guia-sin-codigo.md`).
- Núcleo común (`comun/`): sección de seguridad, plantillas `CLAUDE.md` (global y por
  proyecto), `settings.json` de ejemplo y diagrama del modelo en capas.
- Router `claude-kit.md`: fuentes de skills/plugins curadas, lectura mínima cross-track
  y nota de seguridad.
