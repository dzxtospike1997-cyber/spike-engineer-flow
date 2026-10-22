---
name: round-table
description: "Solve a hard problem with a host-led round table: one main model owns the evolving proposal, the other expert members each propose their own solution, and the host repeatedly absorbs their results to challenge and complete its own, converging on a robust recommendation. Use for design decisions or any question where one viewpoint is not enough."
---

Solve a hard problem by putting a host model and several expert members around a table. The host owns the evolving solution; the members push it with their own; the host integrates what they give back, so the final result is more complete than any single member's.

## 1. Frame the question

Ask the engineer for the problem or decision and what is at stake. Read `.spike-engineer-flow/context.md` if it exists so every member starts from the same project facts (chip, RTOS, standard, domain). These facts are common ground, not part of the debate.

## 2. Choose the members and the host

Pick 3-5 expert roles that matter for this question, and designate one of them as the **host** (主理人). For embedded work the usual roles are:

- **architect** - structure, module boundaries, interfaces.
- **performance** - cycles, latency, deadlines, stack depth, code size.
- **hardware coupling** - drivers, timing, interrupts, DMA, peripherals.
- **reliability / safety** - edge cases, fault injection, watchdog, failure modes.
- **maintainability** - coupling, nesting, code and variable volume, testability.
- **devil's advocate** - attacks every proposal and defends nothing.

The host is usually the **architect** (or the role closest to the question's core). The host is the main model: give it the strongest model available. Every other member proposes its own solution independently, so each must have a real position of its own, not just a critique of the host's.

### Assign a model per member (optional)

By default the host runs on the strongest available model and the other members on the default. The engineer may override per member:

- Ask the engineer whether they want to pick models. If not, host = strongest, others = default.
- If yes, surface exactly the models the agent can spawn — the values the sub-agent `model` option accepts (e.g. `sonnet` / `opus` / `haiku` / `fable`). Offer those for each member; never invent names.
- Offer "same for all" and "leave the rest default" shortcuts. The engineer owns the mapping.
- Pass the chosen model to each sub-agent's `model` option when dispatching in section 3.

## 3. Run the rounds

Dispatch the members as parallel sub-agents, each with the same question, the same project facts, and its assigned model. Run round 1, then let the engineer gate every further round:

1. **Host proposes** - the host states its current solution in full.
2. **Members propose** - every other member independently writes its own solution to the same question, not merely a critique of the host's.
3. **Host integrates** - the host reads the members' solutions and revises its own: use them to 反推 (challenge its own assumptions and spot where it is wrong or incomplete), then 补全 (absorb what fills the gaps). Publish the revised solution.
4. **Hand the next step to the engineer** - after round 1, do not auto-loop. The host states which points it would still optimize or improve next, and asks the engineer whether to run another round. Continue only when the engineer says so; otherwise converge now. This keeps the meeting from burning tokens and context on repeated discussion.

## 4. Converge

The host's last revised solution is the recommendation. State it, why it beats the members' alternatives, the trade-offs it accepts, and the risks that remain. Mark any decision that still needs the engineer.

## 5. Output

Present the converged recommendation first, then which member contributed which strengthening piece, then the single highest-risk assumption. Do not act on the recommendation until the engineer confirms.
