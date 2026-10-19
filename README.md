# spike-engineer-flow

一套开源的、**拷问式自适应**的嵌入式产品软件开发 skill 家族（Claude Code 插件）。

覆盖嵌入式产品从需求到文档的完整生命周期，但**不做任何死板假设**：产品领域、芯片厂商与驱动库、RTOS 调度模型、编码标准、MISRA 等国际标准——全部在运行时拷问使用者后适配，而不是写死在 skill 里。因此它既能用于储能 BMS，也能用于电机控制、IoT、医疗等任何嵌入式产品。

## 设计原则

- **拷问式自适应**：一切领域相关项运行时询问，不预设。
- **事实归 agent，决策归工程师**：能从代码 / 文档查到的由 agent 自己查，关键决策（安全、时序、硬件相关）回交工程师。
- **硬件现实**：嵌入式无法纯软件模拟，验证依赖工程师线下抓取的报文 / 波形 / 日志，agent 离线分析。

## 六段全流程

> **元能力**：不知道从哪开始 → **`ask-spike`**（路由器）；难题要多个专家视角讨论 → **`round-table`**（多代理圆桌辩论，收敛可靠方案）。

| 段 | 目录 | skill（计划） |
|---|---|---|
| 0 proj-cfg（项目配置） | `skills/00-proj-cfg` | `proj-cfg` ✅ |
| 1 规格 | `skills/01-spec` | `interrogate` ✅（拷问 + ADR + 术语表）→ `spec`（正式规格） |
| 2 设计 | `skills/02-design` | `design`（模块 / 外设 / API 设计）→ `senior-en` ✅（设计评审 + 验证前代码评审，拷问与建议并行） |
| 3 实现 | `skills/03-impl` | `refactor-port` ✅ + `driver-dev`（芯片驱动）+ `app-logic`（应用层） |
| 4 验证 | `skills/04-verify` | `verify`（静态 + 单测）→ 直接 `code-review`；`log-analyze`（随时调用，查逻辑 / 找 bug）+ `hw-test`（实机验证） |
| 5 评审 | `skills/05-review` | `code-review`（双轴：规范 + 规格） |
| 6 文档 | `skills/06-docs` | datasheet 摘要 / 寄存器手册 / 模块说明 |
| 辅助 | `skills/tools` | `newbie` ✅ + `cn_trans` ✅ + `git-commit` ✅ + `build-flash` + `protocol-tools` |

**正常流程**：`interrogate → spec → design → senior-en（评设计）→ driver-dev / app-logic → verify → code-review → docs`。`senior-en` 在 verify 前可询问是否评代码；`log-analyze` 及其它工具类 skill 随时调用，不入正常流程。

## 安装

本仓库自带 `.claude-plugin/marketplace.json`，可作为一个 Claude Code 插件市场安装：

```bash
claude plugin marketplace add spike-engineer-flow https://github.com/<你的账号>/spike-engineer-flow
claude plugin install spike-engineer-flow@spike-engineer-flow
```

（本地开发期也可直接把 `skills/` 下的目录软链进 `~/.claude/skills/`。）

## 使用

项目接入 spike 流时先运行 `proj-cfg`（新项目，或衍生 / 修改既有项目）：它会拷问平台 / 芯片 / RTOS / 编码标准 / 日志放置方式，生成 `.spike-engineer-flow/context.md`。其余所有 skill 都读这个文件，不再重复询问；项目事实变化时重跑一次即可。

## License

MIT
