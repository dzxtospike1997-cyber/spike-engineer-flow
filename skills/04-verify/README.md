# 04-verify — verification stage

Embedded work is tightly coupled to hardware; there is no pure-software simulation, so verification relies on the artifacts the engineer captures offline.

Normal flow: after `verify` go straight to `code-review` (the 05 review stage); `log-analyze` is not part of the normal flow.

For hardware-coupled modules, prefer the closed loop "test → capture → log-analyze → fix → re-test", but **not every module needs captured logs** — pure logic / algorithm modules only need `verify` (static + unit test).

Skills:
- **`verify`** (landed): the part that can run on a machine — static checks + unit tests (first split host-testable vs must-run-on-board), and calls `measure` to check partition boundaries. Before starting, asks whether to call `senior-en` to review the code.
- **`log-analyze`** (landed): **call anytime, not part of the normal flow**, for verifying code logic and finding bugs. Analyzes messages / waveforms / logs offline; a mandatory 5-question interview plus a reverse-produced "capture list".
- **`hw-test`** (landed): on-hardware / hardware-in-the-loop verification — plans the test, specifies what to capture, guides the engineer through running the hardware, and hands the evidence to `log-analyze`.
