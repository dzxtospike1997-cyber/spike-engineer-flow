# spike-engineer-flow

An open-source, **interview-first adaptive** skill family for embedded product software development (a Claude Code plugin).

It covers the full lifecycle of an embedded product from requirements to documentation, but **makes no rigid assumptions**: the product domain, chip vendor and driver library, RTOS scheduling model, coding standard, and international standards such as MISRA are all adapted by interviewing the user at runtime rather than hard-coded into the skills. It therefore works as well for an energy-storage BMS as it does for motor control, IoT, medical, or any other embedded product.

## Design principles

- **Interview-first adaptive**: every domain-specific item is asked at runtime, never presumed.
- **Facts belong to the agent, decisions to the engineer**: whatever the agent can find from code or docs it finds itself; the key decisions (safety, timing, hardware-related) go back to the engineer.
- **Hardware reality**: embedded work cannot be simulated in software alone; verification relies on the messages / waveforms / logs the engineer captures offline, which the agent analyzes offline.

## The six-stage pipeline

> **Meta-skills**: not sure where to start → **`ask-spike`** (router); a hard problem needs several expert views → **`round-table`** (multi-agent round-table debate that converges on a robust solution).

| Stage | Directory | Skills |
|---|---|---|
| 0 proj-cfg (project config) | `skills/00-proj-cfg` | `proj-cfg` ✅ |
| 1 spec | `skills/01-spec` | `interrogate` ✅ (interview + ADR + glossary) → `spec` ✅ (REQ-ID + traceability matrix) |
| 2 design | `skills/02-design` | `design` ✅ (module / peripheral / API design) → `senior-en` ✅ (review, grilling and advice in parallel) |
| 3 impl | `skills/03-impl` | `driver-dev` ✅ + `app-logic` ✅ + `refactor-port` ✅ |
| 4 verify | `skills/04-verify` | `verify` ✅ (static + unit test + measure) → `code-review`; `log-analyze` ✅ (call anytime) + `hw-test` ✅ (on-hardware verification) |
| 5 review | `skills/05-review` | `code-review` ✅ (two axes: standard + spec, back-fills the traceability matrix) |
| 6 docs | `skills/06-docs` | `docs` ✅ (datasheet summary / register manual / module notes) |
| tools | `skills/tools` | `newbie` ✅ + `cn_trans` ✅ + `git-commit` ✅ + `measure` ✅ + `build-flash` ✅ + `protocol-tools` ✅ |

**Normal flow**: `interrogate → spec → design → senior-en (review design) → driver-dev / app-logic → verify → code-review → docs`. Before `verify`, `senior-en` may offer to review the code; `log-analyze` and the other tool skills are called anytime and are not part of the normal flow.

## Install

This repository ships a `.claude-plugin/marketplace.json`, so it can be installed as a Claude Code plugin marketplace:

```bash
claude plugin marketplace add spike-engineer-flow https://github.com/<your-account>/spike-engineer-flow
claude plugin install spike-engineer-flow@spike-engineer-flow
```

(During local development you can also symlink the directories under `skills/` into `~/.claude/skills/`.)

## Usage

When a project joins the spike flow, run `proj-cfg` first (new project, or a derived / modified existing project): it interviews you for the platform / chip / RTOS / coding standard / log placement, and generates `.spike-engineer-flow/context.md`. Every other skill reads that file and never asks again; re-run it when the project facts change.

## License

MIT
