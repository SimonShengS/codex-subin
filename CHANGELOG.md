# Changelog

All notable changes to Codex Subin are documented here.

## [Unreleased]

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
