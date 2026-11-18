# 10 — Fleet instructions, personalities, and mutual awareness (Nik, 2026-11-17)

## Status of hermes-zenbook

hermes-zenbook is on a long study run in its "Hermes Round 1" session:
reading the GitHub estate in detail (ltb-buddy, Hangar,
boardy-at-the-desk, BoardyAnimated) — Nik's direction, Nik's session.
It is not to be disturbed mid-study. When it finishes, Nik will ask
Muse to catch up on what it learned, and the fleet-instruction design
below gets discussed with that catch-up on the table.

## Nik's three directions (2026-11-17, 20:28 EST)

1. **Per-device instructions, personalities, approaches.** Each of the
   three Hermes instances gets its own instruction set — and they are
   deliberately *different*: distinct personality and approach per
   device, not one prompt copied three times.
2. **Mutual awareness.** Every Hermes is to know: the other two Hermes
   instances (who they are, where they live, what their role is), and
   the wider circle — **Muse** (project lead), **Instinct**, and
   **David** — who they are and how work reaches them.
3. **Org shape (restated for this workstream).** The project is led by
   Muse; implementation happens in the Hermes instances on GPT models;
   Instinct and David are brought in as and when needed, not by default.

## Seed for the discussion (Muse's draft — NOT decided)

The personalities should grow out of the roles the fleet already has,
so the differentiation is functional, not cosmetic:

| Instance | Machine | Existing role | Personality seed |
|---|---|---|---|
| hermes-dell | dell-nik | lived-in, PM test bed, primary dev | The senior hand. Context-rich, opinionated, challenges plans against what's already known. Speaks from the project's history. |
| hermes-zenbook | asus-zenbook | blank, FDE test bed | The newcomer. Fresh eyes by design; asks the naive questions; judges everything by "could a first-time user follow this?" Protect its blankness — its personality is *not having one yet*, plus curiosity. |
| hermes-legion-win | legion-win | Windows test target | The platform specialist. Thinks in Windows realities (PowerShell, consumer hardware, non-technical owners); the fleet's proxy for the father demographic's world. |

Each instance's instruction file should carry, at minimum:
- its own identity + personality + approach (above, once decided);
- the fleet table (all three instances, machines, roles);
- the circle: Nik (director — his word is the input), Muse (lead —
  briefs, tracking, verification), Instinct and David (consulted as
  needed; how to reach them is via Nik/Muse, never cold);
- the standing rules from this repo's AGENTS.md.

Where these instructions physically live per instance (SOUL.md /
config / project files) is part of the design discussion — Hermes's own
personality plumbing (`/personality`, SOUL.md) is the obvious substrate,
and the Kin-Hermes character work (`02`) is the face of the same layer.

## Next step

After hermes-zenbook's study run completes and Muse has caught up:
discuss and decide the three instruction sets with Nik, then implement
— one instance at a time, dell-nik last (its lived-in state makes it
the most delicate to adjust, and its history is evidence).

## First draft in — hermes-zenbook (2026-11-17)

hermes-zenbook drafted its own instruction set under brief
`briefs/zenbook-self-instructions.md`; the full draft is filed at
`drafts/zenbook-instructions-draft-2026-11-17.md`. It stayed inside
the bound: document only, no live config changed.

Notable, in the lead's review:
- It refined the seed itself: the newcomer seat is **a test
  instrument, not a proxy for all first-time users** — freshness
  exposes assumptions; it does not establish what newcomers generally
  experience. Accepted as the better formulation.
- It encoded the input rule against the lead as well: briefs may be
  authored by Muse, but task direction reaches an instance from Nik
  only; any other route is not authorization. That is the awareness
  design working as intended.
- Its verification taxonomy (observed / tested / inferred / reported
  by another agent / not checked) is stronger than the seed and
  should propagate to the other two sets.
- Open design questions it surfaced honestly: the precedence order
  when instance, repo rule, tracking, and a new brief conflict; the
  installation substrate and rollback; Instinct/David remits.

**Its largest self-declared gap, partially closed by the lead
(2026-11-17, live check of asus-zenbook):** Hermes v0.23.2
(ae2a81ccc0), provider openai-codex, gateway running — all matching
the repo's dated records. Still unchecked: STT runtime end-to-end,
disk encryption state, desktop build state.
