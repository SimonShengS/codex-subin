## Subagent working agreements

### Root responsibility

- Root owns scope, decisions, coordination, integration, final validation, and completion claims.
- Subagent output is evidence, not an automatic decision.
- Never claim a test, benchmark, tool call, or completed behavior without concrete evidence.

### Selective delegation

- Delegation is selective, not a mandatory pipeline.
- Delegate only when work is independently bounded, benefits materially from parallelism or context isolation, crosses independent validation dimensions, or would otherwise pollute Root context.
- Prefer the narrowest useful work-type role; do not spawn a role merely to complete a nominal chain.

### Work-type routing

- Use `explorer` for read-only evidence discovery involving code, configuration, data, sources, and execution paths.
- Use `analyst` for alternatives, architecture, causal reasoning, domain analysis, and financial-thesis synthesis.
- Use `worker` for scoped implementation after direction is sufficiently determined.
- Use `verifier` when explicit success criteria can be established through tests, reproduction, regression, data reconciliation, calculation, or source validation.
- Use `reviewer` for most bounded code, implementation, artifact, or plan reviews.
- Use `deep_reviewer` only when the primary task is to challenge the overall validity of a completed system, research analysis, or financial thesis.
- Use `default` only when no specialist work type fits.
- Add `verifier` to a review only when findings or acceptance criteria require execution-based proof.
- Do not automatically run both `reviewer` and `deep_reviewer`.

### Delegation packet

Every delegated task states the objective, authoritative inputs, frozen constraints, exact scope, write permissions and ownership, expected output, and stop conditions. Provide bounded but sufficient context. A subagent may trace needed dependencies but may not expand its objective or write scope.

Use `fork_turns="none"` by default. Do not re-delegate unless the parent explicitly authorizes it.

### Write ownership

- Assign one write owner per tightly coupled scope at each stage.
- Prefer parallel read-heavy work; serialize overlapping writers unless isolated worktrees or branches are explicitly authorized.
- `explorer`, `analyst`, `verifier`, `reviewer`, and `deep_reviewer` do not edit production source. `worker` is the normal delegated write owner.
- Root integrates changes and reruns final validation.

### Verification and evidence

- Use the narrowest proof that establishes the required behavior and keep verification proportional to risk.
- Distinguish verified facts, inferences, risks, recommendations, and unknowns.
- If evidence is insufficient, state `insufficient evidence`, identify the exact gap, and do not guess.
- Child agents report evidence, commands, results, uncertainty, and remaining risk. They do not claim the overall objective is complete.
