# Read-only Runtime Probe

Use **Full Probe** after initial installation, a Codex upgrade, or a broad Profile change. Use **Focused Probe** after changing only one role mapping.

```text
Perform a read-only Codex Subin runtime acceptance probe. Do not modify configuration or project files.

Probe mode: <FULL or FOCUSED>
Expected Profile: <quality, efficient, or a supplied custom matrix>
Focused roles, if any: <role list>

Evidence rules:
- Distinguish (1) configuration declarations, (2) authoritative runtime metadata, and (3) fields the current interface cannot observe.
- Do not infer runtime roles from TOML existence, filenames, task_name, task path, expected mappings, or a child agent's self-report.
- First inspect whether the current spawn interface exposes an actual custom role/agent_type selector.
- If it does not, run only a generic/default read-only probe and record that named routing is unobservable through the current interface. Do not simulate roles with task names.
- If it does, spawn the requested roles with fork_turns="none". Run only bounded read-only work. Use no more concurrency than the runtime permits.
- For each child, inspect host-side structured evidence where exposed: requested agent_type, session_meta.agent_role, turn_context model and effort, multi_agent_version, and injected developer instructions.
- A null or missing role field is not automatically success or failure. Mark exactly what it leaves unobservable.
- Child prose is not authoritative runtime evidence.

Hierarchy check for a Full Probe:
- Give one first-generation role two independently bounded read-only evidence dimensions and require it to decide and execute the smallest useful child delegation without asking Root for separate authorization.
- Limit it to one child. The spawning agent must tell the child it is a leaf that must not re-delegate and must return one consolidated result.
- Inspect authoritative session metadata for parent/child relationship and depth when exposed. Confirm that the child has no descendant and no spawn call.
- Do not saturate the configured concurrency cap by default. To check that a raised cap replaced a lower runtime ceiling, use the smallest concurrent leaf set that crosses the old ceiling and report only the proven lower bound.

For every probed role, report:
- expected model and effort;
- configuration-declared model and effort;
- requested agent_type;
- authoritative runtime role/agent_type;
- authoritative runtime model and effort;
- multi_agent_version, if exposed;
- whether the corresponding custom TOML's instructions are observably injected;
- parent/depth and leaf status for the nested probe, when applicable;
- unobservable fields;
- result: PASS, FAIL, CONFIGURATION ONLY, or UNOBSERVABLE.

Also report the Root's runtime model/effort only if authoritative metadata exposes them. Do not infer Root runtime values from config.toml.

Output one table:
| Item | Expected | Configuration declaration | Runtime actual | Evidence source | Result |

Finish with direct answers:
1. Did default route to its expected model/effort?
2. Did each named role actually activate its corresponding TOML?
3. Is multi-agent v2 observable and active?
4. Did one first-generation agent re-delegate without separate Root authorization, and did its child remain a leaf?
5. What concurrency level was actually observed, as distinct from the configured ceiling?
6. Which claims remain unobservable?
7. Were any files modified? The required answer is no.
```
