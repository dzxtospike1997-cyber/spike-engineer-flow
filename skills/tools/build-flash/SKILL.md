---
name: build-flash
description: "Build the firmware, optionally flash and debug it, then get real resource numbers via measure. Flash/debug is optional and asked each time; the heavy work runs in a temporary sub-agent so the build log stays out of the main context. Use for the build -> flash -> observe loop."
---

Run the build -> flash -> observe loop without polluting the main conversation. The heavy work happens in a temporary sub-agent; the main context only sees the result.

## 1. Prepare

Read `.spike-engineer-flow/context.md` for the toolchain, chip, build output directory, and memory partition layout. If the build command or output location is not obvious from the repo, ask the engineer once.

## 2. Build (in a sub-agent)

Dispatch a temporary sub-agent to run the build. It identifies the toolchain (Keil MDK, STM32CubeIDE, IAR, GCC + CMake/Make), runs the actual build, and reports back: success or failure, the error list, and where the artifacts landed (`.map`, `.elf`, `.hex` / `.bin`). Keep the full build log in the sub-agent; bring back only the summary.

## 3. Ask about flash and debug

Ask the engineer whether they want to flash and/or debug this time. Do not assume; flash and debug are not part of every build. Skip them when the engineer declines.

## 4. Measure

Call `measure` on the build artifacts for real flash / RAM usage, worst-case stack, and the partition boundary verdict. Do not estimate these yourself.

## 5. Report

Report a concise summary: build result, flash / debug result (if done), the measurement numbers, and any errors or boundary overflows.
