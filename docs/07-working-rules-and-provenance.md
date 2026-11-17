# 07 — Working rules and provenance

*How this project is run. These rules come from Nik's standing instructions and
from mistakes already made and corrected; the corrections stay beside the
errors.*

## Provenance

- **Receipts over reassurance.** A claim about live state is made only after
  checking the live state: the served page, the running process, the file's
  hash, the build's install stamp. "It should be fine" is not a status.
- **An agent's report is evidence of what the agent reported** — not, by
  itself, of what happened. Verify delegated work against the primary artifact
  before relaying it. (This seed was verified that way: every machine fact in
  `04`/`05` was re-read from the machine after the subagent reported it.)
- **Corrections beside errors.** When something here turns out wrong, append
  the correction with its date; do not silently rewrite history. Three live
  examples from the day this repo was seeded:
  - The companion premise ("Nous has NO mobile app at all") was corrected the
    same day: no GA app, but an official beta + waitlist exists (`03`).
  - asus-zenbook's install was first recorded "complete and verified" by CLI
    checks while its desktop had never been built; the correction and the fix
    are both on record (`05`).
  - The legion-win CLI fault was first diagnosed as a missing Python path; the
    refined root cause (a broken junction to a healthy Python) replaced it —
    with the original diagnosis kept visible in the repair report (`05`).
- **Inference is labelled.** A grounded inference is owned as an inference; a
  stated fact is cited to its source. Self-reported claims from third parties
  start as presumed puffery until a primary source corroborates them.

## Authority and spend

- **No push without Nik's literal word** — a push can trigger paid deployments
  (the Cost-Control Gate). Before any billable action: name the trigger, the
  affected projects, the estimated cost (unknown stays unknown, never zero),
  the cheaper alternative, the rollback path, and the stop condition.
- **Sends and submits are Nik's.** Outbound email/applications go only on his
  literal "send". Drafts are shown verbatim first.
- **Visual acceptance is Nik's.** Agents build and verify mechanically; Nik's
  eyes close the loop on anything visual.
- **Helper windows on Nik's machines are always hidden**; only the deliverable
  app itself may appear. Elevation on his machines is `pkexec`, never `sudo`.

## Communication

- Name the machine, always (`05`).
- Dictation is thinking, not copy: charged lines from Nik's dictation are
  angles to render through the public-voice filter, never text to transcribe
  into anything outbound.
- Research can be uncompromising; public-facing communication stays welcoming.
- Every factual claim in a document leaving the circle carries a source its
  reader can open and check.
