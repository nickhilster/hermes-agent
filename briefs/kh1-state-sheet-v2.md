# Brief KH-1 (v2) — Glyph state sheet, production spec
## For: hermes-zenbook, on asus-zenbook. Directed by Nik through Muse, 2026-11-20.

DRAFT ONLY: write the spec document; do not modify the fork, the live
install, or any code.

## Inputs — verified present at these exact absolute paths on this machine

The canonical project checkout on this machine is `/home/nik/dev/kin-hermes`
(a clone of the project repo nickhilster/hermes-agent). Read these files
at these paths — do not search other checkouts, and do not substitute
similar files:

1. `/home/nik/dev/kin-hermes/docs/02-persona-the-hermes-character.md`
   — the locked Glyph concept: circle head, vertical staff, two wing
   arcs, electric blue #3847FF on black; face grammar = brows + two
   eyes + lips; wings sit tighter/higher than the v1 art, winged-helm
   style, smaller than the head.
2. `/home/nik/dev/kin-hermes/assets/hermes-character-concept-v4.webp`
   — the locked concept art (v4). Open and look at it.
3. `/home/nik/dev/kin-hermes/evidence/zenbook-estate-review-2026-11-17.md`
   — your own estate review: BoardyAnimated's rig drives mouth/gaze/
   posture from audio amplitude + state.
4. `/home/nik/dev/kin-hermes/reference/boardy-theme-example.json`
   — a real boardy-at-the-desk theme.json; the format reference for
   the theme-mapping sketch.

If any of these files is missing or unreadable at the path above, STOP:
write the failure report (below) naming exactly what is missing, and do
not improvise, search elsewhere, or invent geometry from memory.

## Task

Produce the production state-sheet spec a builder can implement
without further design decisions:

1. Canonical SVG geometry: viewBox, the exact primitives for head,
   staff, wings (paths/coordinates, stroke widths), and the face
   element anchor points. One master glyph; states are configurations
   of it, never redraws.
2. The 7 activity states (idle, run, review, wave, jump, failed,
   waiting): for each — brow position/shape, eye shape, lip shape,
   staff tilt, wing pose, in the locked face grammar.
3. Motion: keyframes and timing per state transition. A messenger
   darts and glides, never bounces. Spec durations and easing in
   numbers, and the idle loop.
4. Voice: amplitude→mouth mapping (from the BoardyAnimated rig
   pattern): input range, mouth shapes, smoothing.
5. A theme.json-style mapping sketch (state → configuration) in the
   boardy-at-the-desk theme format of input 4, so the fork port
   (KH-2) has a target.
6. Acceptance checks: how a reviewer verifies an implementation
   matches this spec at 16px, 64px, and full-screen.

## Deliverables — both required, on this machine

- `/home/nik/kin-hermes-work/kh1/KH-1-state-sheet-spec.md` — the spec.
- `/home/nik/kin-hermes-work/kh1/KH-1-REPORT.md` — the report: what you
  read (with paths), what you produced, every claim labelled
  observed / tested / inferred / not checked, and anything you did
  NOT verify. The report is required on failure too — if you are
  blocked, the report names the blocker and what was left unchanged.
  A run that produces no report is a failed run, whatever its exit
  code says.

End your final message with a 5-line summary.
