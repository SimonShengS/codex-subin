# Custom Profile calibration worksheet

Use this worksheet to adapt Subin to your own workload. It is a decision aid, not a mechanical validation protocol.

## Context

- Review date:
- Codex version and surface:
- Account/model availability:
- Current Profile:
- Reason for recalibration:

## Workload

| Work type | Representative tasks | Frequency | Failure cost | Latency sensitivity | Verification strength |
|---|---|---:|---:|---:|---|
| `default` | | | | | |
| `explorer` | | | | | |
| `analyst` | | | | | |
| `worker` | | | | | |
| `verifier` | | | | | |
| `reviewer` | | | | | |
| `deep_reviewer` | | | | | |

## Candidate mapping

| Role | Current model/effort | Candidate model/effort | Evidence and rationale | Rollback choice |
|---|---|---|---|---|
| `default` | | | | |
| `explorer` | | | | |
| `analyst` | | | | |
| `worker` | | | | |
| `verifier` | | | | |
| `reviewer` | | | | |
| `deep_reviewer` | | | | |

## Evidence

Record official support separately from third-party benchmarks and local inference. Include retrieval dates, sample sizes where available, observed quality, duration, cost, and uncertainty.

## Check

After applying a candidate, restart Codex, run a Focused Probe for changed roles, and try representative tasks. Record runtime actual model/effort, pass/fail/insufficient evidence, unexpected behavior, and whether to retain or revert the mapping.
