# Quality Profile

Quality is the recommended Codex Subin Profile. It favors outcome quality while keeping frequent implementation and explicit verification at a balanced setting.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6.1-sol` | `medium` |
| `explorer` | `gpt-6.1-sol` | `low` |
| `analyst` | `gpt-6.1-sol` | `xhigh` |
| `worker` | `gpt-6.1-sol` | `high` |
| `verifier` | `gpt-6.1-sol` | `medium` |
| `reviewer` | `gpt-6.1-sol` | `xhigh` |
| `deep_reviewer` | `gpt-6.1-sol` | `max` |

## Decision record

- Profile reviewed: 2026-10-01.
- Runtime evidence: [lightweight Sol 6.1 probe](../../docs/runtime/2026-10-01-sol61-probe.md) observed every Quality route with the expected model, effort, and role. Efficient's worker route was not separately tested.
- Historical benchmark input (GPT-5.6 only, not Astra evidence): [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-6.1-sol / medium`.

Use a Full Runtime Probe after installation or a Codex upgrade. This package's TOMLs are configuration declarations, not proof that a route was activated.

The optional Session Defaults set `agents.max_concurrent_threads_per_session = 7`. This is a capacity ceiling for spawned threads, excluding Root, not a target agent count. The accompanying AGENTS fragment permits one bounded level of on-demand re-delegation: Root → subagent → leaf. Current public configuration has no supported `agents.max_depth` key, so the logical depth is instruction-governed and must be runtime-probed.

## Why these settings

- Every role uses GPT-6.1 Sol, with fixed effort selected by work type. [Official model guidance](https://developers.openai.com/api/docs/models/gpt-6.1-sol) supports the configured effort values; this is not evidence that any effort matches Astra's quality.
- `explorer` gets low for focused read-only discovery and returns evidence and gaps. Alternatives, causal synthesis, and architecture decisions belong to `analyst`.
- `analyst` gets xhigh for alternatives, architecture, and synthesis; `deep_reviewer` gets max for independent premise-level and cross-boundary challenge.
- `default` and `verifier` get medium; `worker` keeps high for scoped implementation, debugging, and fixes.
- `reviewer` keeps xhigh for bounded artifact review. Choose deep_reviewer by the nature of the work, not the numeric effort.

The Profile does not specify Root or Plan defaults. See [`examples/session-defaults.toml`](../../examples/session-defaults.toml).

This mapping is a dated maintainer preference, not a measured GPT-6.1 ranking. Runtime routing passed a minimal probe; quality, latency, and cost still need representative discovery, implementation, review, and analysis tasks. To roll back, restore the previous mixed-model profile revision from Git and repeat the affected runtime probe.
