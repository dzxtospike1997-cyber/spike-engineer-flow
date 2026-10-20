---
name: design
description: "Turn the formal spec into an implementable design: module breakdown, register and peripheral mapping, API signatures, state machines, and timing constraints, each traced to a REQ-ID. Use after spec, before implementation."
---

Turn the spec into a design that implementation can follow directly. Every design element traces back to a REQ-ID.

## 1. Read the inputs

Read `docs/spec.md` (requirements and acceptance criteria), `docs/traceability.md`, and `.spike-engineer-flow/context.md` (chip, driver library, RTOS scheduling model, memory partition layout). The design must fit inside the partition layout and use the official driver library.

## 2. Produce the design

Write `docs/design.md` (or `docs/design-<module>.md`). For each module or subsystem, specify:

- **Module breakdown** - which modules, their responsibilities, and their boundaries. Each module maps to one or more REQ-IDs.
- **Register / peripheral mapping** - which peripheral, which registers, which pins, and the intended configuration.
- **API signatures** - the public interfaces (functions, types, data structures), with ownership and lifetime.
- **State machine** - states, transitions, events, and what drives each transition.
- **Timing constraints** - deadlines, ISR budgets, polling periods, and where latency matters.

Trace every design element to a REQ-ID and write that ID next to it, so the traceability matrix's design column can be filled.

## 3. Decide what needs the engineer

The design's facts come from the code and datasheets; the decisions are the engineer's. Put every safety- or timing-critical decision to the engineer (register choices, interrupt priority, memory placement, scheduling), each with a recommendation, and wait.

## 4. Hand off

After the engineer confirms the design, tell them the next step is `senior-en` to review the design, then implementation. Do not start writing code.
