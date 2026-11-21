# KH-12 Phase 0 PREP ONLY — run report

Inspection date: 2026-11-21. Target label dell-nik / hermes-dell is supplied by the brief; host identity was not independently verified.

## Inputs read

- `/home/nikhil/dev/kin-hermes/docs/00-charter.md` — readable; read all 59 lines. **Observed:** includes adults-only hard rule at §§45–59.
- `/home/nikhil/dev/kin-hermes/docs/06-the-experiment.md` — readable; read all 50 lines. **Observed:** locked Plan v0.2; Phase 0 had not started at seed time; rules include Nik-only input, Google Workspace excluded, technical authority blocks verified, evidence over impressions, no mid-course changes; baseline memory write failed at 2,200 chars and deletion ran without confirmation.
- `/home/nikhil/dev/kin-hermes/docs/08-kinos-mode.md` — readable; read all 165 lines. **Observed:** includes safety/approval principles, local-first posture, voice/dictation tracking, and open runtime verification for dell-nik STT.
- `/home/nikhil/dev/kin-hermes/evidence/graveyard-2026-11-17/dell-nik/KH-12-phase0-diff.md` — readable; read all 70 lines. **Observed:** earlier draft was KEEP-all and explicitly caveated missing docs; this run supersedes its conclusions where new docs now provide evidence.
- `/home/nikhil/.hermes/config.yaml` — readable; read lines 1–1799 and 1800–2566 (all 2,566 lines). **Observed:** relevant values and quoted line references are in the v2 diff.

## Deliverables

- `/home/nikhil/kin-hermes-work/kh12/KH-12-phase0-diff-v2.md`
- `/home/nikhil/kin-hermes-work/kh12/KH-12-REPORT.md`

**Tested:** Both deliverables were written successfully by the file-writing tool; the tool confirmed on-disk verification for each. Markdown lint was not run (no configured linter reported). No config parser or runtime checks were run because this was PREP ONLY.

## Activity and boundaries

**Observed:** No config file was edited. No setting was changed. No gateway or service was restarted. No live gateway, approval prompt, memory write, STT transcription, tool denial, messaging delivery, or external connector was exercised. No credentials/secrets were inspected.

**Observed:** All five paths were readable, so the missing-input stop condition did not trigger.

**Inferred:** Documents specify safety posture and experiment constraints, but do not give exact values for several live config keys (notably global approval configuration, exact tool allowlist, STT provider, adults-only admission control, and gateway/A2A participation). Therefore the diff recommends no config changes and records decisions Nik owes rather than guessing.

**Not checked:** Host identity; active profile/process identity; effective runtime config and environment overrides; live gateway access lists; provider/runtime approval behavior; actual memory file sizes/contents; STT runtime import and end-to-end dictation; MCP/A2A connectivity; config parse validity; any post-application behavior.

## Receipt

**Outcome:** Read the requested sources and created a decision-ready, source-line-cited KEEP/decision-needed draft plus this report.

**Verification:** Both artifact writes returned `verified: true`.

**Not done:** No config edits, service restarts, gateway actions, or runtime tests.

**Open items:** Nik must resolve the decisions listed in the diff before any later application; this draft itself authorizes no changes.
