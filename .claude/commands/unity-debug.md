---
description: Systematic Unity bug / build-failure debugging — root-cause first, reproduce with a failing test, minimal fix, verify.
argument-hint: [error message, failing test, or symptom]
---

# Unity Debug

Symptom: **$ARGUMENTS** (if empty, ask for the error text, failing test, or repro steps).

Follow this discipline in order. Do NOT jump to a fix before the root cause is proven.

## 1. Capture
- Pull the exact error: Unity console via `read_console` (Unity MCP), failing test
  output, or stack trace. Note repro steps and the last-known-good state.

## 2. Triage the class of failure
- **Compile / build error:** use the `build-fix` skill or `build-resolver` subagent.
  Check missing references, asmdef wiring, C# 9 constraints, and Odin
  `#if ODIN_INSPECTOR` guards.
- **Runtime / logic bug:** continue below.

## 3. Root cause (do not guess)
- Drive the `superpowers:systematic-debugging` skill (4-phase root-cause) as the spine.
- Use `debugging-and-error-recovery` and `ce-debug` as additional lenses.
- Have the `ce-correctness-reviewer` subagent inspect the suspect code path.

## 4. Reproduce with a test (RED)
- Per XCITE TDD: write the smallest failing EditMode / PlayMode test that captures the
  bug BEFORE fixing it.

## 5. Minimal fix (GREEN)
- Use the `minimal-fix` skill: the smallest change that makes the test pass. No
  unrelated refactors. Fix the root cause, not a symptom.

## 6. Verify
- Run the test suite; confirm the new test passes and nothing regressed.
- Use `loop-verifier` / `superpowers:verification-before-completion` — evidence before
  claiming done. Confirm the Unity console is clean (zero errors AND zero warnings).

## 7. Capture the lesson
- If this was a recurring pattern, append it to `tasks/lessons.md` so it does not recur.
