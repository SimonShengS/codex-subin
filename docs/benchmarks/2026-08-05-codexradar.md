# CodexRadar snapshot — 2026-08-05

This is a dated third-party observation used to calibrate Codex Subin v0.1.0. It is not an OpenAI evaluation and should not be treated as a permanent ranking.

## Sources and method

- Dashboard: [codexradar.com](https://codexradar.com/)
- Chinese dashboard and FAQ: [deng.codexradar.com](https://deng.codexradar.com/)
- Data retrieved: 2026-08-05 01:54:24 +08:00
- Dataset: 112 valid tasks for each listed model/effort point; 21 points in the source snapshot
- Activity totals at retrieval: 867 runs in 24 hours, 1,886 in 48 hours, 21,910 total
- Reported method: latest valid result per task; IQ = pass rate × 150; duration = mean latest duration; price = mean latest measured/estimated task cost under the source's methodology

CodexRadar describes its tasks as real open-source repository tasks evaluated in clean server-side environments. Cost remains an estimate influenced by pricing assumptions, token accounting, caching, and incomplete samples. Consult the source for its current methodology.

## Decision-relevant points

| Model / effort | IQ | Passed / valid tasks | Average duration | Average cost | Average agent steps |
|---|---:|---:|---:|---:|---:|
| `gpt-5.6-sol / medium` | 89.73 | 67 / 112 | 17.27 min | $3.71 | 65.10 |
| `gpt-5.6-sol / high` | 85.71 | 64 / 112 | 20.81 min | $4.64 | 69.95 |
| `gpt-5.6-sol / xhigh` | 107.14 | 80 / 112 | 25.64 min | $6.38 | 80.38 |
| `gpt-5.6-sol / max` | 103.12 | 77 / 112 | 34.39 min | $9.64 | 105.84 |
| `gpt-5.6-luna / max` | 97.77 | 73 / 112 | 31.02 min | $0.46 | 117.82 |

Rounded values are presented for readability. The source is dynamic, so a later visit may show different values.

## How the snapshot influenced v0.1.0

- Subin does not choose Sol/high in this release: in this snapshot it was slower, more expensive, and lower-IQ than Sol/medium.
- Sol/medium is the frequent-work baseline for default, worker, and verifier: it offered a strong latency/quality balance.
- Sol/xhigh is pinned to routine reviewer: review quality matters, but this role remains distinct from open-ended system or thesis analysis.
- Sol/max is pinned to analyst and deep_reviewer. Although Sol/xhigh had a higher aggregate IQ in this snapshot, max was retained for the project's high-value, long-horizon reasoning posture; this is a workload judgment, not a claim that max universally wins.
- Luna/max is pinned to explorer and used by the Efficient worker. It combined strong aggregate results with dramatically lower estimated cost, but its average duration was longer than Sol/medium.

## Limits

Aggregate IQ does not isolate role-specific performance, and a 112-task benchmark cannot represent every repository, research domain, tool environment, or failure cost. Model implementations and effort behavior can change after this snapshot. Recalibrate with current official support, current third-party data, and representative local tasks; then verify actual runtime routing.
