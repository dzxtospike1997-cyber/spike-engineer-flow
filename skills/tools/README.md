# tools — auxiliary stage

Build / communication / documentation / explanation helpers.

- **`newbie`** (landed): explains a confusing concept, a new term, or a complex piece of logic in plain words plus an everyday example, then maps it back to the real context.
- **`cn_trans`** (landed): translates a skill doc into Simplified Chinese, writing `<name>.zh.md` next to the original.
- **`git-commit`** (landed): analyzes the working tree before committing, explains the functional and logical impact of the changes, lists what will be committed, and commits only after the engineer confirms.
- **`measure`** (landed): real measurement — reads flash / RAM usage and worst-case stack depth from the `.map` / `size` / stack analysis, and checks functional partition boundaries (bootloader / app / config regions).
- **`build-flash`** (landed): build + optional flash / debug (asked every time, never automatic); calls `measure` for the real numbers; runs in a temporary sub-agent so the main context only gets a summary.
- **`protocol-tools`** (landed): communication protocol tools (CAN / I2C / SPI / UART / Modbus / Ethernet…, asks the protocol first, then adapts) — parse / build frames, DBC, capture scripts.
