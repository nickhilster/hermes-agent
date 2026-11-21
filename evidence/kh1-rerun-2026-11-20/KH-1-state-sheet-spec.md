# KH-1 — Glyph state-sheet production specification

Status: production specification draft for KH-1; geometry below is a proposed canonical construction derived from the locked brief and v4 concept, not traced source geometry. One SVG master; states are parameter configurations, not alternate drawings.

## Evidence and design boundary

The persona document locks a circular head, vertical staff, two wing arcs, electric blue `#3847FF` on black, a face of brows + two eyes + lips, and tighter/higher/smaller-than-head winged-helm wings. The v4 image visibly presents five examples left-to-right: neutral/alert, running, review (one wing raised), failed (drooped wings, closed eyes, downturn mouth), and waiting/content (upward eyes, soft brows, smile). These observations establish style and state cues, not exact source coordinates. The requested seven states include two additional configurations specified below. All dimensions and timings below are explicit proposed implementation values where the references do not prescribe them.

## Canonical master

Use SVG `viewBox="0 0 100 120"`, preserveAspectRatio `xMidYMid meet`. Background transparent; preview canvas black `#000`; primary stroke `#3847FF`, face stroke `#FFFFFF`. All strokes round-cap/round-join, no fills except eyes may be white filled shapes. Master center axis x=50. Head circle center (50,38), radius 19; stroke 2.4, no fill. Staff is a path M50 57 L50 103, stroke 2.4; terminal ring centered (50,108), r=2.7, stroke 2.4, fill none. The staff begins at the head lower tangent and ends in the terminal ring.

Wing helm arcs are two symmetric closed-outline cubic paths, behind head and staff, stroke 2.4, fill none. Left: `M34 25 C28 14 22 10 15 11 C19 16 20 22 19 29 C23 26 28 25 34 28`. Right is x-mirror around 50: `M66 25 C72 14 78 10 85 11 C81 16 80 22 81 29 C77 26 72 25 66 28`. Render each as a single open path (the endpoint does not connect); the wording “closed-outline” above means contour-like arc, not a closed fill. Wings remain within x=15..85, y=10..29: smaller and higher than the head. State wing pose applies a transform about each wing root (34,26)/(66,26), never replaces the path.

Face anchors in head-local coordinates (head origin x=50,y=38): brow baselines y=-8, eyes centers (-7,-1)/(+7,-1), mouth center (0,+9). Default brow span 8, eye span 5.5, mouth span 8. Brows, eyes, and lips are independent paths/groups with stable IDs `browL`, `browR`, `eyeL`, `eyeR`, `lips`. Keep face within circle with at least 3 units clearance from stroke. Use geometry definitions in the state table; interpolate coordinates/shape morphs only between matching named anchors. Do not scale or translate face independently of the head.

## State configurations

Coordinates below are relative to face origin (50,38). Brow forms: level = line from x±4,y=-8; determined = inner ends y=-10, outer ends y=-6; raised = inner y=-9, outer y=-11; sad = inner y=-6, outer y=-10; soft = shallow quadratic arc with ends y=-8 and center y=-6. Eye forms: oval = 5.5×7; narrow = 6×2.2 horizontal capsule; dot = r=1.7; closed = quadratic arc endpoints x±2.5,y=0 with control (0,2); pleased = upward arc endpoints x±2.5,y=1 with control (0,-2). Mouth: neutral horizontal 8-unit line; pressed 7-unit line; smile quadratic ends x±4,y=10 control (0,7); frown ends x±4,y=8 control (0,11); open ellipse 5×4, voice-driven vertical radius 1..4. “Wing pose” is per-wing rotation around root: neutral 0°; swept -12° rearward (left) / +12° rearward (right); raised outer tips 18°; spread 8° outward; drooped -18° downward. Rotation sign is visualized in the canonical coordinate system; preserve bilateral readability.

