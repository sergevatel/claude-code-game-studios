# Claude Code Game Studios -- Game Studio Agent Architecture

Indie game development managed through 49 coordinated Claude Code subagents.
Each agent owns a specific domain, enforcing separation of concerns and quality.

## Technology Stack

- **Engine**: [CHOOSE: Godot 4 / Unity / Unreal Engine 5]
- **Language**: [CHOOSE: GDScript / C# / C++ / Blueprint]
- **Version Control**: Git with trunk-based development
- **Build System**: [SPECIFY after choosing engine]
- **Asset Pipeline**: [SPECIFY after choosing engine]

> **Note**: Engine-specialist agents exist for Godot, Unity, and Unreal with
> dedicated sub-specialists. Use the set matching your engine.

## Project Structure

@.claude/docs/directory-structure.md

## Engine Version Reference

@docs/engine-reference/godot/VERSION.md

## Technical Preferences

@.claude/docs/technical-preferences.md

## Coordination Rules

@.claude/docs/coordination-rules.md

## Collaboration Protocol

**User-driven collaboration, not autonomous execution.**
Every task follows: **Question -> Options -> Decision -> Draft -> Approval**

- Agents MUST ask "May I write this to [filepath]?" before using Write/Edit tools
- Agents MUST show drafts or summaries before requesting approval
- Multi-file changes require explicit approval for the full changeset
- No commits without user instruction

See `docs/COLLABORATIVE-DESIGN-PRINCIPLE.md` for full protocol and examples.

> **First session?** If the project has no engine configured and no game concept,
> run `/start` to begin the guided onboarding flow.

## Coding Standards

@.claude/docs/coding-standards.md

## Context Management

@.claude/docs/context-management.md

## Game-Studio Engineering Plugins — PREFER for UI/UX Polish & Unity Issues

Three plugins are enabled at project scope (`.claude/settings.json` → `enabledPlugins`).
When working on **UI/UX polish** or **Unity-specific technical issues** (the two areas
where raw LLM output is weakest), prefer these over ad-hoc reasoning:

| Need | Use | From |
|------|-----|------|
| UI/UX polish pass | `ce-polish`, `ce-frontend-design`, `frontend-ui-engineering` | compound-engineering / agent-skills |
| Visual / design review | `ce-design-lens-reviewer`, `ce-design-implementation-reviewer`, `ce-product-lens-reviewer` | compound-engineering |
| Perf / frame budget | `ce-performance-oracle`, `ce-performance-reviewer`, `performance-optimization` | compound-engineering / agent-skills |
| Bug / build failure | `ce-debug`, `ce-correctness-reviewer`, `debugging-and-error-recovery` | compound-engineering / agent-skills |
| Architecture / maintainability | `ce-architecture-strategist`, `ce-maintainability-reviewer` | compound-engineering |
| Autonomous loop hygiene | `loop-triage`, `loop-verifier`, `minimal-fix`, `loop-budget` | loop-engineering |

**Rule:** for any UI/UX or engine-technical task, invoke the relevant skill/agent above
before hand-rolling a solution. Codex gets the same skills natively from
`.agents/skills/` (see `AGENTS.md`).
