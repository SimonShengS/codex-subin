# Quality Profile

Quality is the recommended Codex Subin Profile. It favors outcome quality while keeping frequent implementation and explicit verification at a balanced setting.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6.2-sol` | `medium` |
| `explorer` | `gpt-6.2-sol` | `low` |
| `analyst` | `gpt-6.2-sol` | `xhigh` |
| `worker` | `gpt-6.2-sol` | `high` |
| `verifier` | `gpt-6.2-sol` | `medium` |
| `reviewer` | `gpt-6.2-sol` | `xhigh` |
| `deep_reviewer` | `gpt-6.2-sol` | `max` |

## Decision record

- Model pins refreshed: 2026-11-18. Role semantics and efforts are unchanged.
- Runtime evidence: the [2026-10-01 probe](../../docs/runtime/2026-10-01-sol61-probe.md) verified the previous GPT-6.1 Sol routes, not GPT-6.2 activation.
- Historical benchmark input (GPT-5.6 only): [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-6.2-sol / medium`.

Use a Full Runtime Probe after installation, a Codex upgrade, or a broad Profile change. This package's TOMLs are configuration declarations, not proof that a route was activated.

The optional Session Defaults set `agents.max_concurrent_threads_per_session = 7`. This is a capacity ceiling for spawned threads, excluding Root, not a target agent count. The accompanying AGENTS fragment permits one bounded level of on-demand re-delegation: Root → subagent → leaf. Current public configuration has no supported `agents.max_depth` key, so the logical depth is instruction-governed and must be runtime-probed.

## Why these settings

- Every role uses [GPT-6.2 Sol](https://developers.openai.com/api/docs/models/gpt-6.2-sol), with fixed effort selected by work type.
- `explorer` gets low for focused read-only discovery and returns evidence and gaps. Alternatives, causal synthesis, and architecture decisions belong to `analyst`.
- `analyst` gets xhigh for alternatives, architecture, and synthesis; `deep_reviewer` gets max for independent premise-level and cross-boundary challenge.
- `default` and `verifier` get medium; `worker` keeps high for scoped implementation, debugging, and fixes.
- `reviewer` keeps xhigh for bounded artifact review. Choose deep_reviewer by the nature of the work, not the numeric effort.

The Profile does not specify Root or Plan defaults. See [`examples/session-defaults.toml`](../../examples/session-defaults.toml).

This mapping is a maintainer preference. Use representative discovery, implementation, review, and analysis tasks to compare quality, latency, and cost. To roll back, restore the previous GPT-6.1 Sol Profile revision from Git, restart Codex, and run a Full Runtime Probe.
