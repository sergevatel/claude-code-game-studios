# AGENTS.md — Codex Operating Contract (Claude Code Game Studios)

**Repo:** claude-code-game-studios (game-studio agent-architecture template)
**SSOT:** This file is the primary instruction set for Codex in this repository.

---

## Read First

This repo is a **template** for a multi-agent game studio (engine-agnostic — Godot /
Unity / Unreal). `CLAUDE.md` is the master configuration; read it before any work.

**Collaboration protocol (mandatory):** every task follows
**Question → Options → Decision → Draft → Approval**. Ask before writing with
Write/Edit. **No commits without explicit user instruction.** See
`docs/COLLABORATIVE-DESIGN-PRINCIPLE.md`.

**Authority chain (highest to lowest):**
1. Runtime system/developer instructions
2. This file (`AGENTS.md`)
3. `CLAUDE.md` (master configuration)

---

## UI/UX Polish & Engine-Technical — Use These Skills

The two areas where raw model output is weakest are **UI/UX polish** and
**engine-specific technical issues**. The skills below are vendored into
`.agents/skills/` (Codex-native — Codex does not load Claude Code plugins) and MUST be
applied rather than improvised:

| Skill | Invocation | When |
|-------|-----------|------|
| `ce-polish` | `$ce-polish` | UI/UX polish, juice, layout, visual feel |
| `frontend-ui-engineering` | `$frontend-ui-engineering` | UI implementation and interaction quality |
| `performance-optimization` | `$performance-optimization` | Frame budget, memory, draw calls |
| `debugging-and-error-recovery` | `$debugging-and-error-recovery` | Bugs, build failures, runtime errors |

Do NOT hand-roll UI polish or perf/debug analysis when one of these applies.
Provenance + re-sync: `.agents/skills/VENDORED.md`. Claude Code consumes the same
skills via the plugins enabled in `.claude/settings.json`.

---

*AGENTS.md v1.0.0 — claude-code-game-studios Codex Operating Contract*
*Skills-based invocation via `.agents/skills/` (Codex-native)*
