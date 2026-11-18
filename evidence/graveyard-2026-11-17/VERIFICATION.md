# Verification — Graveyard shift 2026-11-17 (checked 2026-11-18 morning, America/Toronto)

Verifier: Muse (morning pack run). Method: reports collected over SSH from
dell-nik and asus-zenbook, read in full, compared line-by-line to their briefs
in `briefs/graveyard-*.md`, plus independent live checks noted below.
Claims labelling is assessed per report.

## Runner outcomes (from runner.log on each machine)

- dell-nik: RUNNER-START 2026-11-17T23:30:19-05:00, RUNNER-DONE 23:37:27-05:00.
  kh6 rc=0, kh7 rc=0, kh12 rc=0.
- asus-zenbook: RUNNER-START 2026-11-17T23:30:23-05:00 — waited for Hermes
  Round 1 to go quiet, proceeded 23:40:23. kh8 rc=0, kh1 rc=0 (process exit
  only — see KH-1 below: rc=0 does NOT mean a deliverable was produced).
  RUNNER-DONE 23:43:46-05:00.

## KH-6 — Wayland GUI-driving gap (hermes-dell, dell-nik)

- Deliverable: PRESENT — `dell-nik/KH-6-wayland-report.md` (15,365 bytes).
- Brief compliance: RESEARCH ONLY respected — report states no packages,
  configuration or persistent services were changed; only read-only probes.
- Coverage: all brief-required options covered — XDG ScreenCast/RemoteDesktop
  portals, AT-SPI2, ydotool/wtype/dotool, XWayland/X11 fallback, GNOME Shell
  extensions, dogtail/pyatspi — each with capability, permission posture,
  stock-Ubuntu survival, security posture and a verdict
  (viable / conditional / dead end).
- Claims labelling: GOOD. Observed local state (portal versions ScreenCast 5 /
  RemoteDesktop 2, GNOME Shell 50.1, package versions, `/dev/uinput` ACL for
  user `nikhil`, running user-local `ydotoold`) is separated from not-tested
  items (no end-to-end portal session was requested, no input was generated,
  pyatspi/dogtail not installed so not exercised).
- Caveat carried in the report itself: the Zenbook control-ceiling evidence
  path `evidence/full-access-zenbook-2026-11-17/` was not found in the
  checkout hermes-dell searched, so the AccessDenied finding is treated as
  supplied context, not independently revalidated. That checkout is the fork
  clone on dell-nik, not this project repo — the evidence does exist in this
  repo. Input-location failure, not a research failure.
- Headline: Portals (ScreenCast + RemoteDesktop) + AT-SPI2 are the viable
  least-privilege path; Xorg whole-desktop is a dead end; the existing
  uinput ACL + ydotoold on dell-nik is non-stock local state to audit
  separately, not a deployment recipe.

## KH-7 — Tailscale peer visibility (hermes-dell, dell-nik)

- Deliverable: PRESENT — `dell-nik/KH-7-tailscale-report.md` (12,933 bytes).
- Brief compliance: RESEARCH ONLY respected — no Tailscale settings, ACLs or
  device configuration changed (stated in report; no contrary evidence).
- Coverage: (1) demonstrated with read-only commands as user `nikhil` —
  full peer table and `status --json` field inventory (node keys, MagicDNS
  names, IPs, OS, online/last-seen, byte counters, peer API URLs); socket
  `/var/snap/tailscale/common/socket/tailscaled.sock` is world rw, which is
  why the unprivileged read works on this host. (2) Controls covered: ACLs/
  grants, device posture, tailnet lock, LocalAPI surface, per-user vs system.
  (3) Mitigations ranked for a home deployment where Nik's father does nothing.
- Claims labelling: GOOD — host observations, documentation claims and the
  one failed probe (`tailscale ping` timed out; `debug netmap` denied) are
  distinguished. Note: the tested account is in the sudo group (invocations
  did not use sudo) — the report discloses this itself.
- Headline: visibility ≠ connectivity, but the full fleet map is readable by
  any local process on dell-nik today. Ranked fix #1: isolate KinOS from the
  host tailscaled at the OS boundary (dedicated UID / namespace, no LocalAPI
  socket). ACLs alone do NOT hide the peer map.

## KH-12-prep — Phase 0 config diff, DRAFT ONLY (hermes-dell, dell-nik)

- Deliverable: PRESENT — `dell-nik/KH-12-phase0-diff.md` (11,968 bytes),
  24 items, each with current value + file/key, proposal, rationale, risk.
- Brief compliance — NOTHING APPLIED, independently verified by Muse:
  `~/.hermes/config.yaml` on dell-nik has mtime 2026-11-17 12:24:14 EST and
  size 129,460 bytes — hours BEFORE the 23:34–23:37 run. The run did not
  change hermes-dell's config. No gateway/service restart is claimed or found.
- Major limitation, disclosed by the report itself: hermes-dell could NOT
  read docs/00-charter.md, docs/06-the-experiment.md or docs/08-kinos-mode.md
  — the checkout it searched is the fork clone (Teambotics-Inc/hermes-agent),
  which has no `docs/`, and GitHub returned 404 for the project repo path it
  tried. Result: every item is KEEP / NO CHANGE pending the actual locked
  v0.2 text. As a diff it is therefore provisional and decision-incomplete;
  as a read-only inventory of current values (memory 220000 / 137500,
  approvals not explicitly set, muse-harness `denyUnmatched`, broad CLI
  toolset, stt.enabled true / local model base, gateway.allow_all_users
  false) it is usable.
