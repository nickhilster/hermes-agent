# Graveyard brief KH-8 — Whisper/STT close-out (hermes-zenbook, asus-zenbook)

Overnight run, directed by Nik through Muse (2026-11-17). Nik
already authorized the user-level Whisper install on this machine in
the "Hermes Round 1" session; this run executes and verifies it.
Bounds: user-level changes only (your own env, uv/pip user installs,
Hermes config for STT). No sudo, no system packages, no pkexec. If
the only path needs elevation, stop and report that as the blocker.

Known starting state (dated, re-verify): config has stt.enabled:
true with local model "base"; faster-whisper was NOT found in the
searched paths on 2026-11-17.

Task: (1) Re-verify the current STT state: config values, whether
faster-whisper imports in the actual Hermes runtime python (find
the runtime the launcher uses; test the import there, not in a
random python). (2) If missing, install user-level into the correct
environment and re-test the import. (3) Prove transcription
end-to-end WITHOUT a microphone: obtain or synthesize a short
speech audio file (e.g., espeak/espeak-ng if present, or a small
public sample) and transcribe it through the same code path Hermes
uses; quote the transcript you got. If synthesis is unavailable,
say exactly where the proof stopped. (4) Note model size, disk
used, and load time — the father demographic's hardware is the
reference, so cost matters.

Deliverable: ~/graveyard-2026-11-17/KH-8-whisper-report.md on this
machine, separating observed / tested / not-checked, + a 5-line
summary in your final message.
