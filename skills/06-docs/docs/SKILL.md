---
name: docs
description: "Write the project's documentation: datasheet summaries, register manuals, and module descriptions, generated from the code, design, and spec. Use to produce or update docs."
---

Write the documentation from what already exists, so it does not drift from the code.

## 1. Read the sources

Read `.spike-engineer-flow/context.md` (chip reference material paths), `docs/spec.md`, `docs/design.md`, and the code. Use the datasheets and reference manuals recorded in context.md for register-level facts.

## 2. Write the docs

Produce, in the repo's doc style:

- **Datasheet summary** - the chip's key registers, memory map, and errata the project actually uses.
- **Register manual** - each register / peripheral the code touches, its fields, and what the driver sets.
- **Module description** - per module: its responsibility, public API, state machine, and the REQ-IDs it implements.

Keep the docs close to the code they describe; when the code changes, the docs must change with it.

## 3. Hand off

After writing, point the engineer to what to review. Do not pad; document only what the project uses.
