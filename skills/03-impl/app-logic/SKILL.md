---
name: app-logic
description: "Write the application and business logic above the drivers: state machines, protocol parsing, domain algorithms, and scheduling, following the design and spec. Use after design, for application-layer work."
---

Write the application and business logic above the drivers, following the design and spec.

## 1. Read the inputs

Read `.spike-engineer-flow/context.md` (scheduling model: bare-metal / FreeRTOS / RT-Thread), `docs/spec.md` (requirements and acceptance criteria), and the design document (modules, state machines, APIs).

## 2. Write the logic

Produce the application code: state machines, protocol parsing, domain algorithms, and task / ISR wiring per the scheduling model. Follow the coding standard and MISRA rules. Mark the requirement each piece implements with `@req REQ-xxx`.

## 3. Put the business rules to the engineer

The business rules (thresholds, policies, state transitions) are the engineer's; the implementation is yours. When the code depends on a business rule the spec does not pin down, ask the engineer rather than inventing one.

## 4. Hand off

After the logic is written, point the engineer to `build-flash` and `measure`, then `verify` and `code-review`. Do not claim it works until it has been built and verified.
