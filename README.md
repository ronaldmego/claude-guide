# claude-guide

> A ready-to-use, **Spanish-language** enablement kit for rolling out **Claude** in
> a company — primarily **Claude Code** (technical / data), with a secondary track
> for **Cowork** (non-technical). Curated official sources, a session plan, and
> copy-paste `CLAUDE.md` / `settings.json` templates.

## The problem

Most Claude onboarding material is in English and scattered across docs, videos and
social posts. Teams that want to adopt Claude well — especially non-English-speaking
ones — end up starting from scratch and improvising the security and configuration
parts.

## The solution

This kit curates the **official sources**, organizes them by audience (technical vs
business), proposes a **training plan**, and ships **ready-to-copy templates** so a
team goes from "we have Claude" to "we use it well and safely" fast. The content is in
**Spanish on purpose**: there's plenty in English, far less curated in Spanish.

It splits into **two self-contained guides by audience** plus a central summary that
routes between them — so a reader opens only the track they care about. The emphasis
is on the **Code / data track** (this repo is mostly visited by coders and data
folks); the **BPO / business track** is secondary, there for whoever also wants it.

## What's inside

| File | What it is |
|---|---|
| **`claude-guide.md`** | **Central summary / router** — the two tracks, shared skill sources, cross-track minimum reading, security note, and the training program. **Start here.** |
| **`guia-code.md`** ★ | **Code / data guide (primary)** — Claude Code, `CLAUDE.md`/skills/hooks/subagents, self-service analytics, project setup, security (secrets/permissions). Self-contained. |
| `guia-bpo.md` | **BPO / Cowork guide (secondary)** — Claude Cowork for non-technical roles (Legal, HR, ops), official sources by function, security (access & actions). Self-contained. |
| `diagrama-capas-claude-empresa.md` | ASCII diagram of the layered setup (global vs per-project), infographic-style. |
| `global-claude-md-empresa.md` | Ready template: **global** `CLAUDE.md` (goes in `~/.claude/`). |
| `proyecto-claude-md-empresa.md` | Ready template: **per-project** `CLAUDE.md` (repo root). |
| `settings-json-empresa.md` | Ready sample: `settings.json` with a `deny` rule to protect secrets. |

## Quick start

```bash
git clone https://github.com/ronaldmego/claude-guide.git
```

1. Read **`claude-guide.md`** (central summary) and pick your track:
   - Technical / data → **`guia-code.md`** (the primary track).
   - Business / non-technical → **`guia-bpo.md`**.
2. Copy `global-claude-md-empresa.md` → `~/.claude/CLAUDE.md` and replace `[nombre de la empresa]`.
3. Copy `proyecto-claude-md-empresa.md` → a `CLAUDE.md` at the root of each repo.
4. Copy the `settings.json` from `settings-json-empresa.md` (most useful on shared / less-trusted machines).

## The layered model

A company Claude setup is built in **layers** — from the most general (every employee)
to the most specific (one repo). See `diagrama-capas-claude-empresa.md` for the full
diagram:

- **Layer 1 · global** (`~/.claude/CLAUDE.md` + `settings.json`) — corporate identity,
  security and generic working principles. Shareable with anyone.
- **Layer 1.5 · global skills** (`~/.claude/skills/`) — reusable skills invocable as
  `/<name>` from any project, wired from a versioned hub repo. See the global template.
- **Layer 2 · per project** (`<repo>/CLAUDE.md`) — context, commands, conventions.
- **Determinism** lives in hooks; **repeatable procedures** live in skills.

## Language

The content is in **Spanish** (the differentiator). This README is in English for
discoverability.

## License

MIT — see [LICENSE](LICENSE).
