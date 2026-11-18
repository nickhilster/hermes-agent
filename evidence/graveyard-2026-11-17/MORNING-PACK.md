# Morning Pack — Kin-Hermes Graveyard Shift, 2026-11-17 night

Compiled 2026-11-18 morning (America/Toronto) by Muse.
Chart: Nik approved "go as charted" (2026-11-17). Overnight rule (Nik, 23:33 EST):
anything needing Nik was held for the morning; the rest kept going.
All reports, per-run logs and runner logs are filed in this folder:
`dell-nik/` (from dell-nik) and `asus-zenbook/` (from asus-zenbook).
Full brief-by-brief verification: `VERIFICATION.md` in this folder.

Runs: dell-nik 23:30:19–23:37:27 EST, all rc=0. asus-zenbook 23:30:23–23:43:46 EST
(waited for Hermes Round 1 to go quiet first). No new Hermes runs were started
by this pack, the KH-12 diff was NOT applied, and no fork branches were pushed.

---

## KH-6 — Wayland GUI-driving gap (hermes-dell, dell-nik)

- **Outcome:** Delivered. Research only, nothing installed or changed.
- **Headline:** The viable least-privilege path is XDG Portals —
  ScreenCast (v5 advertised) + RemoteDesktop (v2 advertised) for screen +
  input, with AT-SPI2 as a semantic companion. XWayland/Xorg as a
  whole-desktop solution is a dead end. dell-nik already has a non-stock
  local state worth auditing separately: a per-user ACL on `/dev/uinput`
  and a running user-local `ydotoold`, plus `wtype` installed.
- **Needs Nik's decision:** Whether to approve an end-to-end portal test
  (consent prompt + real capture/input session) — the one thing research
  could not prove without prompting. Also whether the existing uinput ACL /
  ydotoold state on dell-nik is intentional or should be removed.

## KH-7 — Tailscale peer visibility (hermes-dell, dell-nik)

- **Outcome:** Delivered. Research only, no Tailscale changes.
- **Headline:** Any local process on dell-nik can read the full fleet map
  (`tailscale status --json`: names, tailnet IPs, OS, online/last-seen,
  node keys, byte counters) — the tailscaled socket is world-readable/
  writable on this host. Visibility is not connectivity, but ACLs alone
  do not hide the map. Ranked fix #1 for KinOS: isolate the agent from the
  host daemon at the OS boundary (dedicated UID / namespace, no LocalAPI
  socket) — Nik provisions once, the father does nothing.
- **Needs Nik's decision:** Pick the KinOS mitigation posture (OS-boundary
  isolation vs separate scoped tailnet vs allowlisted relay) when KinOS
  networking is designed. No change is proposed for the current fleet tonight.

## KH-12 — Phase 0 config diff, prep only (hermes-dell, dell-nik)

- **Outcome:** Draft delivered; **NOTHING was applied — verified.** Muse
  checked independently: `~/.hermes/config.yaml` on dell-nik is timestamped
  2026-11-17 12:24 EST, hours before the run. No gateway restart.
- **Headline:** The draft is a KEEP-everything inventory, not a usable
  Phase 0 diff — hermes-dell could not read the charter / experiment /
  KinOS-mode docs (it searched the fork clone, which has no `docs/`, and
  got a 404 for the project repo), so it refused to propose changes without
  the locked v0.2 text. Current values are inventoried (memory 220000 /
  137500, muse-harness approval `denyUnmatched`, STT on / local base,
  gateway allow_all_users false).
- **Needs Nik's decision:** Re-run KH-12-prep with the project-repo docs
  actually reachable by hermes-dell, or accept the KEEP-all draft as the
  baseline record. Nothing in this draft should be applied as-is.

## KH-8 — Whisper / STT close-out (hermes-zenbook, asus-zenbook)

- **Outcome:** Delivered and proven. No install was needed and none was made.
- **Headline:** The brief's starting state was already superseded —
  faster-whisper 1.2.1 already imports in the real Hermes runtime on
  asus-zenbook, and Hermes' own transcription path transcribed a real
  LibriSpeech sample correctly end-to-end (1.14 s, ~515 MB peak RSS, base
  model ~139 MiB on disk). Zenbook STT is closed. Observed / Tested /
  Not-checked labelling is exemplary.
- **Needs Nik's decision:** None for the Zenbook. Remaining KH-8 scope was
  not in this run and stays open: dell-nik runtime proof, legion-win
  Hermes-side STT wiring, and a spoken dictation test per machine.

## KH-1 — Glyph state sheet spec (hermes-zenbook, asus-zenbook)

- **Outcome:** **FAILED — no spec file was produced.** Stated plainly:
  `KH-1-state-sheet-spec.md` does not exist on asus-zenbook.
