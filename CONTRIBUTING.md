# Contributing

Codex Subin is a small reference kit. Contributions should make its decisions easier to inspect and adapt, not turn it into a configuration manager.

## Principles

- Route by bounded work type, not simulated persona.
- Keep `quality` and `efficient` as complete seven-file packages.
- Preserve role semantics across Profiles; a Profile difference should normally be limited to `model` and `model_reasoning_effort`.
- Separate official capability claims from third-party observations and local inference.
- Date benchmark evidence and never present a transient ranking as permanent.
- Require runtime evidence for activation claims; file presence is configuration evidence only.
- Keep the English and Chinese READMEs structurally aligned.
- Do not add credentials, personal paths, session identifiers, or private runtime logs.

## Profile changes

A proposed mapping change should state the affected work type, failure cost, representative workload, evidence date, expected quality/latency/cost tradeoff, runtime compatibility, and a rollback choice. Prefer changing one route at a time. Update the relevant Profile document, both READMEs, the benchmark note when applicable, and `CHANGELOG.md`.

## Scope

Lightweight documentation, Profile packages, examples, prompts, and dated evidence are in scope. Installers, automatic configuration mutation, benchmark scraping pipelines, and mandatory validation frameworks are intentionally out of scope unless a later ADR changes the project boundary.
