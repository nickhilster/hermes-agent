# 03 — Onboarding and the relationship

*Thesis developed by Nik with hermes-zenbook ("Hermes Round 1" session,
asus-zenbook, 2026-11-17), and adopted as the fork's second workstream.*

## The critique

Nik enjoyed Hermes's first-run onboarding — and, as a product matter, it leaves
a lot for the user to figure out. The current flow is a sequence of setup beats
(name, theme, layout, connectors, plugins, a tour, then a first build). It is a
**configuration wizard**. But Hermes is not merely software: its value accumulates
in continuity, memory, trust, permissions and shared history — which makes
onboarding **the first act of relationship design**, and it should be designed
as one.

## The business challenge: the card, not the amount

From a business perspective, the first challenge is **getting the user to part
with their credit card details at all — not the amount**. Take a leaf from the
Meta playbook for Muse: a card is required to sign up, free credits come with
it, and the user gets *used to* the product before money is ever asked for.

Hermes already has the seed of this: the `nous/welcome` model is a **one-time
free onboarding trial, once per OS user**. Reframed correctly, that welcome
allowance is not a cheap trial quota — it is a **relationship-acquisition
budget**, and it should be spent like one: visibly, generously, and never as a
surprise paywall in the middle of a forming relationship.

## Onboarding Milestone 1 (scoped, not yet started)

To be built in the fork, testable in the fork desktop build (`04`):

1. **Value before configuration.** Resequence first-run so the user reaches a
   real first win before the theme/layout/connectors/plugins beats. Setup
   arrives when it is relevant, not as a gate in front of value.
2. **The card moment, redesigned.** Card as an identity/anti-abuse step paired
   with welcome credits, framed honestly ("this is how the free budget works"),
   with the remaining welcome budget **visible** — a relationship budget on the
   table, spent down in the open.
3. **Relationship beats.** During onboarding, Hermes says what it will remember,
   where that lives, and asks — Nik's Capture → Preview → Human choice pattern —
   instead of memory being a buried setting discovered later. The Hermes
   character (`02`) hosts these beats: a person asks; a wizard collects.

## Why this workstream (and why it outranks the companion app)

An official Hermes mobile beta exists (waitlist live at
hermes-agent.nousresearch.com/mobile, verified 2026-11-17; Nik is on it), which
puts a native companion app on Nous's own roadmap. Onboarding/relationship has
no such collision: it is the PM role in product form, it survives any Nous
roadmap, and it transfers wholesale to KinOS if Nous says no. The companion
work is capped at its Milestone 1 placement decision (`04`) until the beta's
scope is known.
