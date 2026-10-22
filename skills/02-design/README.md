# 02-design — design stage

Module / peripheral / API design + senior review.

- **`senior-en`** (landed): reviews as a senior embedded expert, at **two trigger points** — after design it reviews the design document (functional boundary / coverage breadth / performance / MCU-DSP efficiency / stack / code size), and before verify it reviews the code at the design level (data-structure decoupling, code and variable volume, nesting, heavy functions, stack depth, basic efficiency), calling `measure` to assess performance and partition boundaries; grilling and advice run in parallel.
- **`design`** (landed): turns the spec into an implementable design — module boundaries, register / peripheral mapping, API signatures, state machines, timing constraints, each design element tied to a REQ-ID.
