# Changelog

All notable changes to Codex Subin are documented here.

## [Unreleased]

### Unified GPT-6.1 Sol Profile — 2026-10-01

- Unified Quality on GPT-6.1 Sol with fixed work-type efforts: default/medium, explorer/low, analyst/xhigh, worker/high, verifier/medium, reviewer/xhigh, and deep_reviewer/max.
- Updated Efficient's six shared roles; retained its optional GPT-6 Luna/max worker.
- Updated bilingual guidance and optional Session Defaults to Sol 6.1/high with a Sol 6.1/medium subagent fallback; left Plan effort unset.
- Documented optional codebase-memory effort pins without bundling installation-specific MCP configuration.
- Added a sanitized lightweight v2 probe confirming Root and all seven Quality routes, plus three existing codebase-memory extensions. No comparative quality, latency, cost, nested-depth, or saturation claim is made.
- Preserved historical benchmarks and runtime probes.

### GPT-6 family refresh — 2026-09-23

- Synced Quality with the accepted seven-role Sol/Luna/Astra mapping; analyst uses Astra/high.
- Updated Efficient's optional worker to GPT-6 Luna/max.
- Set the reference concurrency ceiling to seven spawned agents and the optional subagent fallback to Sol/medium.
- Added a sanitized seven-role v2 runtime probe: all returned READY; Root plus seven children were observed running. No long-task quality or stability claim is made.


### Astra profile refresh — 2026-09-07

- Migrated Quality to GPT-6 Astra: analyst/xhigh, deep_reviewer/high, explorer/low, and default/worker/verifier/reviewer/medium.
- Updated Efficient's shared roles; retained its optional Luna/max worker.
- Updated bilingual guidance and session defaults (Astra/medium, Plan/xhigh).
- Kept historical benchmarks and probes unchanged; they do not establish Astra performance or activation.


- Added the modern `agents.max_concurrent_threads_per_session = 10` reference ceiling.
- Allowed bounded first-generation subagents to re-delegate once without separate Root authorization.
- Required nested children to remain non-redelegating leaves and documented the Root → subagent → leaf logical hierarchy.
- Extended the bilingual Runtime Probe to distinguish configured concurrency from observed concurrency and verify authoritative depth metadata.

## [0.1.0] - 2026-08-05

- Published the seven-role work-type routing model.
- Added complete Quality and Efficient Profile Packages.
- Added bilingual application and read-only runtime-probe prompts.
- Added optional Session Defaults and a mergeable AGENTS fragment.
- Recorded the dated CodexRadar evidence used for initial calibration.
- Documented the project's reference-kit boundary and core design decisions.
