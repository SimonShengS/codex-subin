# Codex Subin

**让合适的模型，在合适的工作中替补上场。**

Codex Subin 是一套有明确观点、但可自行调整的 Codex subagent 参考方案：先按**工作类型**划分路由，再为每种工作固定合适的模型与推理档位。名称 `Subin` 同时呼应 *substitute in*（替补上场）与 *subagent*。

本项目不是安装器、自动路由器、排行榜或“永久最优配置”的承诺。它为高级个人用户和小团队提供一个透明起点：可以审阅、修改，并在模型和 Codex 更新后重新验证。

[English](README.md)

## 快速开始

1. 选择 [`quality`](profiles/quality/PROFILE.md)（推荐）或 [`efficient`](profiles/efficient/PROFILE.md)。
2. 审阅该 Profile Package 中的七个 TOML 文件。
3. 将它们复制或谨慎合并到你的 Codex 自定义 Agent 目录。
4. 按需把 [`examples/AGENTS.fragment.md`](examples/AGENTS.fragment.md) 合并到全局或项目指令，并审阅 [`examples/session-defaults.toml`](examples/session-defaults.toml)。
5. 重启 Codex，运行只读的 [`完整运行时探针`](prompts/verify-runtime.zh-CN.md)。

不同 Codex 版本和环境的路径、支持字段、账号模型权限可能不同。应用 Profile 前，请查看最新的 [官方 subagents 文档](https://developers.openai.com/codex/subagents/)。

## 七种工作类型

| 角色 | 适用工作 | 不应用于 |
|---|---|---|
| `default` | 没有专门角色适配时的通用委派 | 假装某个命名路由已经激活 |
| `explorer` | 只读发现代码、配置、数据、来源与执行路径 | 设计或实现方案 |
| `analyst` | 比较方案、架构、因果分析与金融论点综合 | 修改文件或执行已经确定的实现 |
| `worker` | 方向充分明确后的有界实现 | 扩大范围或擅自决定未解决的公共语义 |
| `verifier` | 测试、复现、回归、数据核对、计算与来源验证 | 开放式批判或修复发现的问题 |
| `reviewer` | 对有界变更做常规审查：缺陷、回归、可维护性、普通安全风险、需求偏差与缺失测试 | 质疑整个系统或论点的根本前提 |
| `deep_reviewer` | 对完整系统、研究分析或金融论点做跨边界与前提级挑战 | 大多数普通代码审查或明确的验收检查 |

同一套角色可覆盖三类常见工作：

- 软件生命周期：发现 → 设计 → 实现 → 验证 → 审查；
- 调研和金融分析：证据发现 → 论点综合 → 计算/来源验证 → 前提级挑战；
- 工具与配置：检查状态 → 分析选项 → 有界修改 → 验证运行时行为。

委派是选择性的，不是强制执行七段流水线。每个任务只使用最小且有价值的角色集合。

## 为什么按工作类型，而不是模拟人格

OpenAI 的[自定义 Agent 指南](https://developers.openai.com/codex/subagents/)建议为 Agent 定义狭窄、清晰的工作，并用指令阻止它漂移到相邻任务。Subin 在此基础上做出一项设计推论：用可观察的工作边界定义路由，而不是模拟性格或职位。

工作类型可以明确目标、权威输入、写权限、证据标准、输出与停止条件。人格提示词容易把语气、地位、能力和权限混在一起，路由及运行时验收都更难精确。这是 Subin 的设计选择，并非 OpenAI 禁止使用人格提示词。

## 推荐 Profile

**Profile** 只映射 subagent 角色。Root 与 Plan 档位属于独立的[会话默认值](#会话默认值)。

### Quality（推荐）

| 角色 | 模型 | 档位 | 设计意图 |
|---|---|---:|---|
| `default` | `gpt-6-astra` | `medium` | 平衡的兜底路由 |
| `explorer` | `gpt-6-astra` | `low` | 低推理开销的有界只读发现 |
| `analyst` | `gpt-6-astra` | `xhigh` | 高价值方案设计与综合分析 |
| `worker` | `gpt-6-astra` | `medium` | 高频实现与延迟之间的平衡 |
| `verifier` | `gpt-6-astra` | `medium` | 针对明确标准的客观验证 |
| `reviewer` | `gpt-6-astra` | `medium` | 有界的常规产物审查 |
| `deep_reviewer` | `gpt-6-astra` | `high` | 前提与跨边界挑战 |

### Efficient

Efficient 仅修改 `worker`：改用 `gpt-5.6-luna / max`。它追求更低成本，**不保证更快**。

| 变化角色 | Quality | Efficient |
|---|---|---|
| `worker` | `gpt-6-astra / medium` | `gpt-5.6-luna / max` |

两套包都包含完整七个 TOML，角色指令完全相同，不存在隐式继承链。

## 如何选择

如果你更在意结果质量而非 token 成本，尤其实现经常跨越陌生代码或配置，先用 Quality。若多数实现任务边界非常清楚、容易验证，并且成本比耗时更重要，可以试用 Efficient。

不要机械地把所有角色升到 `max`。Effort 不是放之四海皆准的质量阶梯：更高档位可能增加时间和 token，却不改善特定工作。把高推理需求路由给 `analyst` 或 `deep_reviewer`，让高频实现和明确验证保持有界。

## 并发与层级

对于确有并行工作负载的用户，Subin 推荐把子 Agent 线程容量上限设为 10：

```toml
[agents]
max_concurrent_threads_per_session = 10
```

这个上限不包含 Root，而且只是容量，不是目标数量。普通任务仍然只使用最小且有价值的角色集合。十个角色实例不等于新增十种角色；Subin 仍然只有七种工作类型。

AGENTS 片段允许一层无需 Root 单独授权的按需再委派。第一层子 Agent 可以在确实改善并行、上下文隔离或独立证据时创建有界子任务，并必须把每个子节点标记为不得再委派的叶子。最大逻辑结构是 Root → subagent → leaf subagent。

当前公开的 Codex 配置没有受支持的 `agents.max_depth`，因此并发上限由运行时执行，逻辑深度由指令约束。不要为了形成层级而创建中间 manager，也不得制造重叠的并行写入。

初始实现已有一份带日期的[两层运行时探针](docs/runtime/2026-08-05-two-level-probe.md)：权威元数据实际观察到 depth=2 的叶子，以及 Root 与四个同时运行的子 Agent。测试有意没有占满十个线程，因此十并发仍是配置声明，而不是基准证据。

## 会话默认值

[`examples/session-defaults.toml`](examples/session-defaults.toml) 是**最小片段**，不是完整 `config.toml`：

```toml
model = "gpt-6-astra"
model_reasoning_effort = "medium"
plan_mode_reasoning_effort = "xhigh"

[agents]
max_concurrent_threads_per_session = 10
default_subagent_model = "gpt-6-astra"
default_subagent_reasoning_effort = "medium"
```

Root 继续负责范围、决策、集成、最终验证和完成声明。环境支持时，可以为顶层会话手动选择 `ultra`，但它不是自定义 Agent Profile 的默认档位。模型与档位支持情况以最新 [Codex 模型文档](https://developers.openai.com/codex/models/)为准。

## 手动应用或让 Codex 协助

如果你了解所有生效的配置层，手动合并最稳妥。若希望让 Agent 协助，使用 [`prompts/apply-profile.zh-CN.md`](prompts/apply-profile.zh-CN.md)。提示词要求 Codex 先检查、保留无关配置、展示冲突、只做已授权变更，并且不从文件存在推断运行时已激活。

Subin 有意不提供安装器、生成器或配置管理器。本地约定和 Codex 版本始终优先。

## 验证真实运行时

配置声明不等于运行时证据。应用 Profile 并重启 Codex 后，使用 [`prompts/verify-runtime.zh-CN.md`](prompts/verify-runtime.zh-CN.md)。

探针区分：

1. 请求的 `agent_type`；
2. `session_meta.agent_role` 等宿主侧权威元数据；
3. 运行时 turn context 中的实际模型与 effort；
4. 接口可见时的 `multi_agent_version` 与注入角色指令；
5. 配置文件声明；
6. 配置嵌套委派时的有界 Root → subagent → leaf 探针；
7. 当前接口不可观测的字段。

不得根据 TOML 文件名、文件存在、task name、task path 或子 Agent 自我描述推断激活。首次安装、Codex 升级或整体 Profile 变化后运行**完整探针**；只修改单个路由后运行**聚焦探针**。

## 动态校准，不要神化配置

模型表现是动态的。可用性、实现、effort 语义、延迟、价格和基准结果可能独立变化。把这些 Profile 当作有日期的假设：

1. 定义你的真实工作类型和失败代价；
2. 检查当前官方支持；
3. 查看最新第三方及本地证据；
4. 尽量一次只调整一个映射；
5. 运行聚焦运行时探针和代表性任务；
6. 记录日期、理由及剩余不确定性。

[`profiles/custom/PROFILE-TEMPLATE.md`](profiles/custom/PROFILE-TEMPLATE.md) 提供轻量校准表。它是参考，不是机械验收系统。

## 基准证据

初始配置参考了有明确日期的 [2026-08-05 CodexRadar 快照](docs/benchmarks/2026-08-05-codexradar.md)。[CodexRadar](https://codexradar.com/) 及其[中文面板](https://deng.codexradar.com/)属于第三方来源，并非 OpenAI 官方评测。IQ、耗时和估算成本是有价值的信号，不是普遍真理。

这份快照解释的是初始 GPT-5.6 选择，包括当时避开 Sol/high 的原因，不能用于评判 Astra。2026-09-07 的更新采用 Astra：analyst/xhigh、deep_reviewer/high、explorer/low，其余角色/medium。这是维护者选择的起点，本次没有新增 Astra 基准或运行时验收报告。Efficient 仅为可选 worker 保留 Luna/max，实际成本与耗时需用自己的任务重新比较。

## 兼容性与限制

- 方案面向支持自定义 subagent 且可逐角色设置 model/effort 的 Codex 环境。
- 即使配置可解析，账号权限或客户端版本仍可能拒绝某个模型。
- 多 Agent 运行时行为随版本变化；显式上限使用 `agents.max_concurrent_threads_per_session`，不要使用旧的 `agents.max_threads` 别名或不受支持的 `agents.max_depth`。
- 元数据字段不可用时，结果是**不可观测**，不能自动判为通过或失败。
- 金融示例只描述研究流程，不构成交易指令。
- Profile 是参考材料；修改前请备份并审阅本地配置。

## 贡献与许可

证据和一致性要求见 [`CONTRIBUTING.md`](CONTRIBUTING.md)。设计决策位于 [`docs/adr`](docs/adr)，术语位于 [`CONTEXT.md`](CONTEXT.md)。

Codex Subin 采用 [MIT License](LICENSE)。
