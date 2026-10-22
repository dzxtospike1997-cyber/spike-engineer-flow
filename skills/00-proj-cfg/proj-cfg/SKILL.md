---
name: proj-cfg
description: "Interview the engineer about their embedded project and write the answers to a project context file the rest of spike-engineer-flow reads. Captures product domain, chip and vendor driver library, chip reference material paths, memory partition (flash / RAM / stack / no-init regions and their boundary overlaps), scheduling model (bare-metal / RTOS), build toolchain, coding standard, and log placement. Use to configure a project's spike-flow context (a new project, or one derived or modified from an existing project), and whenever one of these facts changes."
---

Capture the facts about an embedded project so every other spike-engineer-flow skill can read them instead of re-asking.

Interview the engineer in **rounds**, then write `.spike-engineer-flow/context.md` at the project root. In each round, ask every question whose answer nothing else depends on, give a recommended answer where you can, and wait for the engineer's reply. Word questions so "yes" accepts your recommendation.

**Discover first, ask second.** Before asking anything, look at the repo and find what the code already answers: toolchain markers (`.uvprojx`, `.ioc`, `CMakeLists.txt`, `Makefile`, `*.ld`), RTOS directories (`FreeRTOS`, `RT-Thread`, and so on), vendor library folders (`HAL`, `stdperiph`, `cmsis`), and standards documents (for example a company C coding standard). Only ask the engineer what the code cannot tell you.

## Round 1: product and platform

- **Product domain** - what kind of product is this? (energy-storage BMS, motor control, IoT, medical, consumer, other.) The domain tells later skills which regulations and idioms matter; it is never a hard-coded assumption.
- **MCU / SoC** - vendor and family (STM32, GD32, NXP, Renesas, ESP32, and so on). A project may target several; list them all.
- **Chip reference material** - where do each chip's datasheet, reference manual, register map, and errata live? Record exact paths or URLs so `driver-dev` and `senior-en` can read them directly.
- **Other compute** - does the project also run on Linux (C/C++) or depend on Python scripts (host tools, data processing)? If so, note their role as auxiliary.

## Round 2: firmware facts

- **Driver library** - what does driver code build on? The rule is the vendor's official, still-maintained library (HAL, standard peripheral library, LL, or bare registers), chosen per chip. Never assume one abstraction covers every chip in the project.
- **Scheduling model** - bare-metal, FreeRTOS, RT-Thread, another RTOS, or mixed. If mixed, say which parts use which.
- **Languages** - C, C++, assembly. Assembly is for startup / interrupt / timing-critical paths unless the engineer says otherwise.
- **Build toolchain** - Keil MDK, STM32CubeIDE, IAR, GCC + CMake/Make, other. Note the flash/debug probe (J-Link, ST-Link, and so on).

## Round 3: memory partition

The partition is the most load-bearing fact of the project: where the app links, how big the stack is, and what survives reset all hang off it, and every later skill (`design`, `senior-en`, `measure`, `verify`) reads it. Interrogate it fully — this is not a one-line question.

**Discover first.** Find the linker script / scatter file (`.ld`, `.scat`, `.sct`), the `.map` file, the toolchain project's flash config (`.uvprojx`, `.ioc`), and the startup file (`Stack_Size`, `__initial_sp`). Read the regions, addresses, and sizes straight from them. Ask the engineer only what the artifacts cannot answer — region purposes, per-target (Debug vs Release) differences, and reset-retention semantics.

Grill, one question at a time, on:

- **Flash layout** - total flash size; every region (bootloader / app / config / calibration / boot params) with start address, size, and purpose. Ask per build target: Debug and Release often link at different bases (for example Debug at 0x0, Release at 0x3000). Where does the parameter/calibration region live, and what is its erase/write granularity for in-place update?
- **RAM layout** - total RAM size and start/end; the static-data (RW/ZI) region; heap (if any) and its size; the stack region with its exact address range and size. Flag any region that crosses a memory-map boundary (for example a RAM block split across 0x20000000).
- **Stack** - stack size, and how it is determined (linker symbol, startup `Stack_Size`, runtime watermark). Single MSP stack, or MSP + per-task PSP under an RTOS? If RTOS, the per-task stack sizes. Growth direction (almost always down).
- **No-init / reset-retained regions** - which RAM survives reset, and where reset-retained / no-init variables live (exact addresses). Any variable pinned with `__attribute__((at(...)))` or an explicit section.
- **Overlaps and boundaries** - any region that overlaps another (stack vs no-init, app vs config), and how each boundary is enforced (scatter assertion, startup check, runtime check). Verify it against the artifact; do not trust the comment — this is where partition bugs hide.

Record the result as a table in the context file: region name, address range, size, purpose, and whether it survives reset.

## Round 4: standards and logs

- **Coding standard** - which standard does this project follow (a company internal doc, MISRA-C:2012 or 2004, ISO 26262 coding rules, none)? Where is the source document?
- **Compliance** - does the product need MISRA-C or another international standard, and which version? Is it already enforced by a tool (lint, PC-lint, static analyser)?
- **Log placement** - how are captured artifacts stored? Ask for each of: protocol captures (CAN/LIN/UART), waveforms (oscilloscope / logic analyser), serial logs, crash dumps, register dumps. Record exact directory paths and naming rules. These feed `log-analyze`, so they must be exact.

## Write the context file

Write `.spike-engineer-flow/context.md` at the project root, one section per round, plain markdown. Record "unknown" or "N/A" rather than guessing a fact. Close by telling the engineer: every other skill reads this file, so when a fact changes, run this skill again.
