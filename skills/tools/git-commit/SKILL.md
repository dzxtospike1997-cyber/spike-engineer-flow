---
name: git-commit
description: "Prepare a commit safely: analyze the working tree, explain the functional and logical impact of the changes in plain language, show exactly what will be committed, propose a commit message, and commit only after the engineer confirms. Use before every git commit."
---

Prepare a commit, but never commit silently. The engineer must see, in plain language, what the changes *do* and exactly what goes into the commit, and confirm before anything is committed.

## 1. Discover the working tree

Run and read:

- `git status --short --branch`
- `git diff --stat` and `git diff --cached --stat`
- the actual diffs (`git diff` for unstaged, `git diff --cached` for staged)
- `git log -5 --oneline` to match the repo's recent message style

Note what is staged, unstaged, and untracked. If nothing is staged and nothing untracked, say so and stop.

## 2. Explain functional and logical impact

Read the diff and explain, in plain language, what the change *does*: the behaviour it adds, changes, or removes, and the logic it touches. Group by intent, not by file. For each group say what changed and why it matters. Do not just list filenames; describe the function and logic the diff alters.

## 3. Show what will be committed

Present a review card before committing:

- the files to commit, with `+/-` line counts
- staged vs unstaged vs untracked, and which of these will actually go into the commit
- the proposed commit message

Then wait. Do not stage, unstage, or commit until the engineer confirms.

## 4. Commit message

Propose a message in the repo's existing style (default to Conventional Commits: `feat`, `fix`, `refactor`, `docs`, `chore`). Keep the subject under 72 chars. Offer to edit it.

## 5. Commit only on confirmation

After the engineer confirms both the change set and the message, stage exactly those files and commit. If asked to push, push only what was committed.
