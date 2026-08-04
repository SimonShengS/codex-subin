# 应用 Codex Subin Profile

在需要配置的 Codex 环境中使用本提示词。把 `<PROFILE>` 替换为 `quality` 或 `efficient`，并让 Codex 能读取本仓库。

```text
把 Codex Subin 的 <PROFILE> Profile 应用到当前 Codex 环境。

约束：
- 编辑前检查当前 Codex 配置、自定义 Agent 目录以及实际适用的 AGENTS 指令。
- 把所选 Profile Package 视为参考输入，不得据此覆盖无关设置。
- 使用当前环境的正常安全方式备份或保留原状态。
- 逐字段比较七个目标 Agent TOML。保留无关 Agent 和无关配置，除非它们与所选 Profile 冲突。
- 对任何实质冲突、不支持字段、账号/模型可用性问题或生效指令冲突，先展示再修改受影响项目。
- Root/Plan 的 Session Defaults 与 subagent Profile 分开。只有我明确授权时，才应用 examples/session-defaults.toml。
- 当 multi-agent v2 运行时自行管理并发时，不要加入旧的 agents.max_threads 或 depth 限制。
- 不得根据文件存在、文件名、task name、task path、预期映射或子 Agent 自述推断运行时激活。
- 不安装额外插件、工具或验证框架。

完成已授权编辑后：
1. 使用当前可用的原生或标准解析器解析每个被修改的 TOML；
2. 报告哪些文件/设置被修改，哪些被保留；
3. 把配置声明与运行时事实分开报告；
4. 提醒我重启 Codex；
5. 重启后，使用 prompts/verify-runtime.zh-CN.md 执行相应的只读探针。

只有权威运行时证据支持时，才能声明角色已成功激活。接口无法提供的运行时字段必须标记为“不可观测”。
```
