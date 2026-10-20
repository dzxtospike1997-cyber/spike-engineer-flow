---
name: log-analyze
description: "Analyze offline captured artifacts (protocol captures, waveforms, serial logs, crash dumps) to verify code logic and find bugs. On-demand, not part of the normal flow; asks a mandatory set of questions about log placement and analysis goals, and can output a capture list for the engineer to fetch. Use whenever a bug or logic needs on-target evidence."
---

Analyze the artifacts the engineer captured offline, to verify code logic or find a bug. You cannot run the hardware yourself; the engineer captures, you analyze.

## 1. Mandatory interview

Ask these before analyzing, one at a time:

1. **Log placement** - where do captured artifacts live, and what is the naming rule? Discover the directory structure yourself first.
2. **Folder contents** - what does each folder hold: protocol captures, waveforms, serial logs, crash dumps, register dumps?
3. **What to verify** - which function or logic is being analyzed or verified?
4. **What bug to find** - what is the symptom: dropped frame, timing error, wrong register, random reset, data overflow?
5. **Capture list (reverse)** - if the engineer has not captured yet, output a capture list first: which signals, what trigger, what sample rate or baud rate. The engineer captures against the list, puts the files back, and you analyze.

## 2. Read the artifacts

Read the relevant captures, waveforms, and logs from the paths the engineer gave. Cross-check the observed behaviour against the design and spec (REQ-IDs) and the chip's documented behaviour.

## 3. Analyze and report

Report what the artifacts show, where they diverge from the expected behaviour, and the most likely cause. Distinguish proven facts from hypotheses, and say what additional capture would confirm each hypothesis. Do not claim a root cause you have not seen in the data.
