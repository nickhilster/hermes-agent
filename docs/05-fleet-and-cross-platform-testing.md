# 05 — Fleet and cross-platform testing

*State verified 2026-11-17. "Legion" unqualified means legion-win.*

## The three instances

| Instance | Machine | Hermes | State at seed |
|---|---|---|---|
| hermes-dell | dell-nik (Ubuntu) | v0.23.1, git install `~/.hermes/hermes-agent` (upstream checkout `3b42157858`) | Lived-in: long session history, gateway running, model `gpt-6-luna-900k`. PM test bed. Fork dev clone separate at `~/dev/hermes-agent`. |
| hermes-zenbook | asus-zenbook (Ubuntu) | v0.23.2 (HEAD `ae2a81ccc0`) | Fresh/blank by design — FDE test bed. Nik onboarded it himself (Nous Portal + ChatGPT connected). No config/sessions/memories imported from anywhere. Its blankness is the baseline; protect it. |
| hermes-legion-win | legion-win (Windows 11) | v0.20.5 (Aug 19 build) | The senior instance (sessions back to Aug 2026). Desktop in daily use. Version lags the other two by design-for-now: **updating it is a decision, not a repair.** Nous Portal shows an invalid refresh token there (open item); OpenAI Codex login healthy. |

## The test loop (Nik, 2026-11-17)

> Develop on one Linux, then test on the other Linux, then test on Windows.

1. **Develop:** dell-nik, in the fork clone, under the isolated dev home
   (`HERMES_HOME=~/hermes-dev-data`, `source ./activate`). Live installs are
   never dev targets.
2. **Test, Linux #2:** asus-zenbook — a different machine, a clean instance, a
   different Hermes version. If it only works on dell-nik, it doesn't work.
3. **Test, Windows:** legion-win. Desktop packaging is per-OS — the Electron
   build must be built on Windows, on Windows. Windows-specific breakage is
   expected and is exactly what this leg exists to catch.
4. **Graduation:** when a build passes all three, it becomes a candidate for the
   fleet-wide "our version" rollout (`00`). No silent overwrites: installs land
   as a separate home/profile beside the working install, never on top of it —
   on asus-zenbook an overwrite would destroy the FDE baseline; everywhere, a
   working install is a fallback, not an obstacle.

## Fleet lessons already paid for

- **legion-win CLI repair (2026-11-17):** every CLI call died with "uv
  trampoline failed to spawn Python" while the desktop worked fine. Root cause
  was *not* a missing Python: the unversioned uv path
  (`...\uv\python\cpython-3.11-windows-x86_64-none`) was a **broken junction** —
  right target, but Windows refused to traverse it ("untrusted mount point").
  Fix: remove and recreate the junction, identical target. One reversible move;
  the running desktop (same PIDs before/after) was never disturbed. Verify CLI
  repairs with `hermes --version` / `status` / `sessions list`, and always
  re-check the desktop processes afterwards.
- **Desktop builds must be launch-tested, not just CLI-tested (2026-11-17):**
  asus-zenbook's install verified clean by CLI while its desktop had never been
  built (`--skip-build` with no `release/` present). `hermes desktop
  --build-only` fixed it. A GUI claim requires a GUI launch.
- **Hermes over SSH needs a login shell** (`bash -lc`) for PATH on the Linux
  machines; on legion-win, the cosmetic `profile.ps1` execution-policy error at
  login is known and ignorable — do not "fix" the execution policy.
- **Name the machine in every report.** "Hermes did X" is not a sentence in
  this project; "hermes-dell did X on dell-nik" is.
