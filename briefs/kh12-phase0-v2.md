# Brief KH-12 (v2) — Phase 0 KinOS-posture config diff, PREP ONLY
## For: hermes-dell, on dell-nik. Directed by Nik through Muse, 2026-11-20.

HARD BOUND: this is a drafting run. Apply NOTHING. Do not edit any
config file, do not restart the gateway or any service, do not change
any setting. Your only writes are the two deliverables below. (Your
2026-11-17 prep run respected this bound and its KEEP-all draft was
honest; the reason for this re-run is that the project docs were not
reachable to you then. They are now — see Inputs.)

## Inputs — verified present at these exact absolute paths on this machine

The canonical project checkout on this machine is
`/home/nikhil/dev/kin-hermes` (a clone of the project repo
nickhilster/hermes-agent). Read these files at these paths — do not
search other checkouts (in particular, the fork clone at
~/dev/hermes-agent is a different repo and has no docs/):

1. `/home/nikhil/dev/kin-hermes/docs/00-charter.md` — the project
   charter, including the adults-only hard rule.
2. `/home/nikhil/dev/kin-hermes/docs/06-the-experiment.md` — the
   locked experiment plan (Plan v0.2); Phase 0 is its KinOS-posture
   setup stage.
3. `/home/nikhil/dev/kin-hermes/docs/08-kinos-mode.md` — KinOS Mode:
   the posture Phase 0 configures toward.
4. `/home/nikhil/dev/kin-hermes/evidence/graveyard-2026-11-17/dell-nik/KH-12-phase0-diff.md`
   — your own 2026-11-17 draft: the current-values inventory and the
   KEEP-all assessment this re-run supersedes.
5. Your live config, read-only: `/home/nikhil/.hermes/config.yaml`.

If any input is missing or unreadable at its path, STOP: write the
failure report (below) naming exactly what is missing. Do not
improvise from memory of the earlier draft.

## Task

Produce a usable proposed Phase 0 diff — a decision-ready document,
not an inventory:

For every config key the charter / experiment / KinOS-mode docs bear
on (memory budgets and posture, approval policy, STT, gateway access,
tool authority, anything else the docs implicate):

- the key's exact name and its CURRENT value, observed by you from
  the live config in this run (quote the source line);
- the PROPOSED value, or KEEP with a reason;
- the rationale, tied to a named section of docs 00 / 06 / 08;
- the risk or behaviour change if applied, stated plainly;
- what evidence the experiment gains or loses either way.

Where the docs do not determine a value, say so and name the decision
Nik owes — do not fill the gap with a default.

Close with: (a) the exact list of changes you would make if Nik
approved, in application order; (b) the verification steps to run
after application (including how to prove the gateway and memory
behave as intended); (c) the rollback for each change.

## Deliverables — both required, on this machine

- `/home/nikhil/kin-hermes-work/kh12/KH-12-phase0-diff-v2.md` — the diff.
- `/home/nikhil/kin-hermes-work/kh12/KH-12-REPORT.md` — the report:
  what you read (with paths), confirmation that nothing was applied
  and nothing restarted, every claim labelled observed / tested /
  inferred / not checked. The report is required on failure too.
  A run that produces no report is a failed run, whatever its exit
  code says.

End your final message with a 5-line summary.
