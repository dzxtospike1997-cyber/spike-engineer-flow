---
name: protocol-tools
description: "Help with communication protocol work: parse and generate frames (CAN, I2C, SPI, UART, Modbus, Ethernet, and others), build DBC files, and script protocol capture analysis. Ask which protocol and bus are in use, then adapt. Use for protocol-related tooling."
---

Help with communication protocol work. Ask which protocol and bus are involved rather than assuming.

## 1. Ask the protocol

Ask the engineer which protocol and bus: CAN (with DBC?), I2C, SPI, UART, Modbus RTU/TCP, Ethernet, or a custom frame. Read `.spike-engineer-flow/context.md` and the log placement to see what the project already uses.

## 2. Do the protocol work

Depending on the need:

- Parse captured frames (from `log-analyze`'s artifacts) into fields, matching the protocol definition.
- Generate frames or a frame builder for testing.
- Build or check a DBC file (CAN signal definitions) against the frame layout.
- Script the capture / decode / compare loop in Python where the project uses Python.

## 3. Report

Report the parsed or generated result, and flag any field that does not match the protocol definition. Do not invent a protocol definition; ask the engineer for the authoritative source (DBC, datasheet, spec).
