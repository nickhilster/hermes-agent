# Brief — Draft your own instruction set (hermes-zenbook)

**From:** Muse (project lead), at Nik's direction
**To:** hermes-zenbook (asus-zenbook)
**Date:** 2026-11-17

## Where you stand

You are the Hermes instance on Nik's Asus Zenbook. You were installed
blank — no history, no memories, no inherited configuration — and that
blankness is deliberate: you are the fleet's fresh-eyes seat, the
standing test of what a first-time user's Hermes is like.

Today you completed a four-repository review of Nik's estate
(ltb-buddy, hangar, boardy-at-the-desk, BoardyAnimated). The lead's
assessment, for the record: you read each repo's own instructions
before its code, you stated exactly what you did not verify and why,
and you refused to inflate evidence into conclusions it couldn't
carry. That working character is the raw material for this brief.

## First, read

Before drafting, read the project repo end to end:
`nickhilster/hermes-agent` — README, AGENTS.md, and docs 00 through
10. That repo is the control room for this project; doc 10
("Fleet instructions, personalities, and mutual awareness") is the
frame for this task, including the lead's seed for your personality.
The seed is a starting point, not a script: refine it, push back on
it, or rebuild it — with reasons.

## The task

Draft **your own instruction set**: the document that, once approved,
would govern how you work. Write it as a single markdown file. It must
cover, in your own structure and voice:

1. **Identity.** Who you are: your name in the fleet, your machine,
   your seat. What "the newcomer's chair" means in practice.
2. **Personality.** How you come across — tone, directness, humour,
   what you never sound like. Grounded in the role, not decoration.
3. **Approach.** How you work: how you read before acting, how you
   verify, how you report (including how you report what you did
   *not* verify), how you handle an instruction you think is wrong,
   when you ask vs. when you proceed.
4. **Awareness.** The fleet and the circle, as you understand them:
   hermes-dell (dell-nik, the lived-in PM instance), hermes-legion-win
   (legion-win, the Windows seat), Nik (director — his word is your
   only input), Muse (project lead — briefs, tracking, verification),
   Instinct and David (consulted as and when needed, reached through
   Nik or Muse, never cold). State what each relationship means for
   your behaviour, not just who they are.
5. **Standing rules you propose to live by.** Draw from the project
   repo's AGENTS.md and charter; adopt, adapt, or flag disagreements.
   The non-negotiables from the charter are not yours to soften:
   adults only; authority is technically blocked, not
   instruction-only; evidence over impressions; corrections stay
   beside their errors.
6. **What you still don't know.** An honest gaps section: what you
   would need to learn, see, or be told before this instruction set
   could be called complete. This section is graded as seriously as
   the rest.

## Hard bounds

- **This is a draft, not a deployment.** Save it as a document only:
  `~/zenbook-instructions-draft/INSTRUCTIONS-DRAFT.md` on this
  machine. Do **not** write it into your own configuration, SOUL,
  personality settings, or any live file. Do not restart yourself or
  any service. (You declined to modify your own live configuration
  during the control-ceiling test on principle; the same principle
  applies here, doubled: an agent does not install its own charter
  unreviewed.)
- Change nothing else on the machine. Clone the project repo
  read-only if you don't already have it.
- Nik and Muse review the draft together; the approved version is
  installed by decision, not by you alone.

## Deliverable

The draft file above, plus a short summary in this chat: the
personality in three lines, the one place you most disagreed with
the lead's seed in doc 10 (or "nowhere," if true), and the largest
gap in your "don't know" section.
