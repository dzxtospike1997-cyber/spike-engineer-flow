---
name: spec
description: "Turn the shared understanding from interrogate into a formal specification, assigning each requirement a unique REQ-ID and acceptance criteria, and set up the traceability matrix. Use after interrogate, before design."
---

Write the formal specification from the shared understanding that `interrogate` produced, and give every requirement a traceable ID.

## 1. Take the shared understanding

Read what `interrogate` left: the design tree, the ADRs in `docs/adr/`, the glossary in `docs/glossary.md`, and `.spike-engineer-flow/context.md`. If `interrogate` was not run, run it first or ask for the requirement.

## 2. Write the spec with REQ-IDs

Write `docs/spec.md` (or `docs/spec-<module>.md` for per-module specs). For every requirement:

- Assign a unique ID: `REQ-<module>-<NNN>` (for example `REQ-CAN-001`, `REQ-BAL-012`).
- State the requirement in one sentence.
- State its acceptance criteria: how you will know it is met, observable and measurable.
- Mark its status as `To design`.

Keep each requirement small enough that one test can cover it. Merge or split the engineer's statements as needed, and confirm the split with them.

## 3. Set up the traceability matrix

Create `docs/traceability.md` with one row per REQ-ID:

| REQ-ID | Requirement | Design | Implementation | Test | Status |

Fill the REQ-ID and Requirement columns now. The design, implementation, and test columns are filled by later skills as they reference these IDs.

## 4. Hand off

Tell the engineer the traceability convention: implementation code marks the requirement it implements with `@req REQ-xxx` in a comment, and tests mark the requirement they cover with `@covers REQ-xxx`. Later, `code-review` and `verify` read these markers and update the matrix. Do not start designing; hand off to `design`.
