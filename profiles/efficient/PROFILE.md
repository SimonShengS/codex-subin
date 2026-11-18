# Efficient Profile

Efficient is a cost-efficiency variant of the Quality Profile. It changes only `worker` to Luna/max and does not promise lower latency.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6.2-sol` | `medium` |
| `explorer` | `gpt-6.2-sol` | `low` |
| `analyst` | `gpt-6.2-sol` | `xhigh` |
| `worker` | `gpt-6-luna` | `max` |
| `verifier` | `gpt-6.2-sol` | `medium` |
| `reviewer` | `gpt-6.2-sol` | `xhigh` |
| `deep_reviewer` | `gpt-6.2-sol` | `max` |

## Decision record

- Model pins refreshed: 2026-11-18. The Luna/max worker, role semantics, and efforts are unchanged.
- Runtime evidence: the [2026-10-01 probe](../../docs/runtime/2026-10-01-sol61-probe.md) verified the previous GPT-6.1 Sol routes shared with Quality. It did not test Efficient's Luna/max worker or GPT-6.2 activation.
- Historical benchmark input (GPT-5.6 only): [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-6.2-sol / medium`.

Choose this Profile when worker tasks are sharply bounded and independently verifiable, and cost matters more than elapsed time. The retained Luna worker is an optional cost-oriented candidate; compare cost, latency, and correctness with Quality on your own tasks. Use Quality for a unified GPT-6.2 Sol configuration or when worker tasks routinely require synthesis across unfamiliar boundaries.

The optional Session Defaults set `agents.max_concurrent_threads_per_session = 7`. This is a capacity ceiling for spawned threads, excluding Root, not a target agent count. The accompanying AGENTS fragment permits one bounded level of on-demand re-delegation: Root → subagent → leaf. Current public configuration has no supported `agents.max_depth` key, so the logical depth is instruction-governed and must be runtime-probed.

All semantic role fields are identical to Quality. This package is complete and does not inherit from Quality.

To roll back the model refresh, restore the previous Profile revision from Git, restart Codex, and run a Full Runtime Probe.
