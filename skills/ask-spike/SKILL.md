---
name: ask-spike
description: "Router for spike-engineer-flow. Check the repo for what already exists, ask the engineer where their project stands and what they need, then recommend which skill to use and where to start. Use when the engineer is unsure which skill to reach for."
---

Route the engineer to the right skill based on where their project is and what they need. Do not start the work yourself; your job is to point at the right skill and hand off.

## 1. Check what already exists

Look at the repo before asking. Facts you can find yourself:

- `.spike-engineer-flow/context.md` - has `proj-cfg` been run? If missing, the project is not configured yet.
- `docs/adr/`, `docs/glossary.md` - has `interrogate` produced decisions and terms?
- spec and design documents - is there a spec or a design doc already?
- the working tree - is there uncommitted code, or a branch mid-review?

## 2. Ask where they are and what they need

Ask the engineer, concisely and one question at a time, what they want to do right now. You only need enough to route; do not interrogate the requirement itself (that is `interrogate`'s job).

## 3. Recommend a skill

| Situation | Skill |
|---|---|
| No context.md yet | `proj-cfg` |
| New requirement, not yet clear | `interrogate` |
| Requirement clear, need a formal spec | `spec` |
| Need module / peripheral / API design | `design` |
| Design ready, want it reviewed | `senior-en` (design review) |
| Want to write a chip driver | `driver-dev` |
| Want to write application / business logic | `app-logic` |
| Want to port or refactor a module | `refactor-port` |
| Code written, want to verify | `verify` |
| Want a code-design review before verify | `senior-en` (code review) |
| Have captured logs / waveforms, want to find a bug or verify logic | `log-analyze` |
| Want a code review | `code-review` |
| Want to write docs | `docs` |
| Want to commit | `git-commit` |
| A term or logic is hard to understand | `newbie` |
| Want to translate a skill doc to Chinese | `cn_trans` |

State the recommendation, why, and the rest of the path from there (for example: "start with `interrogate`, then `spec`, then `design`"). If the situation is ambiguous, ask one more question rather than guessing. If a routed skill is not built yet, say so and describe what it will do.

## 4. Hand off

Tell the engineer which skill to invoke, or offer to invoke it. Do not perform that skill's work here.
