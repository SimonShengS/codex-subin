# Codex Subin

Codex Subin is a configuration and calibration toolkit for routing Codex subagents by work type. Its profiles are explicit, revisable choices rather than permanent rankings of model intelligence.

## Language

**Work-type Role**:
A bounded category of work defined by its objective, evidence needs, write authority, and expected output.
_Avoid_: Persona, simulated specialist, job-title role

**Role Route**:
The selection of a Work-type Role for a delegated task whose scope and stop conditions are already bounded.
_Avoid_: Character casting, mandatory agent pipeline

**Profile**:
A named mapping from Work-type Roles to model and reasoning-effort choices, optimized for an explicit quality, latency, and cost posture.
_Avoid_: Intelligence tier, permanent model ranking

**Quality Profile**:
The reference Profile that prioritizes outcome quality while retaining balanced settings for high-frequency implementation and verification work.
_Avoid_: Optimal Profile, permanent best configuration

**Efficient Profile**:
A cost-efficiency variant of the Quality Profile that assigns Luna/max to Worker while preserving the other role mappings; it does not promise lower latency.
_Avoid_: Faster Profile, low-intelligence Profile

**Profile Package**:
A self-contained set of seven custom-agent TOML files that can be installed without resolving a base profile or override chain.
_Avoid_: Partial override, implicit inheritance bundle

**AGENTS Fragment**:
A bounded block of shared orchestration guidance designed to be merged into existing instructions without replacing unrelated user or project rules.
_Avoid_: Complete global AGENTS file, silent replacement

**Session Defaults**:
Optional recommendations for a new Root session's model and reasoning effort, kept separate from a Profile so users can change the primary session without remapping delegated roles.
_Avoid_: Subagent Profile, mandatory Root setting

**Benchmark Snapshot**:
A dated observation from a stated evaluation source, used as one input when revising a Profile.
_Avoid_: Timeless score, official ranking

**Runtime Probe**:
A read-only acceptance check that distinguishes configuration declarations from authoritative session metadata and unobservable fields.
_Avoid_: Filename check, task-name check, agent self-report

**Runtime Evidence**:
Host-side structured metadata and injected instructions that show which role, model, and reasoning effort a spawned session actually received.
_Avoid_: Configuration declaration, expected mapping, role self-identification

**Full Probe**:
A Runtime Probe covering every core Work-type Role after initial installation, a Codex upgrade, or a broad Profile change.
_Avoid_: Routine per-task pipeline

**Focused Probe**:
A Runtime Probe limited to the Work-type Role affected by a narrow configuration change.
_Avoid_: Full regression

**Root**:
The primary Codex session that owns scope, decisions, coordination, integration, final validation, and completion claims.
_Avoid_: Manager persona, automatic approver
