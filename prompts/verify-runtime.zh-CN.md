# 只读运行时探针

首次安装、Codex 升级或整体 Profile 变化后使用**完整探针**。只修改一个角色映射后使用**聚焦探针**。

```text
执行一次只读的 Codex Subin 运行时验收探针。不要修改配置或项目文件。

探针模式：<完整或聚焦>
预期 Profile：<quality、efficient，或提供的 custom matrix>
聚焦角色（如适用）：<角色列表>

证据规则：
- 严格区分：(1) 配置文件声明，(2) 权威运行时元数据，(3) 当前接口不可观测字段。
- 不得根据 TOML 存在、文件名、task_name、task path、预期映射或子 Agent 自述推断运行时角色。
- 首先检查当前 spawn 接口是否真正提供 custom role / agent_type 选择器。
- 如果没有，只运行一个 generic/default 只读探针，并记录“当前接口无法观测命名路由”。不要用 task name 模拟角色。
- 如果提供，使用 fork_turns="none" 启动所需角色。每个任务必须有界且只读，并发量不得超过运行时允许范围。
- 对每个子 Agent，在接口提供时检查宿主侧结构化证据：请求的 agent_type、session_meta.agent_role、turn_context 的 model/effort、multi_agent_version、注入的 developer instructions。
- role 字段为 null 或缺失不自动代表成功或失败；必须说明因此无法观测的具体项目。
- 子 Agent 的文字自述不是权威运行时证据。

完整探针的层级检查：
- 给一个第一层角色两个相互独立的只读证据维度，要求它无需向 Root 请求单独授权，自行判断并执行最小且有价值的子委派。
- 最多允许它启动一个子节点。启动方必须明确告诉子节点：它是不得继续委派的叶子；随后由启动方返回一个汇总结果。
- 接口可见时，从权威 session metadata 检查父子关系和 depth，并确认叶子没有下级节点或 spawn 调用。
- 默认不要占满配置并发上限。若要确认新上限突破了旧运行时限制，只使用刚好超过旧上限的最小叶子集合，并只报告已经证明的并发下界。

对每个探针角色报告：
- 预期 model 和 effort；
- 配置声明的 model 和 effort；
- 请求的 agent_type；
- 权威运行时 role / agent_type；
- 权威运行时 model 和 effort；
- 接口可见时的 multi_agent_version；
- 是否可观察到对应自定义 TOML 的指令被注入；
- 适用时，嵌套探针的 parent/depth 与叶子状态；
- 不可观测字段；
- 结果：通过、失败、仅配置确认、当前接口不可观测。

只有权威元数据可见时才报告 Root 的运行时 model/effort。不得从 config.toml 推断 Root 实际值。

输出一个表格：
| 验收项 | 预期 | 配置声明 | 运行时实际 | 证据来源 | 结果 |

最后直接回答：
1. default 是否实际路由到预期 model/effort？
2. 每个命名角色是否实际激活对应 TOML？
3. multi-agent v2 是否可观测且已激活？
4. 第一层 Agent 是否无需 Root 单独授权就完成了再委派，且子节点是否保持为叶子？
5. 实际观察到的并发是多少，它与配置上限有何区别？
6. 哪些结论仍不可观测？
7. 是否修改了任何文件？要求答案为“否”。
```
