# Quality Profile

Quality is the recommended Codex Subin Profile. It favors outcome quality while keeping frequent implementation and explicit verification at a balanced setting.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6-astra` | `medium` |
| `explorer` | `gpt-6-astra` | `low` |
| `analyst` | `gpt-6-astra` | `xhigh` |
| `worker` | `gpt-6-astra` | `medium` |
| `verifier` | `gpt-6-astra` | `medium` |
| `reviewer` | `gpt-6-astra` | `medium` |
| `deep_reviewer` | `gpt-6-astra` | `high` |

## Decision record

- Profile reviewed: 2026-09-07.
- Runtime compatibility: confirm Astra and per-role effort support in your client; this refresh does not ship a new runtime acceptance report.
- Historical benchmark input (GPT-5.6 only, not Astra evidence): [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-6-astra / medium`.

Use a Full Runtime Probe after installation or a Codex upgrade. This package's TOMLs are configuration declarations, not proof that a route was activated.

The optional Session Defaults set `agents.max_concurrent_threads_per_session = 10`. This is a capacity ceiling for spawned threads, excluding Root, not a target agent count. The accompanying AGENTS fragment permits one bounded level of on-demand re-delegation: Root → subagent → leaf. Current public configuration has no supported `agents.max_depth` key, so the logical depth is instruction-governed and must be runtime-probed.

## Why these settings

- `explorer` gets Astra/low for bounded evidence discovery with a focus on response time; the serialized effort is `low`, not `light`.
- `analyst` gets Astra/xhigh for alternatives, architecture, and synthesis; `deep_reviewer` gets Astra/high for independent premise-level challenge.
- `default`, `worker`, and `verifier` get Astra/medium for frequent, bounded work with clear objectives.
- `reviewer` gets Astra/medium for routine bounded reviews. Choose deep_reviewer for premise-level work rather than raising effort based on importance.

The Profile does not specify Root or Plan defaults. See [`examples/session-defaults.toml`](../../examples/session-defaults.toml).

This mapping is a dated maintainer preference, not a measured Astra ranking. Use representative discovery, implementation, review, and analysis tasks to recalibrate. To roll back, restore a pre-Astra revision from Git and repeat the affected runtime probe.
