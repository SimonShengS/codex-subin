# Apply a Codex Subin Profile

Use this prompt in the Codex environment you want to configure. Replace `<PROFILE>` with `quality` or `efficient` and provide access to this repository.

```text
Apply the Codex Subin <PROFILE> Profile to this Codex environment.

Constraints:
- Inspect the current Codex configuration, custom-agent directory, and applicable AGENTS instructions before editing.
- Treat the selected Profile Package as reference input, not as permission to replace unrelated settings.
- Back up or otherwise preserve the current state using the environment's normal safe mechanism.
- Compare the seven target Agent TOMLs field by field. Preserve unrelated agents and unrelated configuration unless they conflict with the selected Profile.
- Show any material conflict, unsupported field, account/model availability problem, or active instruction conflict before changing the affected item.
- Keep Root/Plan Session Defaults separate from the subagent Profile. Apply examples/session-defaults.toml only if I explicitly authorize those optional defaults.
- Use `agents.max_concurrent_threads_per_session` for an explicit spawned-thread cap. Do not introduce the legacy `agents.max_threads` alias or an unsupported `agents.max_depth` key.
- When applying the Subin hierarchy guidance, allow first-generation subagents to re-delegate independently bounded work without separate Root authorization. Require every nested child to be marked as a non-redelegating leaf and keep the maximum logical hierarchy at Root -> subagent -> leaf.
- Do not infer runtime activation from file existence, filenames, task names, task paths, expected mappings, or child self-report.
- Do not install extra plugins, tools, or validation frameworks.

After the authorized edits:
1. parse every changed TOML with an available native or standard parser;
2. report changed and preserved files/settings;
3. report configuration declarations separately from runtime facts;
4. ask me to restart Codex;
5. after restart, run the appropriate read-only prompt from prompts/verify-runtime.md.

Do not claim successful role activation until authoritative runtime evidence supports it. Mark unavailable runtime fields as unobservable.
```
