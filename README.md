# hermes-agent (Nik's / TeamBotics build)

**Hermes, Bro!** — the development home for our own build of [Hermes Agent](https://github.com/NousResearch/hermes-agent) by Nous Research.

This repository starts as **documents** — the charter, strategy, design specs, build
records and working rules for the project — because three Hermes instances (on
dell-nik, asus-zenbook and legion-win) can all read this repo, and this is where they
get their shared picture of what we are building and why.

## Why this exists

We are building on Hermes **irrespective of any job application**. Hermes is open
source, we have real contributions to make, and at some point **we will run our own
build** — on every machine in the fleet — whether or not upstream ever takes our
changes. The applications to Nous Research (Product Manager, Hermes Agent and
Forward Deployed Engineer) grow out of this work; they are not the reason for it.

The direction in one line: **features commoditize; the moat is the Human+Hermes
relationship.** Code is cheap and getting cheaper. The business is in the
relationship — and right now Hermes has a logo, a personality *system*, and borrowed
pet sprites, but no *person*. Step one is the persona.

## Read in this order

1. `docs/00-charter.md` — what this project is, and the run-our-own-build commitment
2. `docs/01-strategy-application-and-competition.md` — the competitive landscape,
   the insider posture of the Nous applications, and the fork-as-application decision
3. `docs/02-persona-the-hermes-character.md` — the mascot audit (what Hermes already
   has, verified in its own codebase) and the Hermes character spec: the Boardy
   character architecture, remixed
4. `docs/03-onboarding-and-relationship.md` — onboarding as the first act of
   relationship design; the credit-card challenge; welcome credits as a
   relationship-acquisition budget; Onboarding Milestone 1
5. `docs/04-builds-so-far.md` — what's already built: sidebar Projects +
   External-sessions, the companion placement decision, the fork desktop build recipe
6. `docs/05-fleet-and-cross-platform-testing.md` — the three Hermes instances, their
   roles, and the develop-on-one-Linux / test-on-the-other-Linux / test-on-Windows loop
7. `docs/06-the-experiment.md` — the locked Hermes experiment (Plan v0.2): ground
   rules, baseline results, deviations
8. `docs/07-working-rules-and-provenance.md` — how we work: receipts over
   reassurance, corrections beside errors, the Cost-Control Gate

`AGENTS.md` in this repo root is the briefing for any Hermes instance (or any other
agent) picking this project up cold.

## Status at seed (2026-11-17)

- Sidebar stack built and packaged on dell-nik (fork clone `~/dev/hermes-agent`,
  branch `feat/sidebar-external-sessions`, 2 commits, clean tree, desktop build
  verified by install stamp) — **not pushed anywhere yet**
- Companion Milestone 1: placement decided and recorded in an (empty) first commit on
  dell-nik's companion worktree; build parked pending the persona/onboarding direction
- Onboarding Milestone 1: scoped, not started
- Hermes character: concept stage (this seed)
- Fleet: hermes-dell v0.23.1 · hermes-zenbook v0.23.2 · hermes-legion-win v0.20.5
  (CLI repaired 2026-11-17; update is a decision, not yet taken)
