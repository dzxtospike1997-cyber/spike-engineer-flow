---
name: driver-dev
description: "Write a chip driver from the datasheet to a working driver using the vendor's official library: initialization, register configuration, interrupt and DMA handling, and read/write APIs. Vendor-agnostic; use the official maintained library recorded in context.md. Use after design, for driver work."
---

Write a chip driver from the datasheet to a working driver, using the vendor's official, still-maintained library. Never hand-roll an abstraction the vendor already provides.

## 1. Read the inputs

Read `.spike-engineer-flow/context.md` for the chip, its reference material paths (datasheet, reference manual, register map, errata), the driver library, and the memory partition layout. Read the design document for the peripheral mapping and API signatures.

## 2. Read the datasheet, then the library

For each peripheral: read the datasheet and reference manual for the register meaning and timing, then find the vendor library's API that covers it. Map the register configuration to the library's calls. Check the chip's errata before trusting the documented behaviour.

## 3. Write the driver

Produce the driver code: initialization, register configuration, interrupt / DMA handling, and the read / write APIs the design specified. Follow the coding standard and MISRA rules from context.md. Mark the requirement the driver implements with `@req REQ-xxx`.

## 4. Put the hard decisions to the engineer

Generate the code automatically, but put the hardware-critical choices to the engineer: register values that affect safety or timing, interrupt priority, DMA buffer placement, and any errata workaround. Give a recommendation with each and wait.

## 5. Hand off

After the driver compiles, point the engineer to `build-flash` to build and `measure` for the real numbers, and to `log-analyze` if the driver needs on-target verification. Do not claim a driver works until it has been built and, where relevant, measured or run on target.
