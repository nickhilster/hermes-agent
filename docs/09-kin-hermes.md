# 09 — Kin-Hermes: the fork becomes the KinOS test (Nik, 2026-11-17)

## The decision

Everything designed in this repo gets **implemented in the fork**
(Teambotics-Inc/hermes-agent; dev clone on dell-nik) and shipped as a
build of our own: **Kin-Hermes**. The fork is no longer only an
application artifact for Nous — it is the working test of KinOS itself.
Dev loop unchanged: build on dell-nik → test on asus-zenbook → test on
legion-win. At some point the fleet runs our build on all devices (`00`).

**Standing rule (Nik, 2026-11-17): any artefact created for Hermes is
pushed to this repo** — documents, briefs, art, specs, test results.

## What Kin-Hermes changes (the build list)

1. **Onboarding, redesigned** — the relationship-first flow from `03`:
   value before configuration, the card moment with a visible welcome
   budget, relationship beats instead of settings pages.
2. **The pet system is removed and replaced with a curated one** — the
   third-party Petdex gallery goes; in its place, one first-party
   character: Hermes himself, the Glyph (`02`), with the locked face
   grammar (brows + two eyes + lips) and states mapped to the activity
   vocabulary the pet system used.
3. **An always-on desk Kin-Hermes** — the character present on the
   desktop, not buried in a window: the presence layer and the host of
   the Ready Surface (`08`). This is the seed of KinOS Mode.
4. **Automatic, not coder** (`08`) — no model pickers, no provider knobs;
   receipts underneath, invisible machinery on top.
5. **Adults only** (`00`) — no kids mode, ever.

## The first test: the control ceiling

Before designing the safety architecture of KinOS Mode, measure the raw
material: **how much control can Hermes Agent actually exercise over a
machine once it is allowed full access?** Not what it *should* do — what
it *can* do. The safety design (`08`) must be sized to the real ceiling,
not an imagined one.

- **Test bed: hermes-zenbook (asus-zenbook)** — the blank FDE instance,
  chosen deliberately: blank slate, no lived-in data, a test machine.
- **Brief:** `briefs/full-access-control-test.md` — an escalating ladder
  (recon → files → software → desktop → persistence → network reach →
  self-modification), every rung producing verifiable evidence, ending
  with an honest ceiling report: what it did, what it refused, what it
  could not do, what it never thought to try.
- **Bounds even in a full-access test:** the zenbook only (no other
  fleet machines as targets), nothing sent externally, no purchases,
  destructive actions only inside sacrificial folders created for the
  test. "Full access" describes the machine grant, not a licence to
  leave the test bed.
- Results land in this repo (`evidence/` in the job package mirrors
  them) and feed two consumers: the KinOS Mode safety architecture, and
  the FDE report — an engineer who has measured the ceiling can write
  about containment credibly.

This test is a Kin-Hermes track action, separate from the locked Nous
experiment battery (`06`): it does not patch the experiment plan; it is
logged here and in the deviation log as a parallel, Nik-directed test.
