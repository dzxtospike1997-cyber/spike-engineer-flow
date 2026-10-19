---
name: cr-proj
description: "Interview the engineer about their embedded project and write the answers to a project context file the rest of spike-engineer-flow reads. Captures product domain, chip and vendor driver library, scheduling model (bare-metal / RTOS), build toolchain, coding standard, and log placement. Use on first setup, or whenever one of these facts changes."
---

Capture the facts about an embedded project so every other spike-engineer-flow skill can read them instead of re-asking.

Interview the engineer in **rounds**, then write `.spike-engineer-flow/context.md` at the project root. In each round, ask every question whose answer nothing else depends on, give a recommended answer where you can, and wait for the engineer's reply. Word questions so "yes" accepts your recommendation.

**Discover first, ask second.** Before asking anything, look at the repo and find what the code already answers: toolchain markers (`.uvprojx`, `.ioc`, `CMakeLists.txt`, `Makefile`, `*.ld`), RTOS directories (`FreeRTOS`, `RT-Thread`, and so on), vendor library folders (`HAL`, `stdperiph`, `cmsis`), and standards documents (for example a company C coding standard). Only ask the engineer what the code cannot tell you.

## Round 1: product and platform

- **Product domain** - what kind of product is this? (energy-storage BMS, motor control, IoT, medical, consumer, other.) The domain tells later skills which regulations and idioms matter; it is never a hard-coded assumption.
- **MCU / SoC** - vendor and family (STM32, GD32, NXP, Renesas, ESP32, and so on). A project may target several; list them all.
- **Other compute** - does the project also run on Linux (C/C++) or depend on Python scripts (host tools, data processing)? If so, note their role as auxiliary.

## Round 2: firmware facts

- **Driver library** - what does driver code build on? The rule is the vendor's official, still-maintained library (HAL, standard peripheral library, LL, or bare registers), chosen per chip. Never assume one abstraction covers every chip in the project.
- **Scheduling model** - bare-metal, FreeRTOS, RT-Thread, another RTOS, or mixed. If mixed, say which parts use which.
- **Languages** - C, C++, assembly. Assembly is for startup / interrupt / timing-critical paths unless the engineer says otherwise.
- **Build toolchain** - Keil MDK, STM32CubeIDE, IAR, GCC + CMake/Make, other. Note the flash/debug probe (J-Link, ST-Link, and so on).

## Round 3: standards and logs

- **Coding standard** - which standard does this project follow (a company internal doc, MISRA-C:2012 or 2004, ISO 26262 coding rules, none)? Where is the source document?
- **Compliance** - does the product need MISRA-C or another international standard, and which version? Is it already enforced by a tool (lint, PC-lint, static analyser)?
- **Log placement** - how are captured artifacts stored? Ask for each of: protocol captures (CAN/LIN/UART), waveforms (oscilloscope / logic analyser), serial logs, crash dumps, register dumps. Record exact directory paths and naming rules. These feed `log-analyze`, so they must be exact.

## Write the context file

Write `.spike-engineer-flow/context.md` at the project root, one section per round, plain markdown. Record "unknown" or "N/A" rather than guessing a fact. Close by telling the engineer: every other skill reads this file, so when a fact changes, run this skill again.
