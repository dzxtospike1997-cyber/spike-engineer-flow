---
name: round-table
description: "Put multiple expert perspectives around a round table to solve a hard problem: spawn parallel sub-agents with distinct roles, have them propose and critique each other, and converge on a single reliable recommendation. Use for design decisions, tricky technical problems, or any question where one viewpoint is not enough."
---

Solve a hard problem by letting several expert perspectives debate it until a reliable recommendation emerges. Do not settle for a single viewpoint when the decision is hard.

## 1. Frame the question

Ask the engineer for the problem or decision and what is at stake. Read `.spike-engineer-flow/context.md` if it exists so every agent starts from the same project facts (chip, RTOS, standard, domain). These facts are common ground, not part of the debate.

## 2. Choose the perspectives

Pick 3-5 expert roles that matter for this question. For embedded work the usual roles are:

- **architect** - structure, module boundaries, interfaces.
- **performance** - cycles, latency, deadlines, stack depth, code size.
- **hardware coupling** - drivers, timing, interrupts, DMA, peripherals.
- **reliability / safety** - edge cases, fault injection, watchdog, failure modes.
- **maintainability** - coupling, nesting, code and variable volume, testability.
- **devil's advocate** - attacks every proposal and defends nothing.

Choose only the roles the question needs; do not spawn agents for the sake of it. State which roles are in and why.

## 3. Run the round table

Dispatch the roles as parallel sub-agents, each with the same question and the same project facts. Then run the debate in rounds:

1. **Propose** - each role states its solution or position independently.
2. **Critique** - each role reads the others' proposals and attacks them, then defends its own where it still stands.
3. **Referee** - a synthesis pass (the main agent or the devil's advocate) collects the strongest points and exposes the conflicts that remain.

## 4. Converge

Turn the debate into one recommendation: the chosen solution, why it beats the alternatives, the trade-offs it accepts, and the risks that remain. Mark any decision that still needs the engineer.

## 5. Output

Present the converged recommendation first, then the minority views that were rejected and why, then the single highest-risk assumption. Do not act on the recommendation until the engineer confirms.
