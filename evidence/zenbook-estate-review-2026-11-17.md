# hermes-zenbook estate review — 2026-11-17

Source: hermes-zenbook's "Hermes Round 1" study run (asus-zenbook),
reported to Nik and relayed to Muse 2026-11-17 21:23 EST. Four repos
read in Nik's order, each repo's own instructions/status docs first;
all four review clones left clean, nothing changed or pushed.
Verification limits are stated per repo in the original report and are
part of the evidence (e.g., LTB Buddy full suite not run — Deno absent,
Node 22.22.1 vs required 22.22.2+; Boardy Electron files not run).

## LTB Buddy — nickhilster/ltb-buddy · 5328486
- Tenant-rights intake + case prep; clinic mode = structure the story
  for staff review, not autonomous legal decisions.
- Good: export/deletion derive identity from a verified bearer token,
  not a body user ID; deletion validates evidence paths and reports
  partial failure honestly.
- **Trust gap (repo-authored data-lifecycle audit, 2026-09-20):**
  guest users lack self-serve deletion; export ≠ deletion coverage;
  profile/analytics records outside the deletion handler; admin chat
  viewer has elevated raw-conversation access with no access log;
  retention setting unenforced; masking inconsistent across AI calls.
  Audit predates the checked commit — claims are repo-authored, not a
  production compliance assessment.
- check-id-drift passed across frontend/backend/SQL/registry IDs.

## Hangar — nickhilster/hangar · 6745897
- Portfolio governance dashboard; cleanup made legible without making
  the dashboard a destructive actor. audit_repos.py vs registry;
  server-side redaction of sensitive entries (name + lifecycle only
  unless SHOW_SENSITIVE=1).
- Freshness: registry updated 2026-11-13; stored audit 2026-10-11 —
  stale against its own 8-day threshold; `/` prerenders static, so the
  stale warning doesn't refresh between builds.
- **Boundary: no app-level auth found in the dashboard code** —
  deployment-level control unverified. Never expose publicly with
  SHOW_SENSITIVE=1 without an external boundary.
- npm test 67/67; build OK; npm ci: 24 advisories incl. 1 critical
  (not fixed, not auto-fixed — reported).

## Boardy at the Desk — Teambotics-BackBurner/boardy-at-the-desk · f4d11b8
- Desktop companion: agent hook/plugin → local HTTP server → session
  state machine → pet/dashboard UI. Loopback /state + /permission;
  Hermes plugin falls back to Hermes's native permission flow when
  Boardy is unavailable or gated off.
- Mobile server deliberately read-only (LAN bind, rotating-token WS
  auth, snapshots only, no phone approvals) — **but snapshots carry
  full working dirs, titles, changed files, recent events, last
  output; the connection-info endpoint is unauthenticated; the token
  file writer doesn't set restrictive permissions explicitly.**
- **auto-approve-all is a real permission decision, not a
  notification shortcut** — when on, eligible requests are allowed
  with no bubble (DND/headless/per-agent gates evaluate earlier).
  Cautionary input for Kin-Hermes approval UX.
- Tests: 237/237 focused set; 38/38 mobile preview; 84 permission/SSH;
  4 Electron files couldn't start (binary unavailable).

## BoardyAnimated — nickhilster/BoardyAnimated · cc6b76c
- Six-chapter case study; shipped/demo/historical/roadmap/reflection
  kept distinct; unfinished labeled unfinished.
- **Character rig: audio amplitude + state drive mouth, gaze, posture**
  (controls clamped; reduced-motion honored) — the direct ancestor
  technique for the Glyph's animated lips (`02`, KH-1).
- Doc mismatch: changelog says redesign "not merged" but main is the
  PR #9 merge; verification report dated 2026-11-05 not re-run.
- Vite build OK (44 modules, sparse checkout); no test script; site
  emits noindex by configuration.

## Reviewer's own closing (preserved)
"Hangar and Boardy are especially clear about keeping humans in the
decision loop. LTB Buddy has the most serious trust gap... That is
evidence about the work, not an independent hiring assessment or
validation of the market predictions."
