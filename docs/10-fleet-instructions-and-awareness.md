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
