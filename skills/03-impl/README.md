# 03-impl — implementation stage

Code implementation, porting, and refactoring.

- **`refactor-port`** (landed): ports / refactors a functional module — interviews for the module to port → clarifies the original project's business flow and code flow → refactors into the new project → compares the logic flow → outputs the differences (optionally saved to a doc).
- **`driver-dev`** (landed): chip driver development (datasheet → official library API mapping → driver implementation), vendor-agnostic, with hardware-critical decisions returned to the engineer.
- **`app-logic`** (landed): application / business-layer implementation (state machines, communication, algorithms); business rules belong to the engineer, implementation to the agent.
