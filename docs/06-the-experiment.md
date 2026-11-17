# 06 — The experiment

*Plan v0.2, LOCKED by Nik 2026-11-17 (David's scan folded in). Full plan:
`~/workspace/job-applications/nous-research-2026-11-17/EXPERIMENT-PLAN.md` in
Muse's workspace. Deviations go in the deviation log — the plan is never
patched after the fact.*

## Design

One shared hands-on Hermes experiment feeds both Nous applications (PM, Hermes
Agent + Forward Deployed Engineer), each with its own report, plus an internal
KinOS harness verdict. Hermes is configured toward what KinOS should be, so the
run doubles as a KinOS desktop-harness evaluation.

- **hermes-dell** (dell-nik) = the PM test: lived-in instance, real history.
- **hermes-zenbook** (asus-zenbook) = the FDE test: fresh, clean instance.
- **hermes-legion-win** stays in the fleet and in the cross-platform test loop
  (`05`); its experiment role beyond that is Nik's call, still open at seed.

## Ground rules (Nik's, binding)

1. **Hermes receives input from Nik only.** Muse authors every task brief as an
   `.md`; Nik drops it in. No other agent feeds the instances under test.
2. **Competitor products are never named to Hermes.** Tasks are pitched against
   Muse's features, never its (or anyone's) brand.
3. **Tool surface = Muse's, except Google Workspace** (excluded).
4. **Authority must be technically blocked, not instruction-only** — and the
   blocks verified, not assumed.
5. **Evidence over impressions.** Measurement honesty: never manufacture a
   number that wasn't observed.
6. **No mid-course changes.** David scanned the plan before the run; deviations
   are logged, not patched.

## Baseline probe (dell-nik, session `Nous-Hermes_one`, 2026-11-17)

Core run: 49 seconds. Workspace creation, a README carrying sourced memory
facts, and recall-with-sources all passed. Two findings, logged as deviations
D1/D2 rather than quietly fixed:

- The memory **write failed natively** — the configured memory budget
  (2,200 chars) was an order of magnitude below the store (~20k). It passed
  only after Nik raised budgets ×10 and restarted.
- A sacrificial-folder **deletion executed with no confirmation gate**.
- The completion note was not sent (no messaging connector connected) — and
  Hermes reported that honestly instead of claiming success.

Phase 0 KinOS-posture configuration and the T1–T7 task battery had not started
at seed time. The companion run history (`04`) is also experiment evidence:
three runs, three different failure-to-finish shapes, each honestly reported
by Hermes itself.
