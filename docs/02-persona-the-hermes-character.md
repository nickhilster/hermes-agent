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

## Concept v1 — "The Glyph" (Muse's proposal, 2026-11-17; concept art: `assets/hermes-character-concept-v1.webp`)

Nik's brief: simple shapes; not cute like Jolly; not corporate like a desk
mascot; simple design. The proposal: **don't design a creature — promote
their own caduceus to a character.** Hermes's CLI banner already carries a
caduceus hero mark. Reduced to primitives, it is a living glyph:

- **A circle** — the head. One eye, drawn as a single line or dot; the eye
  is the entire face. Expression = what the line does (flat = calm, dot =
  attention, arc = contentment, gone = asleep/failed-quiet).
- **A vertical line** — the staff, ending in a small circle. The staff's
  tilt is the body language: upright = ready, leaning = moving, slumped =
  failed.
- **Two wing arcs** — the winged helm, and the main actors. Wings carry the
  emotional register: spread = alert/welcome, swept back = running, one
  raised = wave/approval-ask, drooped = failed or sad, slow-open = waiting.

**States map 1:1 onto the existing Petdex activity vocabulary**
(`idle / run / review / wave / jump / failed / waiting`) — so the character
plugs into the state plumbing Hermes already ships, but as a first-party
Hermes instead of a borrowed gallery sprite. In the Boardy-at-the-Desk
architecture (`theme.json`: states → assets + geometry), each state is a
wing/staff/eye configuration — a handful of SVG primitives, animatable with
darts and glides (a messenger moves in straight lines; he never bounces).

Register: dry, quick, unbothered. Electric blue `#3847FF` line on black, or
B/W with the blue as accent — Nous's own palette. He reads at 16px as a
favicon and at full-screen as the Ready Surface's host (`08`). He is not a
pet you adopt; he is the colleague who was always in the machine — the god,
on duty, in three shapes.

Known refinement for v2 (concept art is a sketch, not the mark): the wings
in v1 drift floral/pinwheel in some states — they should sit tighter and
higher, winged-helm style, smaller than the head; the lower "petal" reading
must go.

## Concept v2 — the face (Nik's direction, 2026-11-17; art: `assets/hermes-character-concept-v2.webp`)

Nik's correction to v1: a glyph alone is a logo; **the character needs
eyes and lips** — that is what personifies him. V2 keeps the three-shape
body (circle / staff / wings) and adds the minimal face:

- **Two eyes** — small ovals or dots. Grammar: open ovals = alert; narrowed
  slashes = effort/running; dots = attention/review; closed curves =
  failed or resting; upward arcs = contentment.
- **Lips** — one small mouth line. Grammar: flat = neutral/dry; tiny curve
  = pleased; small downturn = failed, stated plainly without drama.

The face is deliberately the *only* human layer. No nose, no hair, no body,
no costume — personification by the smallest possible dose, so he stays a
mark at 16px and becomes a someone at conversation size. The warmth this
adds is the point (Nik's call): the wings and staff keep the dignity, the
eyes and lips carry the relationship. States in v2 art, left to right:
alert · running (determined) · review (attentive, one wing raised) · failed
(drooped, eyes closed, small frown) · waiting (content arcs).

## Concept v4 — brows complete the face (Nik, 2026-11-17; art: `assets/hermes-character-concept-v4.webp`)

Nik tested the one-eye variant direction and settled it by eye: **the
two-eyes version wins.** (A one-eye + brow + lips sketch exists in assets
as `hermes-character-concept-v3-one-eye.webp`, kept for the record, not the
direction.) His other ruling stands and completes the face: **eyebrows are
really important** — the whole emoji system, and South Park's entire
emotional range, run on eyes + lips + brows. The face grammar is therefore
three elements, and the brow does the heaviest lifting:

| Element | Grammar |
|---|---|
| Brows | level = calm/alert · angled down-in = determination/effort · raised = curiosity, review, an approval ask · slanted up-in = sadness, apology (failed) · soft arcs = contentment |
| Eyes | ovals = alert · narrowed = effort · dots = attention · closed curves = failed/resting · upward arcs = pleased |
| Lips | flat = dry/neutral · pressed = effort · tiny curve = pleased · downturn = failure stated plainly · gentle smile = ready/waiting |

The animation consequence (Nik's point): lips earn their place *in
motion* — a mouth that opens, presses, and settles is what makes a state
change read as a feeling instead of an icon swap. The state sheet
milestone must spec brow/eye/lip keyframes per state, not just wing and
staff poses.
