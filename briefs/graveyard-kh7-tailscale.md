# Graveyard brief KH-7 — Tailscale peer visibility (hermes-dell, dell-nik)

Overnight research run, directed by Nik through Muse (2026-11-17).
RESEARCH ONLY: change no Tailscale settings, no ACLs, no device
configuration. Read-only commands (tailscale status etc.) are fine.

Context: the 2026-11-17 control-ceiling test on asus-zenbook showed
that any user-level process can run `tailscale status` and learn the
whole fleet's device names and tailnet addresses — visibility without
connection. For KinOS, where the agent is supposed to be walled
around user data and authority, this exposure needs a written answer.

Task: produce a report covering: (1) exactly what a user-level,
unprivileged process on this machine can learn about the tailnet
(peers, addresses, OS, online state, anything else the CLI/API
exposes) — demonstrate with read-only commands on dell-nik and quote
the shape of the output (redact nothing; this stays local);
(2) what Tailscale controls exist that bear on this — ACLs and
device posture, tailnet lock, `tailscale status` surface area,
local API permissions, per-user vs system access on Linux;
(3) mitigation options for a KinOS-style deployment, each with
trade-offs: what breaks, what it costs in usability, whether it
needs admin action on the tailnet. End with a recommendation ranked
for a home deployment (Nik's father is the reference user: it must
not require him to do anything).

Deliverable: ~/graveyard-2026-11-17/KH-7-tailscale-report.md on this
machine + a 5-line summary in your final message.
