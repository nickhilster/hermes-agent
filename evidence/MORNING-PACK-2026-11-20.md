# Morning Pack — Kin-Hermes overnight queue, 2026-11-20 night

Compiled 2026-11-20 (America/Toronto) by Muse, from Nik's queue
given in the Movie Time chat (~20:26 EST). All claims below were
verified by Muse against the artifacts on the machines, not taken
from the instances' summaries alone.

## The standing fix, applied first

The Nov 17 KH-1 / KH-12 failures shared one root cause: no canonical,
fleet-reachable checkout of this repo existed, so briefs pointed at
"the project repo" and the instances searched scratch/fork clones.
Fixed tonight, permanently:

- Canonical checkout is now **`~/dev/kin-hermes` on every machine** —
  cloned fresh on dell-nik and asus-zenbook tonight, both at the same
  commit, every brief input verified present at its absolute path
  before dispatch. The convention is written into this repo's
  AGENTS.md.
- `reference/boardy-theme-example.json` (a real boardy-at-the-desk
  theme.json) was added to this repo so every machine has the format
  reference locally.
- Both runs used **persistent named sessions**, per Nik's standing
  rule: `kin-hermes-zenbook` (session local-ba856c4b…) on asus-zenbook,
  `kin-hermes-dell` (session local-a345fe77…) on dell-nik. Future
  briefs resume these instead of re-buying context.

## Step 0 — live-state recheck (discrepancies vs the Nov 18 pack)

- KH board: all 13 tickets still Todo; nothing was closed Nov 19–20.
- **KH-9 is decided and executed, though the board doesn't say so:**
  on 2026-11-18 Nik directed the fork branches pushed to
  Teambotics-Inc/hermes-agent (sidebar ×2, companion, trackerbuddy-
  adopt) and the fork installed side-by-side on dell-nik. Board
  comment added tonight.
- **KH-11's text is stale:** the companion Phase B continuation
  (2026-11-18) completed the API portion — router mounted, pairing
  token, sessions endpoint (commits 6444a9c499, 24929adab8). Still
  outstanding: the mobile UI and automated tests. Board comment added.
- **KH-13:** relay deployed to xps-plex and two-device tested on
  2026-11-18; only the father's laptop setup remains (needs the real
  call). Board comment added.

## KH-1 — Glyph state sheet (hermes-zenbook, asus-zenbook): DELIVERED

- `evidence/kh1-rerun-2026-11-20/` — spec (11,492 bytes), run report,
  run log. Session `kin-hermes-zenbook`, 1m 43s.
- The spec covers all six brief sections: canonical SVG geometry
  (viewBox 0 0 100 120, head/staff/wings primitives with coordinates),
  all 7 states tabled in the locked face grammar (brows / eyes / lips /
  staff tilt / wing pose), motion keyframes with numeric durations and
  easing (dart/glide, no bob), amplitude→mouth mapping, a theme.json-
  style mapping sketch, and acceptance checks for 16px / 64px /
  full-screen.
- Honest boundary, stated in the spec itself: the references lock the
  style and state cues but contain no canonical coordinates or timing
  constants — every number is an explicit *proposed* implementation
  value, labelled inferred in the run report. Nik's review is the
  approval gate for those numbers.
- One stumble, self-corrected: the first two launch attempts failed on
  runner mechanics (PATH; then `--max-turns` is rejected on session
  resume). Third attempt ran clean. No instance time was wasted on
  either failure — both died before the brief was sent.

## KH-12 — Phase 0 prep re-run (hermes-dell, dell-nik): DELIVERED, nothing applied

- `evidence/kh12-rerun-2026-11-20/` — v2 diff (21,158 bytes), run
  report, run log. Session `kin-hermes-dell`.
- **Verified by Muse:** `~/.hermes/config.yaml` on dell-nik is
  byte-identical before and after the run (sha256 23de9559…, mtime
  2026-11-18 17:13 EST). Nothing applied, nothing restarted.
- The v2 diff is decision-ready: every implicated key with its current
  value quoted from the live config (all 2,566 lines read), KEEP or
  proposal, rationale tied to named sections of docs 00/06/08, risk,
  and evidence gain/loss.
- Its central, honest finding: **the docs specify posture, not exact
  values** — so the diff recommends no speculative edits and records
  the decisions Nik owes. The sharpest three:
  1. **No active `security.approval` block exists** in the live config
     (only commented template lines) — the experiment's "authority
     technically blocked" ground rule is not currently configured.
     Nik must choose the approval transport/mode and which operations
     gate; effective policy then needs a live block test.
  2. **STT conflict:** `stt` is in `agent.disabled_toolsets` while
     `stt.enabled: true` — whether Phase 0 needs the Hermes STT tool
     itself, vs platform voice transcription only, is a decision owed.
  3. **Tool surface not enumerated:** `platform_toolsets.cli` is broad
     (a2a, browser, code_execution, computer_use, …); the "Muse's
     surface minus Google Workspace" set needs Nik's exact list.
- First launch attempt failed: "Gateway did not answer
  session.resume" (the gateway service itself was up; the fork desktop
  was also running against the same data dir). One retry succeeded.
  Recorded here, not smoothed over.

## Held for Nik — not started tonight, per the queue

- **KH-6:** end-to-end portal consent/session test (needs approval);
  ruling on dell-nik's `/dev/uinput` ACL + running `ydotoold`.
- **KH-7:** KinOS tailnet-isolation posture — deferred to KinOS
  networking design.
- **Hermes Round 1 journey report:** write it out from session
  history, or drop it — Nik's call.
- **Ubuntu primary-profile refresh:** daytime, reviewed — the Nov 3
  primary still predates Hermes on the fleet.
- **KH-13:** father's laptop setup — needs the real call (relay is
  live and tested).

## Decisions Nik owes (new, from tonight)

1. KH-1: approve / adjust the proposed geometry and timing numbers.
2. KH-12: the approval-gate configuration (item 1 above), the STT
   tool question (item 2), and the exact Phase 0 tool surface (item 3)
   — after which a Phase 0 *application* run can be briefed.
3. The held items above, at his pace.
