# Codex Subin

**Put the right model on the right kind of work.**

Codex Subin is an opinionated reference kit for routing Codex subagents by **work type** and pinning an appropriate model and reasoning effort for each route. "Subin" evokes both *substitute in* and *subagent*: bring in a specialist only when its kind of work is useful.

This repository is not an installer, automatic router, benchmark leaderboard, or claim of a permanently optimal configuration. It gives advanced individual users and small teams a transparent starting point that can be inspected, adapted, and re-tested as models and Codex change.

[简体中文](README.zh-CN.md)

## Quick start

1. Choose [`quality`](profiles/quality/PROFILE.md) (recommended) or [`efficient`](profiles/efficient/PROFILE.md).
2. Review the seven TOML files in that Profile Package.
3. Copy or carefully merge them into the custom-agent directory used by your Codex installation.
4. Optionally merge [`examples/AGENTS.fragment.md`](examples/AGENTS.fragment.md) into your global or project instructions and review [`examples/session-defaults.toml`](examples/session-defaults.toml).
5. Restart Codex, then run the read-only [`Full Runtime Probe`](prompts/verify-runtime.md).

Paths, supported fields, and account/model availability can differ by Codex release and environment. Consult the current [official subagents documentation](https://developers.openai.com/codex/subagents/) before applying a Profile.

## Seven work-type roles

| Role | Use it for | Do not use it for |
|---|---|---|
| `default` | General delegated work when no specialist fits | Pretending that a named route was activated |
| `explorer` | Read-only discovery of code, configuration, data, sources, and execution paths | Designing or implementing the solution |
| `analyst` | Comparing approaches, architecture, causal reasoning, and financial-thesis synthesis | Editing files or executing a decided implementation |
| `worker` | Scoped implementation after direction is sufficiently determined | Expanding scope or making unresolved public decisions |
| `verifier` | Tests, reproduction, regression, data reconciliation, calculation, and source validation | Open-ended critique or fixing findings |
| `reviewer` | Routine bounded review for defects, regressions, maintainability, ordinary security risks, requirement gaps, and missing tests | Premise-level system or thesis challenge |
| `deep_reviewer` | Cross-boundary challenge of completed systems, research analyses, or financial theses | Most ordinary code reviews or explicit acceptance checks |

These roles cover three common domains without changing their semantics:

- software work: discovery → design → implementation → verification → review;
- research and financial analysis: evidence discovery → thesis synthesis → calculation/source verification → premise-level challenge;
- tools and configuration: inspect state → reason about alternatives → make a bounded change → verify runtime behavior.

Delegation is selective, not a mandatory seven-stage pipeline. A task should use only the smallest useful set of roles.

## Why work types, not personas

OpenAI's [custom-agent guidance](https://developers.openai.com/codex/subagents/) recommends narrow, clearly described jobs and instructions that keep an agent from drifting into adjacent work. Subin extends that guidance with a design inference: define routes by observable work boundaries rather than simulated personalities or job titles.

A work type can state its objective, authoritative inputs, write authority, evidence standard, output, and stop conditions. A persona often entangles tone, status, expertise, and permission, making routing and runtime verification less precise. This is a Subin design choice, not an OpenAI prohibition on persona prompts.

## Recommended Profiles

A **Profile** maps only subagent roles. Root and Plan settings are separate [Session Defaults](#session-defaults).

### Quality (recommended)

| Role | Model | Effort | Reasoning posture |
|---|---|---:|---|
| `default` | `gpt-5.6-sol` | `medium` | Balanced fallback |
| `explorer` | `gpt-5.6-luna` | `max` | Cheap, persistent read-heavy discovery |
| `analyst` | `gpt-5.6-sol` | `max` | High-value design and synthesis |
| `worker` | `gpt-5.6-sol` | `medium` | Frequent implementation with balanced latency |
| `verifier` | `gpt-5.6-sol` | `medium` | Objective checks with explicit criteria |
| `reviewer` | `gpt-5.6-sol` | `xhigh` | Strong routine artifact review |
| `deep_reviewer` | `gpt-5.6-sol` | `max` | Premise and cross-boundary challenge |

### Efficient

The Efficient Profile is identical except for `worker`, which uses `gpt-5.6-luna / max`. It targets lower cost, **not necessarily lower latency**.

| Changed role | Quality | Efficient |
|---|---|---|
| `worker` | `gpt-5.6-sol / medium` | `gpt-5.6-luna / max` |

Both packages contain all seven TOMLs and preserve identical role instructions. There is no hidden inheritance chain.

## Choosing a Profile

Start with Quality when correctness and effect matter more than token cost, especially when implementation often crosses unfamiliar code or configuration. Try Efficient when most worker tasks are sharply bounded, easy to verify, and cost matters more than elapsed time.

Do not mechanically raise every role to `max`. Effort is not a universal quality ladder: a higher setting may consume more time and tokens without improving a particular workload. Route high-reasoning work to `analyst`, `reviewer`, or `deep_reviewer`; keep frequent execution and explicit verification bounded.

## Concurrency and hierarchy

Subin recommends a high-capacity ceiling of ten spawned-agent threads for users who have parallel workloads:

```toml
[agents]
max_concurrent_threads_per_session = 10
```

The cap excludes Root and is capacity, not a target. A normal task still uses only the smallest useful set of roles. Ten role instances do not mean ten new role types: Subin retains the same seven work types.

The AGENTS fragment permits one level of on-demand re-delegation without separate Root authorization. A first-generation subagent may create independently bounded children when this materially improves parallelism, context isolation, or independent evidence; every child must be marked as a non-redelegating leaf. The resulting maximum logical hierarchy is Root → subagent → leaf subagent.

Current public Codex configuration exposes no supported `agents.max_depth` setting, so concurrency is runtime-enforced while logical depth is instruction-governed. Do not introduce an intermediate manager merely to form a hierarchy, and never allow overlapping parallel writers.

The initial implementation has a dated [two-level runtime probe](docs/runtime/2026-08-05-two-level-probe.md): it observed an authoritative depth-2 leaf and Root plus four simultaneously running child agents. The configured ceiling of ten was intentionally not saturated, so ten-way concurrency remains a configuration claim rather than benchmark evidence.

## Session Defaults

[`examples/session-defaults.toml`](examples/session-defaults.toml) is a **minimal fragment**, not a complete `config.toml`:

```toml
model = "gpt-5.6-sol"
model_reasoning_effort = "medium"
plan_mode_reasoning_effort = "max"

[agents]
max_concurrent_threads_per_session = 10
default_subagent_model = "gpt-5.6-sol"
default_subagent_reasoning_effort = "medium"
```

The Root remains responsible for scope, decisions, integration, final validation, and completion claims. `ultra` can be selected for a top-level session when available, but it is deliberately not a custom-agent Profile default. See the current [Codex model documentation](https://developers.openai.com/codex/models/) for supported models and effort levels.

## Apply manually or ask Codex

Manual application is safest when you already understand every active configuration layer. If you prefer agent-assisted application, use [`prompts/apply-profile.md`](prompts/apply-profile.md). It instructs Codex to inspect first, preserve unrelated settings, show conflicts, make only authorized changes, and avoid claiming runtime activation from files alone.

Subin intentionally ships no installer, generator, or configuration manager. Your local conventions and Codex version remain authoritative.

## Verify the runtime

Configuration declarations are not runtime proof. After applying a Profile, restart Codex and use [`prompts/verify-runtime.md`](prompts/verify-runtime.md).

The probe separates:

1. requested `agent_type`;
2. authoritative host metadata such as `session_meta.agent_role`;
3. actual model and effort from runtime turn context;
4. `multi_agent_version` and injected role instructions when exposed;
5. configuration declarations;
6. a bounded Root → subagent → leaf probe when nested delegation is configured;
7. fields the current interface cannot observe.

Never infer activation from a TOML filename, file existence, task name, task path, or a child's self-description. Run a **Full Probe** after initial installation, a Codex upgrade, or a broad Profile change. Run a **Focused Probe** after changing one route.

## Recalibrate, do not canonize

Model behavior is dynamic. Availability, implementation, effort semantics, latency, price, and benchmark results can change independently. Treat these Profiles as dated hypotheses:

1. define your real work types and failure costs;
2. check current official support;
3. inspect current third-party and local evidence;
4. change one mapping at a time when possible;
5. run a Focused Runtime Probe and representative tasks;
6. record the date, rationale, and remaining uncertainty.

[`profiles/custom/PROFILE-TEMPLATE.md`](profiles/custom/PROFILE-TEMPLATE.md) provides a lightweight worksheet. It is guidance, not a mechanical acceptance system.

## Benchmark evidence

The initial choices considered a dated [2026-08-05 CodexRadar snapshot](docs/benchmarks/2026-08-05-codexradar.md). [CodexRadar](https://codexradar.com/) and its [Chinese dashboard](https://deng.codexradar.com/) are third-party sources, not OpenAI evaluations. Their IQ, duration, and estimated cost are useful signals, not universal truth.

The snapshot helps explain why this release does not choose `Sol/high`, why frequent work begins at `Sol/medium`, and why `Luna/max` is attractive for discovery and a cost-efficient worker. The repository does not promise those relationships will persist.

## Compatibility and limitations

- The package targets Codex installations that expose custom subagents with per-role model and effort settings.
- Account entitlements and client releases may reject a model even when a configuration file parses.
- Multi-agent runtime behavior is version-dependent. Use `agents.max_concurrent_threads_per_session` for an explicit cap; do not use the legacy `agents.max_threads` alias or an unsupported `agents.max_depth` key.
- An unavailable metadata field is **unobservable**, not automatically pass or fail.
- Financial examples concern research workflow only; Subin provides no trading instruction.
- Profiles are reference material. Back up and review local configuration before changing it.

## Contributing and license

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for evidence and consistency expectations. Design decisions live in [`docs/adr`](docs/adr), and terminology lives in [`CONTEXT.md`](CONTEXT.md).

Codex Subin is released under the [MIT License](LICENSE).