- Claims labelling: GOOD — "not observed" section lists effective approval
  mode, effective STT provider, live messaging status and the x10 memory
  statement (recorded as supplied context, not verified) as unestablished.
- Decision for Nik: re-run KH-12-prep with the project-repo docs actually
  reachable, or accept the KEEP-all draft as the Phase 0 baseline record.
  Do NOT apply anything from this draft as-is — it contains no proposed
  changes to apply.

## KH-8 — Whisper/STT close-out (hermes-zenbook, asus-zenbook)

- Deliverable: PRESENT — `asus-zenbook/KH-8-whisper-report.md` (5,165 bytes).
- Brief compliance: user-level bounds respected — in fact NO install and NO
  config change were made at all, because the re-verification found the
  brief's dated starting state was already superseded.
- Finding: faster-whisper 1.2.1 + ctranslate2 4.8.3 already import in the
  actual Hermes runtime Python (identified from the launcher path, as the
  brief required); STT config via Hermes' own loader: enabled true, provider
  auto-detected local, model base, language en.
- End-to-end proof WITHOUT a microphone: TESTED — Hermes' own
  `transcription_tools.transcribe_audio()` on a LibriSpeech dev-clean FLAC
  returned the correct transcript (wording matches the corpus reference,
  case/punctuation normalised), 1.138 s in-call, ~515 MB peak RSS, base model
  blob ~138.5 MiB. espeak/espeak-ng/festival/flite absent; `spd-say -w`
  failed — disclosed, then the public-sample route was used as the brief
  allowed.
- Claims labelling: EXEMPLARY — Observed / Tested / Not checked sections.
  Not checked: microphone/live gateway path, other model sizes, multilingual,
  father-hardware suitability (Zenbook i7-1165G7 numbers are this machine only).
- Headline: Zenbook STT is DONE — no install was needed. Remaining KH-8 scope
  (dell-nik runtime proof, legion-win wiring, spoken test per machine) was
  not part of this run and stays open.

## KH-1 — Glyph state sheet spec (hermes-zenbook, asus-zenbook)

- Deliverable: **MISSING — the run produced NO spec file.**
  `~/graveyard-2026-11-17/KH-1-state-sheet-spec.md` does not exist on
  asus-zenbook. Only the session log exists (`asus-zenbook/kh1-state-sheet.log`).
- What happened (from the log, 27 s, 12 messages): hermes-zenbook searched
  its scratch checkout
  (`~/.hermes/cache/scratch/repo-review-2026/repos/hermes-agent`), found the
  persona doc, but could NOT find `evidence/zenbook-estate-review-2026-11-17.md`
  or `assets/hermes-character-concept-v4.webp` in that checkout, could not
  confirm the Boardy theme schema, and declined to invent exact geometry —
  "No spec file was written."
- Assessment: the refusal to fabricate is correct behaviour; the failure is
  an input-location failure — the brief pointed at "the project repo" and
  the instance looked in a stale/partial scratch clone instead of a location
  containing the evidence + assets. The runner still recorded rc=0, so the
  failure is invisible in runner.log alone — it is only visible in the
  per-run log. Stated plainly here and in the morning pack.
- Decision for Nik: re-brief KH-1 with explicit file locations (or a fresh
  clone of nickhilster/hermes-agent in a known path) and re-run; no other
  ticket is blocked by this tonight.

## Hermes Round 1 journey report (asus-zenbook)

- Checked: no journey report file exists in `~/graveyard-2026-11-17/`, in
  `~` (maxdepth search for journey/round/Code2Motion-named report files),
  or among .md files modified on asus-zenbook after 2026-11-17 18:00 outside
  the Hermes install/cache. The underlying repo-review scratch work exists
  (`~/.hermes/cache/scratch/repo-review-2026/` — Code2Motion tree, commit
  history, README batches, dated 2026-11-17 afternoon), but NO finished
  journey report (Code2Motion deep-dive + two-version chronological report)
  and no final summary file was found. The graveyard runner waited for
  Round 1 to go quiet (proceeded 23:40 after "quiet or unknown"), which is
  consistent with the session having ended without delivering that report
  into a file. Status: NOT DELIVERED as a file — if it exists, it lives
  only inside the Hermes session history, not on disk.

## Ubuntu-experience sync (asus-zenbook)

- Note present: `asus-zenbook/ubuntu-sync-note.md` — full text filed.
- Verified against the task chart: fresh capture + compare ran against
  primary 510fa7ce; NOTHING was applied. Holds match Nik's prior decisions
  and the handoff rules (zoom, systemd-zram-generator held 2026-11-12;
  Craft apps unsigned-APT rule — Zenbook already runs them as Flatpaks;
  Dell monitor selector in panel-lengths is hardware-bound; eternal-sunshine
  package needs provenance review).
- Staleness finding confirmed as stated in the note: primary
  `config/primary.json` is dated 2026-11-03 and lacks
  `com.nousresearch.hermes.desktop` in favorite-apps, which the Zenbook has —
  syncing would have removed Hermes from the Zenbook dock. Held for Nik
  (see MORNING-PACK.md).

## Fork tracker (KF) mirror

- Checked dell-nik `~/dev/hermes-agent/.tracker/`: state.json still
  `nextId: 1`, issues/cycles/milestones/initiatives contain only `.gitkeep`,
  board.html timestamp 2026-11-17 20:15 — identical in substance to the
  existing mirror in this repo (`fork-tracker/`, board.html 19,118 bytes,
  same timestamps). The KF board did NOT change overnight, so the mirror
  was NOT refreshed — there was nothing to refresh.