| State | Brows | Eyes | Lips | Staff | Wings |
|---|---|---|---|---|---|
| idle | level | oval | neutral | 0° | neutral |
| run | determined | narrow | pressed; voice may override | 12° toward travel | swept |
| review | raised | dot | neutral, then slight open on speech | 0° | one raised 18° (alternate sides every entry, not during hold) |
| wave | raised | oval | smile | 0° | one raised 24°, other neutral |
| jump | raised | oval | open ellipse | 0° | spread 14° |
| failed | sad | closed | frown | 8° slump | drooped |
| waiting | soft | pleased | smile | 0° | slow-open to 6° outward |

## Motion and transitions

All values are milliseconds; easing is cubic-bezier(x1,y1,x2,y2). Default state transition 320 ms, `cubic-bezier(0.22,0.61,0.36,1)` (out); no spring, overshoot, bounce, squash, or scale pulse. Interpolate the same master group's transforms/anchors. Simultaneous channels start together unless specified.

- idle→run: 90 ms staff lean lead, then 260 ms wing sweep and determined face; total 350 ms. On completion, repeat a 720 ms glide cycle: staff angle 10°→13°→10°, wings -10°→-14°→-10°; linear keyframes at 0/360/720 ms, no vertical bob.
- run→idle/review: 300 ms glide deceleration, `cubic-bezier(0.4,0,0.2,1)`; staff first returns to 0° over 180 ms, face settles over 300 ms.
- any→review: 260 ms out; raised brow/dot eyes at 140 ms, one wing reaches 18° at 260 ms. Hold until state changes.
- any→wave: 180 ms brow/eye recognition, then wing lifts from 0° to 24° over 300 ms; total 480 ms. Hold 700 ms, lower over 260 ms; state remains wave until caller changes it.
- any→jump: 120 ms anticipation via eye/brow only (no body translation), then 220 ms wing spread and open-mouth reveal; settle 180 ms. No vertical displacement. Hold 250 ms before caller transition.
- any→failed: 240 ms staff slump, 180 ms wing droop and face change; total 420 ms; `cubic-bezier(0.4,0,1,1)`. Hold, no automatic recovery.
- any→waiting: 320 ms to soft face; wings slowly open from neutral to 6° over 900 ms. Hold.
- idle loop: period 6000 ms. At t=0 neutral; 1800 ms eye glance (both pupils shift 0.8 units right, 240 ms), return by 2400; blink 120 ms close at 4100, reopen by 4260; rest. No head bob or staff bounce. Add ±0–0.4° wing drift only if reduced motion is off.

Respect reduced-motion: replace loops with static pose and use 100 ms crossfade for state changes. Never convey an operational status through movement alone; caller owns state correctness.

## Voice amplitude → mouth

Use BoardyAnimated's documented pattern as an architectural precedent: amplitude + state drive mouth/gaze/posture, controls clamped, reduced-motion honored. Exact Boardy numeric constants were not supplied in the estate review; values here are proposed KH-1 defaults, not copied settings.

Input is normalized RMS amplitude `a∈[0,1]` per 20 ms audio frame. Clamp input; apply noise gate 0.035; remap `u=clamp((a-0.035)/(0.65-0.035),0,1)`. Mouth vertical radius = `1 + 3u` units; width fixed 5 units. Smooth with attack time constant 45 ms and release 110 ms (one-pole exponential, frame delta-aware). Quantize visual rendering to: closed (u<0.08), small (0.08–0.35), medium (0.35–0.70), wide (>0.70). Mouth changes only while speech output is active; otherwise retain state mouth. Clamp radius [1,4]; reduced-motion may retain amplitude animation because it is speech articulation, but cap updates to 15 fps. Voice does not alter brows, eyes, staff, or wings. State-specific pressed/frown/smile is suspended during active speech and restored with 120 ms ease-out.

## Boardy theme.json-style mapping sketch

Shape follows `reference/boardy-theme-example.json` (schemaVersion/name/version/viewBox/layout/eyeTracking/states/idleAnimations/timings). This is a mapping sketch, not claimed to validate against an existing schema; state values point to configurations of one master, not separate SVG assets.

