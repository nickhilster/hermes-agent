# MIRROR — the KF board (fork tracker)

This directory is a **read-only mirror** of the `.tracker/` directory in
the fork (Teambotics-Inc/hermes-agent, dev clone on dell-nik) — the **KF
board**. This repo (nickhilster/hermes-agent) is the **control room** for
the fork, so its board is mirrored here where the whole fleet can see it.

Rules:
- **Source of truth is the fork.** Tickets are created and edited in the
  fork's `.tracker/` (on dell-nik), never in this mirror.
- Muse refreshes this mirror whenever the fork board changes or
  whenever Muse is asked; a stale mirror is a display bug, not data.
- The project board (KH) lives in this repo's own `.tracker/` and is
  native here — KH is project/control-room work, KF is fork code work.
