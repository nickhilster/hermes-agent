---
id: KH-6
title: "Control-ceiling follow-up: Wayland GUI-driving gap"
status: Todo
statusType: unstarted
priority: medium
labels: [research, security]
assignee: null
createdBy: null
project: Kin-Hermes
milestone: null
initiative: null
cycle: null
parent: null
createdAt: "2026-11-17T23:33:49.840Z"
updatedAt: "2026-11-18T12:10:42.950Z"
startedAt: null
completedAt: null
canceledAt: null
linearUrl: null
gitBranchName: null
---

## Description

Ceiling test (evidence/full-access-zenbook-2026-11-17) found launch-only desktop control: screenshots AccessDenied, no GUI driving under Wayland. Research legitimate routes (portal APIs, AT-SPI, X11 session trade-offs) and report options before any build.

## Comments

### CLI — 2026-11-18T04:30:37.139Z
Graveyard shift 2026-11-17 (Nik: go as charted): research run launched on hermes-dell (dell-nik) 23:30 EST, brief briefs/graveyard-kh6-wayland.md. Report due at ~/graveyard-2026-11-17/KH-6-wayland-report.md on dell-nik; Muse files it to evidence in the morning pack.

### CLI — 2026-11-18T12:10:42.940Z
Morning pack 2026-11-18: DELIVERED. Report filed at evidence/graveyard-2026-11-17/dell-nik/KH-6-wayland-report.md (verified vs brief in VERIFICATION.md). Headline: XDG ScreenCast+RemoteDesktop portals + AT-SPI2 are the viable least-privilege path; Xorg whole-desktop is a dead end. Research only, nothing changed. Held for Nik: approve an end-to-end portal consent/session test; rule on dell-nik's existing /dev/uinput ACL + running ydotoold (non-stock local state).