- **What happened:** hermes-zenbook looked in its scratch repo-review
  checkout, could not find the estate-review evidence file or the v4
  concept art there, could not confirm the Boardy theme schema, and
  declined to invent exact geometry. The refusal to fabricate was correct;
  the brief's "project repo" pointer landed the instance in the wrong
  checkout. The runner recorded rc=0, so this is invisible in runner.log —
  it shows only in the per-run log (filed here).
- **Needs Nik's decision:** Re-brief KH-1 with explicit, verified file
  locations for the persona doc, estate review, concept art and a Boardy
  theme example, then re-run. Nothing else tonight depended on it.

## Hermes Round 1 journey report (asus-zenbook)

- **Outcome:** **No journey report file exists.** Muse searched
  asus-zenbook (graveyard folder, home, recent .md files, scratch): the
  repo-review working materials are on disk (Code2Motion tree, commit
  history, README batches), but no finished journey report — no Code2Motion
  deep-dive + two-version chronological report, and no final summary file.
  If Round 1 concluded it, it lives only in session history, not on disk.
- **Needs Nik's decision:** Whether to ask hermes-zenbook to emit the
  journey report to a file from its session, or drop the deliverable.

## Ubuntu-experience sync (asus-zenbook, done by Muse in the night)

- **Outcome:** Fresh capture + compare ran against primary 510fa7ce.
  **NOTHING was applied** — every candidate was held (see Held for Nik).
  The Zenbook is substantively in sync; the real finding runs the other way:
  the primary is stale.
- **Headline:** `config/primary.json` is dated 2026-11-03 and lacks
  `com.nousresearch.hermes.desktop` in favorite-apps, which the Zenbook
  has — syncing to the primary would have removed Hermes from the Zenbook
  dock.
- **Needs Nik's decision:** Refresh the primary from dell-nik (reviewed,
  daytime, Nik's eyes on it) before the next replica sync. See Held for Nik.

## Fork tracker (KF) mirror

- Checked dell-nik `~/dev/hermes-agent/.tracker/`: still empty
  (nextId 1, only .gitkeep files, board.html from 2026-11-17 20:15) —
  the KF board did not change overnight, so the mirror in `fork-tracker/`
  was not refreshed; there was nothing to refresh.

---

## Held for Nik

Everything that needed Nik overnight, held per his 23:33 EST instruction:

1. **Ubuntu-experience primary refresh (decision):** refresh
   `config/primary.json` from dell-nik — reviewed, daytime — before the
   next replica sync. The primary (2026-11-03) predates Hermes on the fleet
   and would strip Hermes from the Zenbook dock if applied.
2. **Ubuntu sync holds (all left unapplied):** zoom and
   systemd-zram-generator (Nik's 2026-11-12 decisions, not re-litigated);
   11 Craft apps as APT (unsigned-APT rule — Zenbook already runs them as
   Flatpaks; packaging difference, Nik's call); eternal-sunshine-captured
   local package (provenance review first); dash-to-panel panel-lengths
   (carries the Dell monitor selector — never copied); touchpad-gesture
   version discrepancy (extension reports version None vs primary v25).
3. **KH-12 (decision):** re-run the Phase 0 prep with the project docs
   reachable, or accept the KEEP-all draft as baseline. The diff itself
   stays unapplied either way until Nik says otherwise.
4. **KH-1 (decision):** re-brief with verified input locations and re-run,
   or re-scope. No spec exists to review.
5. **KH-6 (decisions):** approve an end-to-end portal consent/session test
   to prove the recommended path; and rule on dell-nik's existing
   `/dev/uinput` ACL + running `ydotoold` (intentional or remove).
6. **Hermes Round 1 journey report (decision):** have hermes-zenbook emit
   it to a file from session history, or drop it — no file was delivered.
7. **KH-7 (design decision, not urgent):** KinOS tailnet-isolation posture
   (OS-boundary isolation ranked #1) when KinOS networking is designed.

## What went wrong overnight — plainly

- KH-1 produced nothing: wrong-checkout input failure, hidden by an rc=0
  runner line. The instance's refusal to invent geometry was the right call.
- KH-12's draft is decision-incomplete for the same root cause: Hermes
  instances are searching scratch/fork checkouts that do not contain this
  project repo's docs, evidence or assets. Two of five tickets were blunted
  by input location, not by the instances' work. A standing fix is worth
  Nik's word: one canonical, fleet-reachable checkout path for
  nickhilster/hermes-agent, named in every brief.
- The Hermes Round 1 journey report was not delivered as a file.
- Nothing else failed: KH-6, KH-7 and KH-8 delivered as briefed, all bounds
  were respected, and no config, Tailscale, sync or fork state was changed
  overnight.
