# 04 — Builds so far

*All state below verified live on dell-nik, 2026-11-17.*

## Sidebar stack (the fork's first feature work)

- **Where:** dell-nik `~/dev/hermes-agent` — origin `Teambotics-Inc/hermes-agent`,
  upstream `NousResearch/hermes-agent`; branch `feat/sidebar-external-sessions`
- **Commits (local only, not pushed):**
  - `b0278260fc` — feat(desktop): add new-project button to sidebar header
  - `7ad1451293` — feat(desktop): add external-sessions section to the sidebar
  - 17 files, +679/−80; verified in the "Nous - 2" session: 57 files / 466 tests
    passing, ESLint fix included; 2 commits ahead of origin/main
- **Why it matters:** the sidebar work is a gap in the *shipping desktop today* —
  seeing work that happens outside the desktop UI (headless runs, other
  instances' sessions) from inside it. It does not depend on Nous's roadmap.
- **Packaged build (2026-11-17):** `apps/desktop/release/linux-unpacked/Hermes`
  in the fork clone, built under the isolated dev home
  (`HERMES_HOME=~/hermes-dev-data`). Install stamp: commit `7ad1451293`,
  `dirty: false` — the binary provably contains both sidebar commits.
  **Build recipe lesson:** a plain `pnpm --dir apps/desktop run pack` fails on a
  clone whose Electron binary installer never ran ("lazy installs are
  disabled"); first run the repo's own prep —
  `node scripts/build/node-deps.mjs --source <clone> --reuse --workspace ui-tui
  --workspace web --workspace apps/desktop` — then pack. Full log:
  `~/fork-desktop-build.log` on dell-nik.
- The live install (`~/.hermes/hermes-agent`, a separate upstream checkout at
  `3b42157858`) **does not run fork features** and was never touched by the build.

## Companion Milestone 1 (parked at placement)

- **Where:** dell-nik `~/dev/hermes-companion`, branch `feat/companion-webapp`,
  isolated dev home as above. Brief: `~/companion-m1-brief.md` on dell-nik.
- **The idea:** a mobile companion for Hermes — webapp first as the test harness,
  Android packaging later, transport kept out of UI components. M1 = pairing/auth
  + gateway-backed session list over the LAN Webapp listener + minimal
  mobile-first UI + tests.
- **Run history (kept whole — the failures are evidence):**
  - Run 1: burned the ~200 tool-call iteration budget on exploration; zero code.
  - Run 2: stopped cleanly on a *real* conflict — the brief requires a dedicated
    companion pairing token, but the repo's `web/AGENTS.md` mandates one session
    token for every route ("never a second scheme"). Hermes refused to silently
    break a repo rule. That refusal is itself experiment-grade behaviour.
  - 2026-11-17: Nik authorized a narrow exception (Addendum 2 to the brief):
    companion routes only, LAN-only, own pairing token with
    generation/validation/rotation/reset; browser sign-in credentials never
    reach the phone; all other routes keep the dashboard token.
  - Run 3: accepted the exception, completed discovery, recorded the placement
    decision in first commit `ba47d16a25` — companion routes in
    `hermes_cli/web_routers/companion.py`, mounted on the existing Webapp server
    under `/api/companion`, exception rationale in the commit message — then
    **stopped voluntarily after ~1 minute / 30 messages**. The commit is empty
    (0 files); no pairing flow, endpoint, UI or tests were built, and Hermes
    said so plainly in its own summary.
- **Status: PARKED** at the placement decision, superseded as the lead
  workstream by persona (`02`) + onboarding (`03`) after the official mobile
  beta came to light. Three runs ending before building is also a finding about
  long-horizon task completion, recorded for the experiment reports (`06`).

## Zed + Muse Code (supporting tooling, 2026-11-17)

asus-zenbook carries the same editor/agent setup as dell-nik: Zed 1.28.1,
Muse Code 1.4.23, muse-acp 0.21.0, dell-nik's Muse login carried over,
Codex ACP alongside. (Custom ACP agents appear in Zed under Agent Panel → New
Thread → External Agents — not in Settings → AI Providers.)
