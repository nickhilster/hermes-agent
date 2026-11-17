# 02 — Persona: the Hermes character

*Direction set by Nik, 2026-11-17: "We need to start with a personality. Step one
is the persona angle."*

## The mascot audit (checked 2026-11-17 — web + the Hermes codebase itself)

**Hermes has a mascot. It does not have a persona.**

What exists today:

| Piece | What it is | Why it isn't a person |
|---|---|---|
| **The Nous Girl** | Nous Research's company mascot/logo: retro 1970s-manga girl, bob + headphones, black-and-white with electric blue `#3847FF` | A static brand illustration. She never speaks, moves, or appears as your agent. |
| **The classical Hermes figure** | Multi-armed, winged-helmet line art on electric blue; poster art for Hermes Agent; caduceus banner art in the CLI | Iconography, not a character. |
| **SOUL.md + `/personality`** | A real personality *system*: SOUL.md is identity slot #1 in the system prompt; presets overlay it per session | Invisible text. No face, no voice, no presence in the room. |
| **Pets (Petdex)** | Animated mascot sprites reacting to agent activity — `idle / run / review / wave / jump / failed / waiting` — across CLI, TUI and desktop | Third-party gallery sprites, off by default, and per Hermes's own docs "purely cosmetic… no effect on the agent's behavior." A borrowed sprite is not *Hermes*. |
| **hermes-bots avatars** | Desktop plugin: avatar picker, bot rows, group-room avatars | Plumbing for instances, not a flagship character. |

The ingredients of a person — brand face, prompt identity, an activity-state
animation model, avatar plumbing — exist in **four separate systems that never
meet**. Compare Muse: Jolly is not a logo *plus* a personality *plus* a pet. Jolly
is one character who is the interface and the relationship. That unity is the gap.

## The remix: Boardy's architecture, Hermes's face

Nik has already built this layer once — for Boardy, a character that started as
a cardboard cutout. The plumbing lives in the `boardy-at-the-desk` repo
(git-verified: 292 commits, authored by Nik):

- A `theme.json` manifest system: each persona theme maps **named states →
  assets**, with layout geometry, **eye tracking**, **idle animations**, sounds
- A **separate voice layer**: voice provider, voice policy, preset registry,
  spoken-voice runtime
- Per character = **visual theme + voice preset + behavior states**
- Plus the lived work around it: BoardyAnimated (103 commits), an animated pitch
  site, a character taught over days of real interaction, voice-note interviews

**The Hermes character build applies that architecture to Nous's own assets:**

1. **Face** — derived from their own brand: the Nous Girl and/or the classical
   Hermes figure, in their cyber-classical style and palette (electric blue
   `#3847FF`, B/W manga contrast). Not a new mascot imposed on them — *their*
   mascot, brought to life.
2. **States** — the Petdex activity vocabulary (`idle / run / review / wave /
   jump / failed / waiting`) is already the right state model; the character
   adopts it natively instead of borrowing gallery sprites.
3. **Voice** — a voice layer with provider/policy separation (per the Boardy
   plumbing), so the character can speak in onboarding, in completions, in the
   moments that build a relationship — and stay silent the rest of the time.
4. **Soul** — the character *is* the SOUL.md made visible: the persona the prompt
   describes is the one you see and hear. One identity across prompt, face and
   voice, per instance, editable by its human.
5. **Presence points** — first-run onboarding (`03`), the desktop sidebar/home,
   completion and failure moments. Not everywhere; a person who never stops
   performing is exhausting. Good help is quiet until the exact moment it matters.

Not "as cute as Jolly" — that is Muse's register, and copying it would be a
costume. Hermes's register is its own: classical, wry, competent — the messenger
who has seen everything twice.

## Status

Concept stage at seed (2026-11-17). Next step: a character spec milestone
(state sheet + voice spec + presence map) written as a brief Nik can drop to
hermes-dell to build in the fork, the same way the sidebar work ran.

## The character is Hermes himself (Nik, 2026-11-17)

Nik, reviewing the Hermes site: the Greek-mythology commitment is total —
cyber-classical, psychedelic, statuary and radiating line art — **and there is
still no single character.** You cannot name the product after a god and then
not have the god show up.

And Hermes is the *right* god for an agent — not light (that's Apollo's
department): **Hermes is the messenger of the gods, the guide of travellers,
the trickster, the inventor of language, and the psychopomp — the guide who
walks souls between worlds.** An agent that carries messages between the human
and the machine, between devices, between the phone in your pocket and the
fleet at home; that guides its human through systems they can't see; that is
quick, wry, and a little bit thief-of-fire on your behalf — that is not a
mascot brief we have to invent. It is sitting in their own name, unused.

So the character spec sharpens: **Hermes, the messenger-guide, rendered in
Nous's own cyber-classical psychedelic register** — winged helm and caduceus
line art given the state/voice treatment (`02` above), the Nous Girl lineage
kept as the house style rather than a competing face. The mythology is the
permission: they already chose a god with a personality. We just let him be
one.
