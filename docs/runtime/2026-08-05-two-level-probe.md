# Two-level delegation runtime probe — 2026-08-05

This read-only probe checked the first Subin release after enabling the optional ten-thread ceiling and bounded on-demand re-delegation. It distinguishes configuration declarations from authoritative runtime metadata and from untested claims.

## Environment

- Codex client metadata: `0.147.0-alpha.1.2`
- Multi-agent runtime metadata: `v2`
- Configured spawned-thread ceiling: `10`, excluding Root
- Probe writes: none

## Evidence

| Claim | Evidence | Result |
|---|---|---|
| First-generation agent can re-delegate without a separate authorization round | The depth-1 `explorer` independently created one bounded child during its assigned acceptance task | Passed |
| Nested child actually ran at depth 2 | Child `session_meta` reported `depth=2` and a parent thread; parent reported `depth=1` | Passed |
| Named route and model mapping remained active | Parent and child metadata reported role `explorer`; turn context reported `gpt-5.6-luna / max` | Passed |
| Child remained a leaf | No descendant thread and no child spawn call were observed before completion | Passed |
| Runtime exceeded the previous Root-plus-three observation | Root and four child agents were simultaneously `running` | Passed; observed lower bound is four spawned threads |
| Runtime supports the full configured ceiling of ten | The probe deliberately did not saturate ten threads | Not tested; configuration only |

## Interpretation

The probe establishes the two-level Root → subagent → leaf path and proves at least four concurrently running spawned agents in this environment. It does not prove that every client or account accepts the same ceiling, and it does not claim ten-way concurrency without a saturation test. Rerun the bilingual Full Runtime Probe after a Codex upgrade or material hierarchy change.
