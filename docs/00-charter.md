# 00 — Charter

*Set by Nik, 2026-11-17.*

## What this is

Serious building on Hermes Agent, the open-source agent from Nous Research —
undertaken **irrespective of the outcome of any job application**. We use Hermes
across a three-machine fleet every day; we have found real gaps in it; we have
contributions to give. This repo is where that work is coordinated and recorded.

## The commitments

1. **We will run our own build.** At some point the fleet runs the version we are
   developing — on dell-nik, asus-zenbook and legion-win — as our daily driver.
   Upstream acceptance of our changes is welcome and will be pursued where it makes
   sense, but it is **not a gate**: if upstream never takes a change we believe in,
   our build carries it anyway.
2. **Cross-platform by construction.** Develop on one Linux (dell-nik), test on the
   other Linux (asus-zenbook), test on Windows (legion-win). A feature that only
   works on the dev machine is not done. (No Mac in the fleet: macOS is stated
   plainly as untested in anything we publish or submit.)
3. **Documents first.** This repo seeds as documentation so that every agent in the
   mesh — all three Hermes instances included — works from the same picture. Code
   homes are listed in `AGENTS.md`; this repo is the intent layer above them.
4. **The direction is relationship, not features.** See `01` and `02`. Everything we
   build is in service of one claim: features will be available across all
   platforms; **the moat is the Human+Hermes relationship**, and loyalty is what is
   at stake.

## Why Hermes (and not only the bigger platforms)

Nik chose to try Hermes because its values match KinOS's: open, local-first,
ownable, the human in control — what KinOS wants to offer at an operating-system
level, Hermes offers at the agent level. That alignment is the reason this project
exists at all, and it is also the heart of the Nous applications (`01`).

## Provenance

Every claim in these documents was checked against a live source at seed time
(machine state read over SSH, the Hermes codebase read in the fork clone, Nous's
public pages fetched). Where a fact ages — versions, session counts, build
status — the docs say when it was true. See `07` for the working rules.
