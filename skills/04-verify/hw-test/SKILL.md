---
name: hw-test
description: "Guide on-target / hardware-in-the-loop verification: what to run on the real hardware, what to observe, and how to capture the evidence so log-analyze can analyze it. Use when verification needs the actual target."
---

Guide the on-target verification, since embedded logic cannot be fully verified without the hardware. You plan and guide; the engineer runs the hardware.

## 1. Plan the test

From the design and spec (REQ-IDs), plan what to verify on target: the test steps, the inputs to apply, the outputs to observe, and the pass criteria for each REQ-ID.

## 2. Specify what to capture

For each test step, specify what evidence to capture: which protocol frames to record, which signals to probe, what trigger and sample rate, and where to save the files (the log placement from context.md).

## 3. Guide the run

Walk the engineer through the run: apply the inputs, observe the outputs, and capture the evidence. If something fails, capture the failure state before touching anything.

## 4. Hand off to log-analyze

After the engineer has captured the evidence, hand it to `log-analyze` for the analysis, then update `docs/traceability.md` for the REQ-IDs that were exercised.
