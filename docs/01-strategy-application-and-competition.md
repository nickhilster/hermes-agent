# 01 — Strategy: competition, the applications, and the fork

*Set by Nik, 2026-11-17. This is the strategy document for the Nous lane.*

## The honest starting point

**Muse (Meta) is, right now, the product to beat.** Stated plainly, from daily
lived use: what Nik can do through Muse — from his phone, over SSH, across his
whole fleet — and the *ease* of doing it, is the benchmark in the personal-agent
space. Whether others can do the same at all, and whether anyone can do it at that
level of ease, is genuinely unknown. The ease is the product. The persona (Jolly)
is not decoration on top of Muse; the persona **is** the interface, and the
relationship is why you stay.

The first lunches Muse eats will be OpenAI's and Anthropic's, in the personal-agent
space. Nous should assume it is on the same menu.

## The warning

Without a relationship layer, Hermes wins the CLI crowd and becomes **another
Claude Code — an office tool**: respected, used at work, and dropped without a
thought when a better tool ships. Tools get replaced. Relationships get kept.
Features will eventually be available across all platforms; **user loyalty is what
is at stake, and the moat is the Human+Hermes relationship. Code is cheap and
getting cheaper. The business is in the relationship.**

## The applications' posture: insider, not applicant

The two Nous applications — **Product Manager, Hermes Agent** and **Forward
Deployed Engineer** — are written as if Nik is **already on the team**: a
colleague's memo proposing a direction and naming the cost of not moving, not an
outsider's pitch. That posture only works with insider-grade artifacts behind it,
which is what the fork is for:

- **The whole fork is the application artifact.** Sidebar work, the companion
  placement decision, the onboarding redesign, the Hermes character — built first,
  written about second.
- **No pushing back upstream for now.** No PRs to NousResearch; the fork is sent
  in *as* the application, on Nik's timing and terms. (Pushing to our own remotes
  for backup is different and encouraged — the work should never exist in exactly
  one place.)
- Each role gets its own resume, cover letter and microsite, resting on one shared
  hands-on experiment (`06`). Nik works from Canada only, and submits himself.

## What we tell them, in order

1. We know the competing products, we use the best of them daily, and the
   competition is serious — named honestly, with respect, and with receipts.
2. Hermes already has every ingredient of the winning product scattered across
   four systems (`02`) — what it lacks is someone whose whole job is the
   relationship those ingredients add up to.
3. Here is that job, already started: the fork.

## Standing boundaries

- Boardy investigation material is out of scope here entirely (separate project,
  separate rules).
- Public-facing words stay welcoming even when the internal analysis is
  uncompromising.
- Nothing ships under Nik's name without his literal go.

## The honest endgame (Nik, 2026-11-17)

Stated plainly, because this document is internal: **Nous has the two things
this project needs — the infrastructure and the money.** The goal is to be
paid to build the KinOS-grade product full-time instead of funding it from
everything else. They can call it Hermes Agent; the name is theirs and it is a
good name. Nik will share Code2Motion with them — the psychedelic register of
their art is a register he already works in. The point was never the label.
**The point is to get the good product out, with the human still in charge of
it — and to be paid to do exactly that.**

## The question (Nik, 2026-11-17)

Every product decision in this project reduces to one question:

> **Does Hermes Agent mean to be a product for people like Nikhil — or for
> people like Nikhil's father?**

Today, Hermes answers "Nikhil": terminal installs, model switching, config
files, a CLI-crowd UI. That is a real market and a small one. Nik's father is
the KinOS target demographic, and the rule behind him is universal: **if his
father can use it, every other demographic can too** — as long as they have a
phone and a computer. Designing for the father is not dumbing the product
down; it is the curb-cut: the power user loses nothing when the machinery
disappears (he was never attached to the machinery — he was attached to what
it *did*), and everyone else gains the product entirely.

Muse is winning because, whatever its other properties, it answers closer to
"the father" than any agent built for the CLI crowd. Hermes can answer "the
father" *without giving up the power* — the power just goes under the floor,
automatic (`08`), with receipts (`07`). That answer is the PM application in
one line, and it is the fork's acceptance test for every feature: **could
Nik's father use this, unaided, on his phone?**

## Internal only — the India window (Nik, 2026-11-17; NOT for the pitch)

Meta/Muse is aiming at the same demographic — the father. The one current
gap: **Muse is not available in India right now.** Nik is explicit that this
does **not** go in the product pitch. It matters elsewhere — notably for
Instinct, whose bet is WhatsApp (where the father demographic already lives)
rather than the desktop. Hermes started in the desktop game; KinOS *is* the
desktop game; that is why this role and this product matter. Recorded here so
the strategy never mistakes a temporary availability gap for a moat.

## Internal — how Meta actually makes money, and the crack in it (Nik, 2026-11-17)

Meta gives Muse's tokens away because the agent is not the product being
sold. The monetization, as Nik reads it (and as Zuckerberg has described
publicly in shape): **transaction tolls** — commissions on shopping and
commerce flowing through the agent; the metaverse play rebuilt in the
agentic verse, with Meta as the toll booth.

The crack, in Nik's analysis: the toll only exists if the merchant lets it.
Repetitive buying (the Walmart grocery run) is exactly the commerce a
merchant can automate *themselves* — Walmart will ship its own bot and keep
its own customer. And for everything else, people mostly *want* to shop;
browsing is leisure, not friction. A toll booth on a road the road-owners
can rebuild for free is not a business — it is a temporary gap.

The deeper distinction, and the one this project is built on: **whose agent
is it?** Meta's agent, however delightful, ultimately serves the toll — its
loyalty runs to the marketplace. The Hermes/KinOS agent runs on the user's
own server, with the user's data in the user's house (`08`), and its loyalty
has exactly one address. Also worth recording: the way Nik uses Muse —
fleet operations over SSH, a working lead with memory and tools — is *not*
what Meta is developing or monetizing Muse for. The capability exists; the
product intent doesn't. Serious infrastructure-grade personal agency is
unclaimed product territory, and it is the territory Hermes already lives in.
