# KH-1 — Glyph state sheet, production spec (RIG EDITION)

Status: **KH-1 deliverable**, approved by Nik 2026-11-18. Supersedes
the failed graveyard-run assignment (KH-1 tracker, 2026-11-18): every
input that run could not find is named below by repo path.
Drafted by Muse, 2026-11-18, from verified sources only:
docs/02 (locked v4 concept), `assets/hermes-character-concept-v4.webp`
(read directly), the BoardyAnimated V2 rig source (`boardyV2Types.ts`,
`boardyV2ExpressionRuntime.ts`, `boardyV2Presets.ts`), the
boardy-at-the-desk `themes/boardy/theme.json` schema, and the
hermes-zenbook estate review of 2026-11-17.

**Direction change recorded (Nik, 2026-11-18):** beyond simple SVG.
The desk generation of Boardy mapped states → static SVG files. The
Glyph is built the BoardyAnimated V2 way: **one rigged master, a
continuous control space, states as control configurations** — SVG is
the drawing layer, not the animation system. A second input the same
day: the Nous brand film ends with its mascot redrawn as an engraved
emblem on a banner. Register consequence, binding on all motion below:
**heraldic stillness.** The Glyph at rest is an emblem. Motion is the
exception — it darts or glides between poses, then *holds*. Nothing
bounces, wobbles, or idles in a loop of fidgets.

---

## 1. Canonical geometry (the master rig drawing)

Design grid: viewBox `0 0 240 240`. Single master; every state is a
configuration of these primitives — never a redraw. All strokes
`#3847FF` (electric blue), stroke-width 5, round caps/joins, no fills,
on transparent ground (composites on black `#00000E` per the brand
booklet palette). Face features are drawn in white (`#FFFFFF`) at
stroke-width 4 — in the v4 art the structure is blue, the face is pale;
that two-tone split is part of the identity.

| Primitive | Geometry (design grid) | Pivot / notes |
|---|---|---|
| Head | circle, centre (120, 78), r 34 | tilts around centre |
| Staff | line (120, 112) → (120, 214) | pivot at (120, 112), the chin junction |
| Finial | circle, centre (120, 221), r 6 | rides the staff |
| Helm wings (small pair) | petal paths rooted at (97, 60) and (143, 60), tips reaching ≈ (92, 30) / (148, 30) | the winged helm; sit tighter and higher than the v1 art, smaller than the head (graveyard brief). Slight articulation only (±6°) |
| Shoulder wings (large pair) | petal paths rooted at the junction (120, 110). Spread keyframe: tips at ≈ (26, 96) / (214, 96), upper edge bowed up, lower edge bowed down (the horizontal crescents of the art). Droop keyframe: tips at ≈ (74, 178) / (166, 178), petals hanging along the staff | pivot at root; shape = blend of the two keyframes (same point count, path-morph) |
| Brows | two strokes, length 13, centred (±14, −10) rel. head centre | each brow: inner/outer endpoint heights + angle are independent controls |
| Eyes | two ovals 4 × 7 at (±13, +2) rel. head centre | openness scales height; closed states replace the oval with an arc (curvature control) |
| Lips | one stroke, width 12, centred (0, +15) rel. head centre | curve + openness morph (§5) |

Proportions from the art, binding: head Ø 68; staff ≈ 2.2 head-Ø below
the junction; spread wingspan ≈ 2.8 head-Ø. At 16 px the silhouette
must still read as circle + staff + two wings.

## 2. The rig — control space

Modelled directly on `BoardyV2Controls`: every control is a number
with a global limit; each state preset may narrow it with safe ranges;
the runtime clamps (never trusts) incoming values. Composition is
layered, exactly as in `boardyV2ExpressionRuntime.ts`:

**resolved = clamp( state preset ← emotion overlay ← moment overlay ← voice/gaze drivers )**