```json
{
  "schemaVersion": 1,
  "name": "Glyph",
  "author": "Nous Research / Kin-Hermes",
  "version": "1.0.0",
  "description": "Single-master Hermes glyph; activity states are configurations.",
  "viewBox": { "x": 0, "y": 0, "width": 100, "height": 120 },
  "layout": {
    "contentBox": { "x": 12, "y": 8, "width": 76, "height": 103 },
    "marginBox": { "x": 0, "y": 0, "width": 100, "height": 120 },
    "centerX": 50,
    "baselineY": 111,
    "visibleHeightRatio": 0.86,
    "baselineBottomRatio": 0.075
  },
  "eyeTracking": {
    "enabled": true,
    "states": ["idle", "waiting"],
    "eyeRatioX": 0.5,
    "eyeRatioY": 0.5,
    "maxOffset": 0.8,
    "bodyScale": 0,
    "ids": { "eyes": "eyes-js", "body": "head", "shadow": "none" }
  },
  "states": {
    "idle": { "master": "glyph-master.svg#glyph", "config": "idle", "transitionMs": 320 },
    "run": { "master": "glyph-master.svg#glyph", "config": "run", "transitionMs": 350 },
    "review": { "master": "glyph-master.svg#glyph", "config": "review", "transitionMs": 260 },
    "wave": { "master": "glyph-master.svg#glyph", "config": "wave", "transitionMs": 480 },
    "jump": { "master": "glyph-master.svg#glyph", "config": "jump", "transitionMs": 520 },
    "failed": { "master": "glyph-master.svg#glyph", "config": "failed", "transitionMs": 420 },
    "waiting": { "master": "glyph-master.svg#glyph", "config": "waiting", "transitionMs": 320 }
  },
  "idleAnimations": [
    { "animation": "idle-glance-blink", "duration": 6000 }
  ],
  "timings": {
    "minDisplay": { "review": 400, "wave": 700, "jump": 250, "failed": 1200 },
    "autoReturn": { "wave": 1260, "jump": 520 },
    "reducedMotionTransitionMs": 100
  },
  "motion": {
    "defaultEasing": [0.22, 0.61, 0.36, 1],
    "overshoot": false,
    "bounce": false,
    "reducedMotion": "static-pose-crossfade"
  },
  "voice": {
    "source": "normalized-rms",
    "frameMs": 20,
    "noiseGate": 0.035,
    "fullScale": 0.65,
    "mouthRadius": { "min": 1, "max": 4 },
    "attackMs": 45,
    "releaseMs": 110,
    "shapeThresholds": [0.08, 0.35, 0.70]
  }
}
```

## Acceptance checks

1. Source inspection: exactly one reusable master geometry and stable face IDs; all seven states resolve to that master; no state-specific duplicate character drawings. Confirm paths and numeric transforms against this document.
2. At 16 px rendered height on black: head circle, staff/ring, bilateral helm wings, two eyes, two brows, and lips remain distinguishable. No wing reads as a lower petal; use pixel-aligned stroke/hinting only if it preserves the geometry. Review at 1× device scale, not enlarged-only.
3. At 64 px: compare all seven states side-by-side with the table; verify brows/eyes/lips independently distinguish run, review, failure, waiting; verify staff and wing poses. Automated image snapshots may compare stable geometry and state anchors; allow rasterizer antialiasing, not altered proportions.
4. Full-screen: inspect on black and transparent backgrounds; verify stroke color exactly `#3847FF`, white face, round joins/caps, no accidental fills, clipping, or overlap. Verify transition timings with a frame capture/timeline and confirm no bounce/overshoot or vertical jump.
5. Motion: measure idle period at 6000 ms; verify run glide period 720 ms; reduced-motion disables loops. Trigger every ordered transition at least once and check completion/hold behavior.
6. Voice: feed RMS values 0, 0.035, 0.35, 0.65, >0.65; verify gate, monotonic mouth opening, [1,4] clamp, attack/release smoothing, and state-mouth restoration. Include noisy near-gate and abrupt onset/release cases.
7. Mapping: parse JSON; assert schemaVersion 1, exact seven state keys, and identical master reference in every state. This checks JSON syntax and mapping intent, not compatibility with an undocumented consumer.
