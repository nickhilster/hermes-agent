---
id: KH-7
title: "Control-ceiling follow-up: Tailscale peer visibility exposure"
status: Todo
statusType: unstarted
priority: medium
labels: [security]
assignee: null
createdBy: null
project: Kin-Hermes
milestone: null
initiative: null
cycle: null
parent: null
createdAt: "2026-11-17T23:33:50.184Z"
updatedAt: "2026-11-18T12:10:52.343Z"
startedAt: null
completedAt: null
canceledAt: null
linearUrl: null
gitBranchName: null
---

## Description

tailscale status exposes the whole fleet's names/addresses to any user-level process (ceiling test finding 1). Document the exposure precisely; propose mitigations (ACLs, peer segmentation) for Nik's decision. No changes without his word.

## Comments

### CLI — 2026-11-18T04:30:37.326Z
Graveyard shift 2026-11-17: research run queued on hermes-dell (dell-nik) after KH-6, brief briefs/graveyard-kh7-tailscale.md. Report due at ~/graveyard-2026-11-17/KH-7-tailscale-report.md; research only, no Tailscale changes authorized.

### CLI — 2026-11-18T12:10:52.343Z
Morning pack 2026-11-18: DELIVERED. Report filed at evidence/graveyard-2026-11-17/dell-nik/KH-7-tailscale-report.md (verified vs brief in VERIFICATION.md). Headline: any local process on dell-nik can read the full fleet peer map via tailscale status --json (world-rw tailscaled socket); visibility is not connectivity and ACLs alone do not hide the map. Ranked KinOS fix #1: OS-boundary isolation from the host daemon. Research only, no Tailscale changes. Held for Nik: KinOS isolation posture decision at design time.