| Control | Range | Drives |
|---|---|---|
| `staffTilt` | −18…18° | staff + finial lean (body language: upright = ready, lean = moving, slump = failed) |
| `headTilt` | −12…12° | head rotation |
| `headY` | −4…6 | head bob offset (glide only; no oscillation except the idle breath, §4) |
| `wingSpreadL/R` | 0…1 | shoulder-wing shape blend: 0 = droop keyframe, 1 = spread keyframe |
| `wingLiftL/R` | −25…50° | shoulder-wing root rotation (raise one wing = wave) |
| `wingSweep` | 0…1 | both shoulder wings swept back (run) |
| `helmWingAngle` | −6…6° | helm-wing micro-articulation |
| `browInnerL/R`, `browOuterL/R` | −6…6 | brow endpoint heights (raise, level, furrow) |
| `eyeOpen` | 0…1 | eye oval height; 0 = closed |
| `eyeArc` | −1…1 | closed-eye curvature: −1 downcast arc, +1 content arc |
| `gazeX`, `gazeY` | −1…1 | pupil/eye-group offset (max ±3 grid units), eye-tracking driver (§4) |
| `mouthCurve` | −1…1 | lip stroke curvature: −1 frown, 0 flat, +1 smile |
| `mouthOpen` | 0…1 | lips part: line → oval morph (voice driver, §5) |
| `mouthWidth` | 0.6…1.3 | lip width scale |
| `blink` | 0…1 | momentary eye closure (runtime-scheduled, §4) |

Presets carry `transitionMs` and, for moments, `returnTo` +
`returnAfterMs` (BoardyV2 preset semantics, unchanged).

## 3. The seven states (activity vocabulary, per docs/02 + KH-1)

Values are targets in the control space; the runtime interpolates.
Face-first rule (KH-1 acceptance): every state must be readable from
the face alone; wings/staff confirm, they do not carry.

| State | Brows | Eyes | Lips | Wings | Staff/head | Transition |
|---|---|---|---|---|---|---|
| **idle** | level (0, 0) | open 1, gaze free | flat (curve 0) | spread 0.55, lift 0 | tilt 0 | — (home pose; the emblem at rest) |
| **run** | furrowed: inner −4, angle ∓10° | open 0.8, gaze forward | flat, width 0.8 | sweep 1, spread 0.7 | staffTilt +14 (leaning in), headTilt +6 | dart, 150 ms |
| **review** | one raised (outer +4, working side), other level | open 0.85, gaze down (+0.6 Y) at the work | flat, slight press (width 0.7) | spread 0.25 (tucked, out of the way) | headTilt −3 toward the work | glide, 450 ms |
| **wave** *(moment)* | raised: outer +5, inner +2 | open 1, gaze at the human | smile +0.6 | one wing lift +48, spread 0.9; other spread 0.5 | tilt 0 | dart up 180 ms, hold, return after 1,600 ms |
| **jump** *(moment)* | raised arcs (inner +3, outer +5) | closed, arc +1 (content) | smile +0.9, open 0.25 | spread 1, lift +12 both | headY −4 (rise, glide — no bounce) | glide 380 ms, hold 900 ms, return |
| **failed** | worried: inner +5, outer −2 (the Λ of concern) | closed, arc −0.7 (downcast) | frown −0.7 | spread 0.05 (full droop) | staffTilt −8 (slump), headTilt −5 | slow glide, 700 ms — failure lands gently |
| **waiting** | level, soft (outer +1) | open 0.7, gaze slow-drifting | flat, curve +0.1 | spread 0.45, lift sway ±3 (the only idle sway allowed) | tilt 0 | glide, 600 ms |

Speaking is not an activity state; it is the voice driver (§5) layered
over whichever state is active — as Boardy layers delivery over state.

## 4. Motion law

- **Darts**: 120–180 ms, ease-out cubic — arrivals, attention shifts, the wave.
- **Glides**: 380–700 ms, ease-in-out — posture changes, failure, settling.
- **No overshoot, ever.** No spring, no bounce, no wobble controls
  (BoardyV2 has `flapWobble`; the Glyph rig deliberately does not).
- **Idle loop**: breath = `headY` ±1.2 on a 4,000 ms sine; blink every
  3,200–5,400 ms (randomised), 110 ms close/open; gaze shifts at most
  every 2,500 ms. Everything else is stillness.
