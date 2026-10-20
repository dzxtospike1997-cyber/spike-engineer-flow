---
name: verify
description: "Run the machine-side verification: static checks against the coding standard and MISRA rules, unit tests for logic that runs on the host, and a measure call for partition boundary checks. Use after implementation, before code-review."
---

Run the verification that does not need hardware. Everything that needs the target is out of scope and goes to `hw-test` or `log-analyze`.

## 1. Ask about a senior-en pass first

Before verifying, ask the engineer whether they want `senior-en` to review the code at the design level first. Run it if yes; continue if no.

## 2. Split host-testable from target-only

Read the code and split it: pure logic, state machines, and algorithms can be tested on the host; drivers, timing, and interrupts need the target. Unit-test only the host-testable part. Tell the engineer what is host-testable and what must go to `hw-test` or `log-analyze`.

## 3. Static checks

Run the static checks against the coding standard and MISRA rules from `.spike-engineer-flow/context.md`, using whatever tool the project has (cppcheck, clang-tidy, PC-lint, or the IDE's checker). Map each finding to the rule it breaks. Skip anything the tool already enforces elsewhere.

## 4. Unit tests

Write and run unit tests for the host-testable logic, using the project's test framework. Mark each test with `@covers REQ-xxx` so the traceability matrix's test column fills.

## 5. Measure

Call `measure` to check the functional partition boundaries (bootloader / app / config regions) and get the resource numbers.

## 6. Report

Report the results: static findings, test results, and the partition boundary verdict. Update `docs/traceability.md` with what was tested. Hand off to `code-review`.
