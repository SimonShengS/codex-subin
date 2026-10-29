# Premium Profile

Premium is an optional higher-tier Profile for demanding work whose failure cost justifies evaluating Astra routes. Quality remains the daily recommendation. Premium is a dated routing hypothesis, not a demonstrated quality ranking or a promise of faster execution.

| Role | Model | Effort |
|---|---|---:|
| `default` | `gpt-6-astra` | `medium` |
| `explorer` | `gpt-6.1-sol` | `low` |
| `analyst` | `gpt-6-astra` | `high` |
| `worker` | `gpt-6-astra` | `medium` |
| `verifier` | `gpt-6-astra` | `medium` |
| `reviewer` | `gpt-6-astra` | `high` |
| `deep_reviewer` | `gpt-6-astra` | `xhigh` |

## Decision record

- Design date: 2026-10-29.
- Official support: the [Astra model documentation](https://developers.openai.com/api/docs/models/gpt-6-astra) lists `low`, `medium`, `high`, `xhigh`, and `max`; the [model-selection guide](https://developers.openai.com/api/docs/guides/model-selection) positions Astra/medium for complex, broad-context tasks and Astra/xhigh for demanding analysis. These capability statements do not validate Subin's individual role assignments.
- Local inference: retain Sol 6.1/low for focused discovery; use Astra/medium for general delegated work, implementation, and objective verification; use Astra/high for synthesis and bounded review; reserve Astra/xhigh for premise-level and cross-boundary challenge.
- Runtime status: Premium has not undergone a post-restart Runtime Probe. Historical benchmark and runtime notes cover other mappings and cannot establish Premium activation.
- Rollback choice: restore the complete [Quality package](../quality/PROFILE.md), restart Codex, and run a [Full Runtime Probe](../../prompts/verify-runtime.md).

## Fixed division of work

Choose roles by their work boundaries, not to obtain a different model or effort. Explorer returns focused evidence; Analyst compares approaches and synthesizes conclusions; Worker implements a decided scope; Verifier checks explicit criteria; Reviewer reviews a bounded artifact; Deep Reviewer challenges premises and cross-boundary behavior. Default remains the fallback when no specialist fits.

All seven TOMLs are self-contained and preserve Quality's descriptions, permissions, and instructions. Only `model` and `model_reasoning_effort` differ. Provider-specific agents, including codebase-memory extensions, remain outside this package.

Root/Plan Session Defaults, the seven-spawned-thread concurrency ceiling, and the bounded Root → subagent → leaf hierarchy remain independent of Profile selection. This Profile does not change [`examples/session-defaults.toml`](../../examples/session-defaults.toml).

## Representative evaluation

Compare Premium with Quality on the same inputs and acceptance criteria before making it a routine choice:

- discovery of an unfamiliar execution path with precise source references;
- architecture or research synthesis with competing explanations and explicit unknowns;
- a scoped cross-module implementation followed by reproducible tests;
- objective reconciliation of calculations or source claims;
- bounded artifact review and independent premise-level challenge.

Comparative quality, elapsed time, and consumption remain unverified. Record task outcomes, elapsed time, and available token/cost evidence separately from runtime routing. A successful runtime probe would establish activation, not superiority on these tasks.
