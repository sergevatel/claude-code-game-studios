---
description: Orchestrated UI/UX polish pass — implementation + design-lens review against XCITE standards, emits a prioritized punch-list.
argument-hint: [screen, component, scene, or file path]
---

# UI/UX Polish Pass

Target: **$ARGUMENTS** (if empty, ask which screen / component / scene to polish, then continue).

Run this as a structured, multi-lens workflow. Do NOT hand-roll — invoke the named
skills and subagents at each step.

## 0. Ground truth first (verify-before-build)
- Locate and VISUALLY read the reference before changing anything: reference keyframes,
  `Docs/ART_BIBLE.md`, `Docs/FIGMA_LAYOUT.md`, and the actual sprite assets on disk.
  Never polish from assumption.
- Capture the current state (screenshot via Unity MCP or a build) as the "before".

## 1. Implementation quality
- Use the `frontend-ui-engineering` skill as a review lens.
- Delegate a focused pass to the `unity-ui-specialist` subagent for layout, anchoring,
  responsiveness, and UGUI / UI-Toolkit correctness.

## 2. XCITE polish standards (hard checks)
- **Typography:** all text via `ITypographyService` / `XCITETextStyle` with semantic
  `FontSlot` tokens — no raw font or size assignment.
- **Easing (DOTween):** Appear = OutBack, Exit = InBack, Smooth = InOutQuad,
  Celebrate = OutElastic. `Ease.Linear` only for continuous rotation.
- **Audio-visual-haptic triad:** every interaction fires sound + animation + haptic.
  Flag any missing leg.
- **Rendering:** URP only (no BIRP / Standard shader).

## 3. Design-lens review (parallel subagents)
- `ce-design-lens-reviewer` — visual and interaction design quality
- `ce-design-implementation-reviewer` — does the build match the design intent
- `ce-product-lens-reviewer` — does it serve the player and product goal

## 4. Polish discipline
- Apply the `ce-polish` skill's checklist (use its discipline; its web dev-server
  tooling does not apply to Unity — skip the automation, keep the rigor).

## 5. Output
- A prioritized punch-list: **P0** (breaks the look or a standard), **P1** (notable),
  **P2** (nice-to-have) — each with `file:line` and the specific fix.
- Apply P2 and low-risk P1 fixes directly. Leave P0 and risky changes for approval
  (per escalation rules).
- Re-screenshot as "after" and diff against the reference.
