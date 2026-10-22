---
name: measure
description: "Read build artifacts (.map, .elf, size, stack analysis) and produce real resource numbers: flash and RAM usage, worst-case stack depth, and functional partition boundary checks (bootloader / app / config regions). Invoked by build-flash, senior-en, and verify. Use whenever real measurements are needed instead of estimates."
---

Measure the built firmware, not estimate it. Produce real numbers from the build artifacts and check the memory-map partition boundaries.

## 1. Locate the artifacts and the map

Find the build output: the `.map` file, `.elf`, `.hex`/`.bin`, and the linker script (`.ld` / `.scat` / `.sct`). Read `.spike-engineer-flow/context.md` for the toolchain and chip. Ask the engineer for the build output directory and the partition layout only if they are not obvious from the repo.

## 2. Measure

- **Flash / RAM usage** - parse the `.map` (sections, `size`, `nm`) for actual code and data size, and the Top-N largest symbols. Report used vs total against the chip's flash and RAM budget.
- **Stack depth** - use `-fstack-usage` (GCC) or the toolchain's static stack analysis plus the call graph, for the worst-case stack per task and per ISR. Prefer a runtime stack watermark (RT-Thread `list_thread` / stack check) when it exists.
- **Functional partition boundaries** - take the memory map (bootloader / app / config regions and their address ranges) from the linker script or the engineer, then check every section against it: does the app stay inside its region, does anything overflow into a neighbour, does total flash fit the chip? Flag any overflow with the exact addresses and sizes.

## 3. Report

Output a measurement report: the real numbers per region, the partition boundary verdict (each region: fits / overflows by N bytes), the worst-case stack, and the Top-N largest symbols. Where a number is estimated rather than measured, say so.

Do not change the code. Report the numbers and hand them to whoever invoked you (build-flash, senior-en, or verify).
