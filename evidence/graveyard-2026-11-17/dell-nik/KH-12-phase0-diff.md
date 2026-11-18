# KH-12-prep — Phase 0 config diff (DRAFT ONLY)

Date: 2026-11-17 (local machine time: America/Toronto)
Target: hermes-dell / dell-nik (identity supplied in work order; host identity not independently verified)
Live config inspected read-only: `/home/nikhil/.hermes/config.yaml` (`HERMES_HOME=/home/nikhil/.hermes`). No config or service changes made.

## Source and evidence caveat

The work order names `nickhilster/hermes-agent` and requests `docs/00-charter.md`, `docs/06-the-experiment.md`, and `docs/08-kinos-mode.md`. The locally available checkout is `/home/nikhil/dev/hermes-agent`, whose configured remotes point to `Teambotics-Inc/hermes-agent` and `NousResearch/hermes-agent`; the supplied repository's sole public `main` was checked at `5dd4b6bd87bd85546693f565691622f360086396`. That tree does not contain `docs/` or the three named files, and the GitHub contents endpoint for `nickhilster/hermes-agent/docs` returned 404. Therefore the locked v0.2 experiment text and charter lines were NOT available to quote. No posture principles below are attributed to those absent documents. This is a deliberately provisional draft: rationale uses only the brief's stated purpose / already-applied facts and observable config comments; obtain the actual locked documents before treating proposals as approved or final.

The work-order statement that memory budgets were raised x10 on 2026-11-17 is recorded as supplied context, not independently verified. The live file presently shows `memory.memory_char_limit: 220000` and `memory.user_char_limit: 137500`; the former agrees with the native cap mentioned in context, so it is not evidence of an un-applied change. Don't infer an older value or apply another x10 multiplier.

## Proposed items

Each item gives the effective configured value observed (or says when none was explicit), a draft proposal, rationale/source, and application risk. “Proposal” is not authorization.

### Memory budgets and posture

1. `~/.hermes/config.yaml` → `memory.memory_char_limit`: current `220000`; proposed `KEEP 220000`. Rationale: brief says budgets were already raised x10 to address the 2,200-character native cap; no locked charter text was obtainable to justify further adjustment. Risk if changed: could alter continuity and prompt size, confounding the baseline; no further change recommended.
2. `~/.hermes/config.yaml` → `memory.user_char_limit`: current `137500`; proposed `KEEP 137500` pending the actual plan text. Rationale: observed live value; no authorized target supplied. Risk if changed: user-profile context volume/content may shift experiment behavior.
3. `~/.hermes/config.yaml` → `memory.memory_enabled`: current `true`; proposed `KEEP true`. Rationale: preserve existing memory-bearing instance for the experiment. Risk if disabled/cleared: loss of lived-in continuity and changed behavior; this is experiment evidence, not disposable setup.
4. `~/.hermes/config.yaml` → `memory.user_profile_enabled`: current `false`; proposed `KEEP false` pending charter confirmation. Rationale: preserve current posture; no evidence that enabling is required. Risk if enabled: newly injected profile context changes responses and the instance's character.
5. `~/.hermes/config.yaml` → `memory.nudge_interval`: current `10`; proposed `KEEP 10`. Rationale: no plan line available to support changing it. Risk: altered memory-writing prompts and behavior.
6. Not observable from `config.yaml`: actual memory file contents, native provider hard caps, and memory backend/provider effective runtime. Proposed: record/inspect separately during authorized baseline, without editing or pruning. Rationale: the prompt calls for posture but contents themselves are historical evidence. Risk: any cleanup, reformatting, migration, or replacement could destroy evidence. Do not perform as part of this draft.

### Approval and confirmation behavior

7. `~/.hermes/config.yaml` → `approvals.*`: no explicit top-level `approvals` block was found; effective approval mode/runtime behavior is therefore not established by this file alone. Proposed: NO CHANGE until inspect the actual locked plan and confirm the intended approval mode, plus a supported read-only runtime/config query. Rationale: absent plan text gives no safe target. Risk: switching to a more permissive mode could authorize consequential tool activity; switching stricter could interrupt the task battery and change latency/interaction. Do not infer `off`, `smart`, or `manual` from absence.
8. `~/.hermes/config.yaml` → `plugins.enabled`, `plugins.entries.muse-harness.settings.approval_mode`: current plugin list includes `muse-harness`; its setting is `denyUnmatched`. Proposed: KEEP. Rationale: observable guardrail, unrelated to permission to alter it. Risk: relaxing it may widen plugin action surface and alter the mediation pathway; tightening it may block task-battery operations.
9. `~/.hermes/config.yaml` → `security.approval.*`: no active block observed (only commented example); effective defaults/plugin transports not confirmed. Proposed: NO CHANGE pending documentation and runtime evidence. Risk: unsupported edits could silently alter tool-confirmation semantics or fail to parse.

### Tool surface

