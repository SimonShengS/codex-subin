# Quality Profile

Quality is the recommended Codex Subin Profile. It favors outcome quality while keeping frequent implementation and explicit verification at a balanced setting.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6-sol` | `medium` |
| `explorer` | `gpt-6-luna` | `max` |
| `analyst` | `gpt-6-astra` | `high` |
| `worker` | `gpt-6-sol` | `high` |
| `verifier` | `gpt-6-sol` | `medium` |
| `reviewer` | `gpt-6-sol` | `xhigh` |
| `deep_reviewer` | `gpt-6-astra` | `medium` |

## Decision record

- Profile reviewed: 2026-09-23.
- Runtime evidence: [seven-role probe](../../docs/runtime/2026-09-23-gpt6-family-probe.md) passed for Quality. Efficient's worker route was not separately tested.
- Historical benchmark input (GPT-5.6 only, not Astra evidence): [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-6-sol / medium`.

Use a Full Runtime Probe after installation or a Codex upgrade. This package's TOMLs are configuration declarations, not proof that a route was activated.

The optional Session Defaults set `agents.max_concurrent_threads_per_session = 7`. This is a capacity ceiling for spawned threads, excluding Root, not a target agent count. The accompanying AGENTS fragment permits one bounded level of on-demand re-delegation: Root → subagent → leaf. Current public configuration has no supported `agents.max_depth` key, so the logical depth is instruction-governed and must be runtime-probed.

## Why these settings

- `explorer` gets GPT-6 Luna/max for bounded read-only discovery. Compare completeness and latency on representative tasks.
- `analyst` gets Astra/high for alternatives, architecture, and synthesis; `deep_reviewer` gets Astra/medium for independent premise-level challenge.
- `default` and `verifier` get GPT-6 Sol/medium; `worker` gets Sol/high for scoped implementation, debugging, and fixes.
- `reviewer` gets GPT-6 Sol/xhigh for bounded artifact review. Choose deep_reviewer by the nature of the work, not the numeric effort.

The Profile does not specify Root or Plan defaults. See [`examples/session-defaults.toml`](../../examples/session-defaults.toml).

This mapping is a dated maintainer preference, not a measured GPT-6 ranking. Use representative discovery, implementation, review, and analysis tasks to recalibrate. To roll back, restore the previous profile revision from Git and repeat the affected runtime probe.
