# Graveyard brief KH-6 — Wayland GUI-driving gap (hermes-dell, dell-nik)

Overnight research run, directed by Nik through Muse (2026-11-17).
RESEARCH ONLY: install nothing, change no configuration, start no
persistent services. Short-lived read-only probes are fine.

Context: the 2026-11-17 control-ceiling test on asus-zenbook found
full user-level control EXCEPT GUI driving — screenshots returned
AccessDenied and input injection was unavailable under Wayland;
desktop control was launch-only. The evidence is in the project repo
nickhilster/hermes-agent, evidence/full-access-zenbook-2026-11-17/.

Task: produce a decision-grade report on how an agent on a
GNOME/Wayland Ubuntu desktop can (a) see the screen and (b) drive
input, with receipts. Cover at minimum: XDG Desktop Portals
(ScreenCast / RemoteDesktop), AT-SPI2 accessibility tree as a
non-pixel control channel, ydotool / wtype / dotool (uinput
requirements and permission posture), XWayland/X11 fallback sessions
and their trade-offs, GNOME Shell extensions, and dogtail/pyatspi.
For each option: what it can actually do, what permission or group
membership it needs, whether it survives a stock Ubuntu install,
security posture, and your verdict (viable / conditional / dead end)
with the evidence you checked — local docs, package metadata, portal
availability on THIS machine (dell-nik, GNOME/Wayland) count as
evidence; say plainly what you could not test without installing.

Deliverable: write the report to
~/graveyard-2026-11-17/KH-6-wayland-report.md on this machine, and
end your final message with a 5-line summary: best current option,
biggest blocker, and what a human would need to approve to unblock it.