10. `~/.hermes/config.yaml` → `platform_toolsets.cli`: current explicit list includes broad access (`a2a`, `browser`, `computer_use`, `cronjob`, `delegation`, `file`, `image_gen`, `kanban`, `memory`, `session_search`, `terminal`, `web`, `x_search`, and others) plus `muse_harness`. Proposed: NO CHANGE until the missing experiment document specifies a task-battery tool policy. Rationale: preserve baseline capability surface. Risk of narrowing: tasks may become impossible; risk of broadening: introduces new capabilities and confounds the experiment.
11. `~/.hermes/config.yaml` → `platform_toolsets.telegram` / `discord` (and other listed platform presets): currently `[hermes-<platform>, muse_harness]`. Proposed: KEEP. Rationale: this is a broad existing messaging tool surface; no plan line supports replacing it. Risk of change: changes how the instance can act from established channels and materially alters its character.
12. `~/.hermes/config.yaml` → `agent.disabled_toolsets`: current list disables `bot_room`, `catalog`, `context_engine`, `desktop_ui`, `discord`, `discord_admin`, `feishu_doc`, `feishu_drive`, `onboarding`, `project`, `stt`. Proposed: KEEP pending plan. Risk of enabling/disabling: changes discoverable capabilities; enabling integrations may expose additional actions/data.
13. `~/.hermes/config.yaml` → `mcp_servers`: several locally configured servers and enabled flags are present (e.g. Notion and Vercel enabled; many others disabled). Proposed: KEEP all as-is; do not connect, authorize, or alter MCP servers in Phase 0 without a precise charter requirement. Risk: added or removed external services change tool reach, data flows, and historical behavior.
14. `~/.hermes/config.yaml` → `agent.max_turns`: current `90`; proposed `KEEP 90` until the experiment specifies a limit. Risk: reducing it could truncate tasks; increasing it may affect cost and autonomy.

### STT / voice

15. `~/.hermes/config.yaml` → `stt.enabled`: current `true`; proposed `KEEP true` pending protocol. `stt.provider` is not explicitly set in the `stt` block; a later `provider: local` at line 1841 is nested under `code_execution`, not STT. The file has `stt.local.model: base`; do not mistake this for proof of effective provider. Proposed: observe the effective provider and package readiness read-only before T1–T7; do not install packages or restart in this run. Rationale: the experiment's required input modality is unknown because its text is unavailable. Risk: selecting local/cloud changes accuracy, latency, privacy, and whether speech is usable; package installation/restart is forbidden in this draft.
16. `~/.hermes/config.yaml` → `voice.voice_chat_mode`: current `chained`; proposed `KEEP chained` pending plan. Risk: changing voice interaction changes the lived-in input/output character and could affect task comparability.

### Gateway and messaging posture

17. `~/.hermes/config.yaml` → `gateway.allow_all_users`: current `false`; proposed `KEEP false`. Rationale: preserve current access control; no plan text supports relaxing it. Risk: allowing all users broadens access to this agent and its tools/history.
18. `~/.hermes/config.yaml` → `gateway.bot_loop_guard.enabled`: current `true`; proposed `KEEP true`. Rationale: safety guardrail. Risk: disabling permits bot-loop amplification; changing thresholds can alter message behavior.
19. `~/.hermes/config.yaml` → `gateway.multiplex_profiles`: current `true`; `gateway.profile_routes`: current `[]`; proposed `KEEP`. Rationale: observed routing posture, no plan instruction. Risk: routing changes can redirect messages across profile boundaries or change which historical agent responds.
20. `~/.hermes/config.yaml` → `streaming.enabled`: current `false`; proposed `KEEP false` pending experiment specification. Risk: enabling changes message timing/partial-output exposure and user experience; disabling it if already on would likewise change behavior.
21. `~/.hermes/config.yaml` → `display.busy_input_mode`: current `interrupt`; proposed `KEEP interrupt`. `display.cleanup_progress` is `false`; proposed `KEEP false`. Rationale: preserve established interrupt and progress-breadcrumb behavior. Risk: changing may alter recovery and erase visible traces of long-running work.
22. `~/.hermes/config.yaml` → messaging platform identities, allowlists, and live service wiring: only partial config is visible; credentials are not inspected, and no live gateway queries were performed. Proposed: do not alter. Risk: access loss, exposure, or destruction of operational evidence. Never include secrets/tokens in the eventual experiment report.

### Instance identity / lived-in character — explicit hold

23. Preserve `/home/nikhil/.hermes` memory, sessions/state database, logs, skills, plugin state, MCP auth, and messaging identities. These contain the instance's accumulated history. Proposed: no clearing, reinitializing, profile replacement, migration, or fresh-profile substitution. Rationale: work order explicitly says lived-in character is evidence. Risk if applied: irreversible loss of continuity and invalidation of the experiment's baseline.
24. Do not change model/provider, personality, SOUL/instruction text, or profile identity without the locked plan's explicit direction. Current model/provider are `gpt-6-luna-900k` / `openai-codex` in `model.default` / `model.provider`; the active personality and runtime overrides were not fully verified. Any such change is high-risk to the instance's voice and comparability.

## Not observed / required before finalizing the Phase 0 diff

- Exact charter and experiment requirements: BLOCKED; the three named docs are absent from the available repo tree and GitHub returned 404 for `nickhilster/hermes-agent/docs`.
- Host identity and which gateway process/profile is currently serving `hermes-dell`: supplied labels only; not independently verified.
- Effective approval mode, per-tool confirmation policy, current authorization/session overrides: not established from this config file.
- Effective STT provider/dependency readiness and actual voice path: not established.
- Live messaging adapter status, allowlists, and runtime overrides: not queried; secrets intentionally not read.
- Native cap and prior/pre-change memory limits: only the work-order statement; not independently evidenced.

## Draft decision

No config change is recommended from the evidence available. Preserve all observed values and historical state until the actual locked v0.2 documents are made available and their exact lines can be mapped to supported keys. This document is a proposal record only; it is not an applied diff. No gateway/service restart was issued.