- **Eye tracking** (from the desk theme's `eyeTracking` block): in
  idle/waiting, gaze follows the pointer / active window direction,
  clamped to ±3 units, body (head) follows at 0.28 ratio. Off in all
  working states — he looks at the work, not at you.
- **Reduced motion**: darts/glides become 0 ms cuts; breath, sway and
  blink disabled; states remain fully readable (BoardyAnimated honors
  reduced-motion; so do we).

## 5. Voice — amplitude → mouth (the BoardyAnimated pattern)

- Input: RMS amplitude of the character's own TTS output, 0…1,
  analysed per `audioAnalysis.ts`'s approach (the ancestor rig's
  method, per the estate review).
- Gate: below 0.02 → mouth closed (curve from state, open 0).
- Mapping: `mouthOpen = clamp((amp − 0.02) × gain)`, gain default 1.6
  (a delivery-style control, as BoardyV2's `mouthGain`).
- Shape: open 0 = the lip stroke; 0→0.5 the stroke parts into a narrow
  oval; 0.5→1 the oval grows. Width follows at 0.85…1.15.
- Smoothing: attack 40 ms, release 130 ms (speech reads as speech,
  not as a level meter).
- This is amplitude lip-sync, honestly named — no viseme claims.

## 6. Theme mapping (KH-2 target, boardy-at-the-desk schema shape)

```json
{
  "schemaVersion": 2,
  "name": "Glyph",
  "description": "Hermes himself — the messenger-guide, as a rigged line character.",
  "viewBox": { "x": 0, "y": 0, "width": 240, "height": 240 },
  "rig": "glyph-rig.json",
  "states": {
    "idle":    { "preset": "idle" },
    "run":     { "preset": "run" },
    "review":  { "preset": "review" },
    "wave":    { "preset": "wave", "moment": true },
    "jump":    { "preset": "jump", "moment": true },
    "failed":  { "preset": "failed" },
    "waiting": { "preset": "waiting" }
  },
  "eyeTracking": { "enabled": true, "states": ["idle", "waiting"],
                   "maxOffset": 3, "bodyRatio": 0.28 },
  "voice": { "amplitudeToMouth": { "gate": 0.02, "gain": 1.6,
             "attackMs": 40, "releaseMs": 130 } },
  "sounds": { "complete": "complete.mp3", "confirm": "confirm.mp3" }
}
```

Schema v2's one structural change from Boardy's v1: states point at
**rig presets**, not image files. KH-2 removes the Petdex gallery path
in Teambotics-Inc/hermes-agent and maps the existing activity-state
plumbing onto these presets.

## 7. Acceptance checks (KH-1)

1. **16 px**: silhouette reads (circle, staff, wings); run vs idle vs
   failed distinguishable by wing/staff configuration alone.
2. **64 px**: all seven states identified from the face alone by a
   reviewer who has not seen the labels.
3. **Full-screen**: line quality holds (uniform stroke, no raster),
   the two-tone face/structure split is visible.
4. **Rig discipline**: fuzz the controls — no input combination
   escapes the global limits or a preset's safe ranges (clamp test,
   BoardyV2 runtime semantics).
5. **Motion law**: no transition in the sheet uses overshoot easing;
   idle 60-second observation shows breath + blink only.
6. **Voice**: a spoken sentence produces mouth motion that starts and
   stops with the audio (±150 ms), and silence closes the mouth.

## Open items (Nik's call, not the builder's)

- **Wave and jump as moments vs states**: the Petdex vocabulary lists
  them as states; this spec treats them as moment overlays with
  return-to-state (BoardyV2 semantics), which is how the desk will
  actually use them. Flagged, not hidden.
- **Sound set**: Boardy's theme carries complete/confirm sounds; the
  Glyph's voice layer (docs/02 §3) is a separate milestone — sounds
  here are placeholders in the schema only.
- **Where he lives first**: sidebar/home presence vs a free desk
  window (boardy-at-the-desk style) is a KH-2/host decision; this
  spec is host-agnostic.
