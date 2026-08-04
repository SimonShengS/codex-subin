# Quality Profile

Quality is the recommended Codex Subin Profile. It favors outcome quality while keeping frequent implementation and explicit verification at a balanced setting.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-5.6-sol` | `medium` |
| `explorer` | `gpt-5.6-luna` | `max` |
| `analyst` | `gpt-5.6-sol` | `max` |
| `worker` | `gpt-5.6-sol` | `medium` |
| `verifier` | `gpt-5.6-sol` | `medium` |
| `reviewer` | `gpt-5.6-sol` | `xhigh` |
| `deep_reviewer` | `gpt-5.6-sol` | `max` |

## Decision record

- Profile reviewed: 2026-08-05.
- Reference runtime: Codex `0.146.0-alpha.9.2`; runtime behavior remains environment-dependent.
- Benchmark input: [CodexRadar snapshot dated 2026-08-05](../../docs/benchmarks/2026-08-05-codexradar.md).
- Fallback route: `gpt-5.6-sol / medium`.

Use a Full Runtime Probe after installation or a Codex upgrade. This package's TOMLs are configuration declarations, not proof that a route was activated.

## Why these settings

- `explorer` gets Luna/max because discovery is read-heavy, independently bounded, and benefits from persistence more than premium synthesis.
- `analyst` and `deep_reviewer` get Sol/max because they carry high-value design, causal, and premise-level reasoning.
- `worker` and `verifier` get Sol/medium because they are frequent and should operate within decided scope or explicit criteria.
- `reviewer` gets Sol/xhigh because routine review is important and adversarial, but distinct from premise-level deep review.

The Profile does not specify Root or Plan defaults. See [`examples/session-defaults.toml`](../../examples/session-defaults.toml).
