# KH-1 run report

Run date: 2026-11-21 (local tool environment date not independently queried). Scope: draft documents only; no fork, live install, or code changes.

## Inputs read

- **Observed:** `/home/nik/dev/kin-hermes/docs/02-persona-the-hermes-character.md` read. Locked direction and v4 face/state criteria recorded.
- **Observed:** `/home/nik/dev/kin-hermes/assets/hermes-character-concept-v4.webp` opened; image metadata 2512×816 RGB. Visual inspection found five figures: alert, running, review/raised wing, failed/drooped, waiting/content.
- **Observed:** `/home/nik/dev/kin-hermes/evidence/zenbook-estate-review-2026-11-17.md` read. It reports BoardyAnimated uses audio amplitude + state for mouth/gaze/posture, controls clamped, reduced-motion honored. This is a prior review report, not independently re-run here.
- **Observed:** `/home/nik/dev/kin-hermes/reference/boardy-theme-example.json` read. Its manifest includes schemaVersion, viewBox, layout, eyeTracking, states, idleAnimations, timings, among other fields.

## Produced

- `/home/nik/kin-hermes-work/kh1/KH-1-state-sheet-spec.md` — **inferred/proposed:** canonical numeric geometry, seven configurations, transitions, voice mapping, theme-style sketch, acceptance checks. References do not supply exact canonical coordinates, full seven-state geometry, timing constants, or Boardy amplitude constants; those values are explicitly proposed rather than observed.
- `/home/nik/kin-hermes-work/kh1/KH-1-REPORT.md` — this report.

## Verification and limits

- **Tested:** all four specified paths existed and were readable using a local Python file read; image decoded successfully with Pillow.
- **Tested:** outputs were written to the requested paths.
- **Not checked:** the mapping sketch was not validated against a formal consumer schema or fork implementation.
- **Not checked:** SVG was not generated/rendered; 16px/64px/full-screen acceptance checks are prescribed, not executed.
- **Not checked:** motion and audio behavior were not implemented or run.
- **Not checked:** no git status/diff was run; scope was limited to deliverable files, and no fork/live-install/code path was written by this run.
- **Inferred:** geometry and all numeric motion/voice settings are a concrete draft target derived from the locked brief and visual reference, not source-authored coordinates or Boardy rig constants.
