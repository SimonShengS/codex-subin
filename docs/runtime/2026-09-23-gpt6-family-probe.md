# GPT-6 family runtime probe — 2026-09-23

Sanitized maintainer acceptance record after a local configuration repair and restart.

## Method

Seven probes selected their named agent_type with fork_turns="none", without explicit model/effort overrides. Each was instructed to reply READY without tools, edits, or delegation.
Roles were read from session_meta.agent_role; actual model, effort, and multi_agent_version came from turn_context. Parent linkage associated the records with this probe. Filenames, task paths, and child self-reports were not used to infer roles. Private identifiers and raw logs are omitted.

| Role | Observed model | Observed effort | Protocol | Result |
|---|---|---|---|---|
| default | gpt-6-sol | medium | v2 | READY |
| explorer | gpt-6-luna | max | v2 | READY |
| analyst | gpt-6-astra | high | v2 | READY |
| worker | gpt-6-sol | high | v2 | READY |
| verifier | gpt-6-sol | medium | v2 | READY |
| reviewer | gpt-6-sol | xhigh | v2 | READY |
| deep_reviewer | gpt-6-astra | medium | v2 | READY |

The global config parsed with agents.max_concurrent_threads_per_session = 7. A live listing observed Root and all seven children running; all seven later returned READY.

The repaired Root file default was Astra/medium. That is a configuration observation, not proof of the running Root selection. Named roles retained their explicit settings.

## Limits

This verifies named routing and minimal execution in one installation, not comparative quality, speed, cost, or sustained-load stability.
Nested delegation was not retested. Efficient's Luna/max worker and unpinned codebase-memory roles were outside the probe.
The session-defaults example is optional: its Sol/medium fallback for unpinned agents and Plan/xhigh are recommendations, not a claim that the tested installation configured those defaults.
