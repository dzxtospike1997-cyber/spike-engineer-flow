---
name: pieces
description: "Before implementation, split settled work into small ordered pieces sized to one session each, and track each piece's progress percentage so a long job can be resumed across short sessions without losing context or focus."
---

Break settled work into small ordered pieces before implementation, and keep each piece's progress recorded, so no session grows long enough for attention to degrade and the next session can resume from the first unfinished piece.

## 1. When to run

Run after `design` (or a review's整改 list) settles what to build, and before `driver-dev` / `app-logic` / `refactor-port` start writing code. Skip when the work already fits in one session.

## 2. Divide into pieces

Read the design or spec and split the implementation into pieces:

- **Order by dependency** - a piece whose prerequisites are not yet done comes later (the same frontier idea as `interrogate`).
- **Size to one session** - each piece should be small enough to finish and verify in a single focused session, and no smaller than useful. Size is the point: do not make one giant piece that spans many sessions.
- **Name each piece** with its goal, the files it touches, a done-criterion (what makes it 100%), and its dependencies.

## 3. Write the piece board

Persist the pieces to `.spike-engineer-flow/pieces.md` (create it if absent). Keep a status table at the top and one section per piece:

    # Implementation pieces

    | # | Piece | Depends on | Progress | Status |
    |---|-------|-----------|----------|--------|
    | 1 | UART RX only stores bytes | - | 100% | done |
    | 2 | Move CAN dispatch to 1ms task | 1 | 40% | in-progress |
    | 3 | NVIC priority layout | - | 0% | todo |

    ## 1. UART RX only stores bytes
    - Goal: ...
    - Files: ...
    - Done when: ...
    - Progress: 100% - done, committed.

Every piece carries a `Progress` percentage and a status (`todo` / `in-progress` / `done`).

## 4. Work one piece per session

Pick the first `todo` piece whose dependencies are all `done`, set it `in-progress`, and do it. Update its `Progress` as it advances, not only at the end. When its done-criterion is met, set it `done` at 100% and note what was finished.

## 5. Update progress as you go

After any meaningful step, update the piece's `Progress` and what is left, so an interrupted session leaves an honest board.

## 6. Hand off

When every piece is `done`, hand the work to `verify`. If the session ends first, the board is the handoff: the next session reads `.spike-engineer-flow/pieces.md`, picks the first unfinished piece, and continues.
