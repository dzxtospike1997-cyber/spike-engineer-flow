# 00-proj-cfg 项目配置段

家族的入口：项目配置（新项目，或衍生 / 修改既有项目）。

- **`proj-cfg`**（已落地）：拷问使用者（产品领域 / 芯片 / 芯片资料路径 / 分区〔flash / RAM / 栈 / no-init / 边界重叠〕/ 驱动库 / 调度模型 / 工具链 / 编码标准 / 日志放置方式），生成 `.spike-engineer-flow/context.md`，供其余所有 skill 读取。

其余段 skill 都不再重复询问项目事实，只读这个 context 文件。
