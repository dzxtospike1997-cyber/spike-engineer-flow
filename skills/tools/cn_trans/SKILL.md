---
name: cn_trans
description: "Translate a skill document (SKILL.md or any markdown doc) into Simplified Chinese and write the result beside the original as <name>.zh.md. Use when the user wants a Chinese version of a skill or doc."
---

Translate a skill document into Simplified Chinese and save the translation next to the original, so the source stays intact and the Chinese copy sits side by side for reference.

## Target and output

- Default target: the `SKILL.md` the user points at (or the one in scope). Any markdown doc works the same way.
- Output name: insert `.zh` before the extension. `SKILL.md` -> `SKILL.zh.md`, `README.md` -> `README.zh.md`.
- Write into the same directory as the original. Never overwrite the original.

## Translation rules

1. Translate prose into natural, precise technical Simplified Chinese, in a formal engineering register that matches the repo.
2. Leave untranslated: code, identifiers, file paths, commands and their flags, URLs, JSON keys, and YAML frontmatter keys. Keep the frontmatter `name` unchanged; leave `description` in English unless the user asks to translate it too.
3. Preserve markdown structure exactly: headings, tables, lists, code fences, link targets. Translate heading text and body text; keep link URLs and anchors intact.
4. Match the document's own formatting conventions (blank-line style, punctuation, list markers) rather than imposing a generic style.
5. One file in, one file out.

## Before writing

If the target file or output name is not obvious, confirm them with the user, then write the translated file into the original's directory.
