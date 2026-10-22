---
name: interrogate
description: "Interview the engineer about a new requirement or idea until you reach a shared understanding, recording each settled decision as an ADR and each clarified term into a glossary as you go. Runs before spec. Use when a new feature or requirement arrives and is not yet clear."
---

Turn a fuzzy idea into a shared understanding, and record the decisions and terms as you go, so nothing settled is lost.

Work in **rounds**. Map the requirement as a **design tree**: every decision branches into the decisions that hang off it. The **frontier** is every decision whose prerequisites are already settled. Number each question, give a recommended answer, and word questions so "yes" accepts your recommendation. Wait for the engineer's answers before the next round.

Before the first round, ask the engineer how to pace the questions, and offer:

- **all at once** - throw the whole frontier in a single round (default).
- **by functional module** - group the frontier by the module or feature each question belongs to; one module per round.
- **by step** - group the frontier by the step or stage each question belongs to; one step per round.
- **batching** - split the frontier into small batches, down to one question at a time; one batch per round.

The pacing is not fixed. The engineer may interrupt at any time, or type a pacing change into the "other" input box on any question; the next round follows the new pace.

Finding facts is your job, never the engineer's. Look in the code, the repo docs, and `.spike-engineer-flow/context.md` before asking. The decisions are the engineer's: put each to them and wait.

The design tree is not agent-owned. The engineer may add their own questions at any time — interrupt, or type one into a question's "other" box. Treat each added question as a new decision node: settle it like any other frontier question, then judge whether it deserves an ADR.

## Record as you go

Do not wait until the end. As each decision settles and each term is defined, write it down immediately:

- **ADR** - one file per significant decision, under `docs/adr/` (create it if absent). Each ADR has: title, status, context, decision, consequences. In embedded work the decisions are often "why DMA not polling", "why this baud rate", "why this register configuration", "why this scheduling model". A decision is significant only if someone will later ask "why did we choose this" — skip anything nobody will question.
- **Glossary** - one line per term in `docs/glossary.md`. Define each term in plain language; when a term is new to the engineer, reuse the `newbie` style (a plain sentence plus an everyday analogy).

Ask the engineer where these files should live if the default does not suit the repo.

## Finish

Stop when the frontier is empty: every branch visited, nothing silently assumed. Then hand the shared understanding (plus the ADRs and glossary) to the `spec` skill, which writes the formal specification. Do not write the spec or any code yourself.
