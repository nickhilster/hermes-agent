# Graveyard brief KH-12-prep — Phase 0 config diff, DRAFT ONLY (hermes-dell, dell-nik)

Overnight drafting run, directed by Nik through Muse (2026-11-17).
DRAFT ONLY: apply NO configuration changes. Do not restart the
gateway or any service. Read-only inspection of your own live config
is expected; changing it is forbidden in this run.

Context: the Nous experiment plan (v0.2, locked) calls for a
"Phase 0 KinOS-posture" configuration of this instance before the
T1–T7 task battery. The posture principles live in the project repo
nickhilster/hermes-agent — read docs/00-charter.md, docs/06-the-
experiment.md and docs/08-kinos-mode.md (clone read-only if needed).
Known already-applied facts: Nik raised the memory budgets x10 on
2026-11-17 after the baseline probe hit the 2,200-char native cap.

Task: produce a proposed Phase 0 diff for THIS instance
(hermes-dell on dell-nik): for each relevant setting — memory
budgets and posture, approval/confirmation behaviour, tool surface,
STT, gateway/messaging posture, anything the charter implies —
give: current value (observed from the live config, with the file
and key), proposed value, rationale tied to a charter/doc line, and
risk if applied. Where you cannot observe a current value, say so;
do not guess. Flag any proposed change that would alter the
lived-in character of this instance, since that history is evidence
for the experiment and must not be destroyed casually.

Deliverable: ~/graveyard-2026-11-17/KH-12-phase0-diff.md on this
machine + a 5-line summary in your final message stating clearly
that nothing was applied.
