---
name: code-review
description: "Review the changes since a fixed point along two axes: Standards (does the code follow the project's coding standard and MISRA rules?) and Spec (does the code implement and test every REQ-ID it claims, matching the acceptance criteria?). Runs both as parallel sub-agents and reports them side by side. Use to review a branch, a PR, or work-in-progress changes."
---

Two-axis review of the diff between `HEAD` and a fixed point the engineer supplies:

- **Standards**: does the code follow the project's coding standard and MISRA rules (from `.spike-engineer-flow/context.md`)?
- **Spec**: does the code implement every REQ-ID it claims (via `@req`), are they tested (via `@covers`), and do they meet the acceptance criteria in `docs/spec.md`?

Both axes run as parallel sub-agents, then this skill aggregates their findings side by side.

## 1. Pin the fixed point

Take the fixed point from the engineer (commit SHA, branch, tag, `main`, `HEAD~5`). Capture `git diff <fixed>...HEAD` and `git log <fixed>..HEAD --oneline`. Confirm the ref resolves and the diff is non-empty before going further.

## 2. Read the project facts

Read `.spike-engineer-flow/context.md` for the coding standard and MISRA requirements, `docs/spec.md` for the requirements and acceptance criteria, and `docs/traceability.md` for the current REQ status.

## 3. Spawn both sub-agents in parallel

**Standards sub-agent** - give it the diff, the commit list, and the coding standard / MISRA facts from context.md, plus this smell baseline: Mysterious Name, Duplicated Code, God Function, Primitive Obsession, Repeated Switches, Shotgun Surgery, Divergent Change, Speculative Generality, Deep Nesting, Global State. Brief: report per file/hunk where the diff violates the standard or a baseline smell; distinguish hard violations from judgement calls; the repo standard overrides the baseline; skip anything tooling already enforces. Under 400 words.

**Spec sub-agent** - give it the diff, the commit list, and `docs/spec.md`. Brief: for each REQ-ID the diff touches (by `@req` marker or the module it changes), report: (a) requirements missing or partial; (b) behaviour not asked for (scope creep); (c) implementations that look wrong against the acceptance criteria; (d) REQ-IDs claimed in code with no `@covers` test. Quote the spec line for each finding. Under 400 words.

## 4. Aggregate

Present the two reports under `## Standards` and `## Spec`, verbatim or lightly cleaned, side by side. Do not merge or rerank. Update `docs/traceability.md` (implementation, test, and status columns) with what each axis found. End with a one-line summary: findings per axis, and the worst issue within each axis.
