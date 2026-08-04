# Efficient Profile

Efficient is a cost-efficiency variant of the Quality Profile. It changes only `worker` to Luna/max and does not promise lower latency.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-5.6-sol` | `medium` |
| `explorer` | `gpt-5.6-luna` | `max` |
| `analyst` | `gpt-5.6-sol` | `max` |
| `worker` | `gpt-5.6-luna` | `max` |
| `verifier` | `gpt-5.6-sol` | `medium` |
| `reviewer` | `gpt-5.6-sol` | `xhigh` |
| `deep_reviewer` | `gpt-5.6-sol` | `max` |

## Decision record

- Profile reviewed: 2026-08-05.
- Reference runtime: Codex `0.146.0-alpha.9.2`; runtime behavior remains environment-dependent.
- Benchmark input: [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-5.6-sol / medium`.

Choose this Profile when worker tasks are sharply bounded and independently verifiable, and cost matters more than elapsed time. Luna/max was materially cheaper in the dated third-party snapshot, but it also took longer on average than Sol/medium. Use Quality when worker tasks routinely require stronger synthesis across unfamiliar boundaries.

All semantic role fields are identical to Quality. This package is complete and does not inherit from Quality.
