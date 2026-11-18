# Zenbook ubuntu-experience sync — graveyard pass, 2026-11-17 night

Procedure followed: docs/zenbook-handoff.md sequence steps 1–6.
Repo: ~/dev/ubuntu-experience @ 510fa7ce81430acff3e6b65f2d4d2f7c029521b1 (master)
Primary profile: config/primary.json (Dell Inspiron, captured 2026-11-03)
Fresh Zenbook capture: .local/profiles/20261118T043417430118Z.json
Full compare: .local/compare-2026-11-17-graveyard.txt

## Applied: NOTHING — deliberately. Every candidate failed a gate:

REVIEW INSTALL (14) — all held:
- 11 *Craft apps as APT: Zenbook already runs them as Flatpaks
  (ai.storyteller.*). Handoff forbids auto-adding the publisher's
  unsigned APT preview. Packaging difference, not missing software.
  Nik decision.
- zoom, systemd-zram-generator: HELD by Nik's own 2026-11-12
  reconciliation decisions. Not re-litigated overnight.
- eternal-sunshine-captured: local package, provenance review first.

REVIEW SETTING (4) — none applied:
- org.gnome.shell favorite-apps: primary (Nov 3) LACKS
  com.nousresearch.hermes.desktop, which the Zenbook HAS pinned.
  Syncing to primary would REMOVE Hermes from the Zenbook dock.
  The primary snapshot predates the Hermes era — it is stale, not
  the replica that is wrong. Correct move: refresh primary from
  dell-nik (daytime, reviewed), then re-compare.
- dash-to-panel panel-lengths: primary value carries the DELL
  monitor selector (CMN-0x00000000). Handoff: never copy it. Held.
- touchpad-gesture-customization x2 keys: extension on Zenbook
  reports version None vs primary v25 (same source URL, ACTIVE).
  Keys unavailable locally; version discrepancy is the real item.
  Held for a compatibility look.

ADAPT ON DEVICE (7): touchpad speed, sleep timeout, dash-to-panel
anchors/positions/sizes, vitals fan/temperature — hardware-specific
by design, not sync targets. No action.
LOCAL ONLY; PRESERVE: flatpak, genoffice, the Flatpak Craft suite,
Edge, android-studio, tailscale snap, dev libs — untouched, as the
rules require.

## Bottom line
The Zenbook is substantively in sync with the primary. The one real
finding runs the other way: config/primary.json (2026-11-03) is
stale — it predates Hermes on the fleet. Next sync should start
with a reviewed primary refresh from dell-nik.
