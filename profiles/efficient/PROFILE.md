# Efficient Profile

Efficient is a cost-efficiency variant of the Quality Profile. It changes only `worker` to Luna/max and does not promise lower latency.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6.1-sol` | `medium` |
| `explorer` | `gpt-6.1-sol` | `low` |
| `analyst` | `gpt-6.1-sol` | `xhigh` |
| `worker` | `gpt-6-luna` | `max` |
| `verifier` | `gpt-6.1-sol` | `medium` |
| `reviewer` | `gpt-6.1-sol` | `xhigh` |
| `deep_reviewer` | `gpt-6.1-sol` | `max` |

## Decision record

- Profile reviewed: 2026-10-01.
- Runtime evidence: [lightweight Sol 6.1 probe](../../docs/runtime/2026-10-01-sol61-probe.md) observed every Quality route. Efficient shares its six non-worker mappings; Efficient's Luna/max worker was not separately tested.
- Historical benchmark input (GPT-5.6 only, not Astra evidence): [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-6.1-sol / medium`.

Choose this Profile when worker tasks are sharply bounded and independently verifiable, and cost matters more than elapsed time. The historical snapshot compared GPT-5.6 variants and does not establish relative GPT-6 or GPT-6.1 performance or costs. The retained Luna worker is an optional cost-oriented candidate; validate current cost, latency, and correctness on your own tasks. Use Quality for a unified Sol 6.1 configuration or when worker tasks routinely require stronger synthesis across unfamiliar boundaries.

The optional Session Defaults set `agents.max_concurrent_threads_per_session = 7`. This is a capacity ceiling for spawned threads, excluding Root, not a target agent count. The accompanying AGENTS fragment permits one bounded level of on-demand re-delegation: Root → subagent → leaf. Current public configuration has no supported `agents.max_depth` key, so the logical depth is instruction-governed and must be runtime-probed.

All semantic role fields are identical to Quality. This package is complete and does not inherit from Quality.

This mapping is a dated maintainer preference, not a measured GPT-6.1 ranking. Use representative discovery, implementation, review, and analysis tasks to recalibrate. To roll back, restore the previous profile revision from Git and repeat the affected runtime probe.
