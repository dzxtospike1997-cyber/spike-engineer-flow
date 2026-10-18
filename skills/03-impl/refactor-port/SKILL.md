---
name: refactor-port
description: "Port or refactor a functional module from an original project into a new one: interview the engineer about which modules to move, read and map the original project's business flow and code flow, refactor into the new project, compare the old and new logic flows, and output the differences (offering to save them as a doc). Use when the engineer wants to port or refactor existing code."
---

Port or refactor existing code without losing track of what the original did. The heart of this skill is the end: a side-by-side comparison of old and new logic flows, with the differences written down.

## 1. Interview: what are we moving

Ask the engineer, in this order, and wait for answers:

- Which functional module(s) are being ported or refactored?
- From which original project, to which new project?
- What is the goal: pure port (same behaviour), port with adaptation (new chip / HAL / RTOS), or refactor (restructure while keeping behaviour)?
- What must be preserved exactly, and what is allowed to change? (timing, register values, public APIs, states)

## 2. Map the original: business flow and code flow

Read the original module until you can draw its shape. This is fact-finding; do it yourself, do not ask the engineer to explain what the code already shows:

- **Business flow**: what the module does end to end, its states, its inputs and outputs, its error paths.
- **Code flow**: the call graph, the driver/register touches, the data structures, the scheduling points (bare-metal or RTOS), the timing assumptions.

Where the code cannot show intent (a magic number's meaning, a deliberate quirk), ask the engineer. Write the map down before touching the new project.

## 3. Refactor into the new project

Carry over what maps directly; adapt what the new platform changes (HAL, chip registers, RTOS calls); restructure only what the goal calls for. Do not silently drop behaviour: every dropped or changed behaviour must be listed in the comparison.

## 4. Compare old and new logic flows

Build a side-by-side comparison: for each piece of behaviour, say kept / adapted / dropped / added, and why. Call out the differences clearly, not just the similarities.

## 5. Offer to save the differences as a doc

Ask the engineer whether to write the comparison out as a doc (for example `docs/refactor-<module>.md`) for the record. Do not create it unless they say yes.
