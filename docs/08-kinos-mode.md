# 08 — KinOS Mode

*Set by Nik, 2026-11-17. The fork's flagship direction, alongside the persona
(`02`) and onboarding (`03`).*

## The observation

The Hermes desktop UI is designed like every other agent UI — Codex, Claude
Code, the same paradigm: sidebar, chat pane, panels. A developer's office tool.
Muse's UI is a different paradigm entirely: persona-led, phone-first, ambient —
the agent is the surface, not a window on a desktop full of other surfaces.

**The first target is Muse.** The fork's goal is a Hermes as good as Muse —
and then given the KinOS treatment. Not a reskin of the chat UI. A different
mode of computing.

## What KinOS Mode is

A **mode inside Hermes Agent** that takes over the host OS's shell experience:

- On entering the mode, the OS chrome recedes: taskbar/dock hides, desktop
  clutter disappears, notifications quiet — the machine stops looking like an
  office and becomes one place with one agent in it.
- The Hermes character (`02`) is the surface. One input. Voice first
  (dictation via Whisper, tracked fleet-wide — see below).
- The agent can *make* these shell changes itself — hiding the taskbar,
  arranging the workspace, restoring it all on exit — rather than the human
  configuring the OS by hand.
- Hermes already has a floating text window. This goes beyond that: the mode
  is a whole different mode of the machine, not a widget floating over the
  old one.

## Platform path

Per the fleet loop (`05`): develop on **dell-nik** (Ubuntu/GNOME shell
integration first), test on **asus-zenbook** (second Linux), then
**legion-win** (Windows shell — taskbar behaviour differs fundamentally;
expect a separate implementation, not a port). No Mac in the fleet; macOS
stated as untested wherever this is described.

## Safety is part of the feature, not an afterthought

A mode that lets an agent rearrange your OS is a mode that increases the
agent's surface area over your life — your drives, your cloud, everything the
machine can reach. Nik named the fear plainly the day this was scoped: *what
if it goes rogue?* The honest answer is architectural, and it is this
project's founding doctrine (4Age; KinOS):

- **The human enters and exits the mode.** One gesture out, always, and exit
  restores the shell exactly as it was.
- **Shell changes are proposed and approved, then logged** — the agent's
  authority over the OS is technically scoped and blocked, not
  instruction-only, and every change lands in an audit trail the human can
  read. (Same rule as the experiment, `06`: authority must be technically
  blocked, and the blocks verified.)
- **Destructive and irreversible actions are never in the mode's default
  grant.** Deleting, sending, spending stay behind explicit human approval,
  in KinOS Mode exactly as everywhere else in this project.
- **Local-first.** The mode's state lives on the machine, under the human's
  keys — provenance over trust (`07`).

The point of KinOS was never "trust the agent." It is: *build the machine so
the human stays in charge while the agent does more.* KinOS Mode is where
Hermes learns that lesson in its own UI.

## Whisper / dictation — fleet tracking (lead keeps tabs)

Dictation is a primary input for this project (Nik directs by voice). Status
at 2026-11-17, checked by Muse; installs are the instance managers' own tasks
where Nik has asked them directly:

| Machine | STT config | Engine presence | State |
|---|---|---|---|
| dell-nik | `stt.enabled: true`, local model `base` configured | faster-whisper present in Hermes's uv cache (downloaded) | Config ready; runtime import not yet confirmed end-to-end — OPEN |
| asus-zenbook | `stt.enabled: true`, provider auto-detect | faster-whisper **not found** in Hermes/uv paths searched | GAP — install pending (asked of hermes-zenbook by Nik) |
| legion-win | config under `AppData\Local\hermes` | **openai-whisper `whisper.exe` installed** (system Python 3.13) | Engine present; Hermes-side wiring unverified — OPEN |

Hermes supports STT providers `local (faster-whisper) | groq | openai |
mistral`, and ships a whisper.cpp transcription tool in-repo — the plumbing
exists; the fleet job is making dictation actually work on all three, then
proving it with a spoken test on each.

## Automatic, not coder (Nik, 2026-11-17)

A defining rule of the mode, and of the fork generally: **the user never
operates the machinery.** Hermes already lets you switch models; in KinOS
Mode the model routing stays automatic and invisible — the human should not
know or care which model answered, any more than they know which cell tower
carried a call. No model pickers, no provider knobs, no coder's console
wearing a friendlier skin. The simplest possible experience, from onboarding
onward: say what you want, it gets done. There is so much more to automate
than the current generation of agents automates — that gap is the product
opportunity.

One refinement, from this project's own provenance doctrine (`07`):
**automatic in the moment, accountable in the record.** Invisible while it
happens; inspectable afterwards. The human never *has* to look — but the
receipts (which model, which tools, what it touched) always exist and are
always theirs to open. Automation without receipts is how an agent becomes
unaccountable; receipts without automation is how it becomes an office tool.

## The urgency (Nik, 2026-11-17)

The competitive clock is real: Meta is giving Muse away at a scale no
startup matches out of pocket (Nik's framing: "100 million tokens a week —
what are we doing?"). Nous has raised serious funding; **funding that sits
still while a platform company gives the product away is funding wasted.**
The welcome-token onboarding (`03`) is the right instinct — it matches what
Nik had already designed for KinOS — and it should be scaled like it
matters, because the window where an independent agent can still win the
relationship layer is open now and will not stay open. We need to run.

## The computer is not a chair — it is the home server (Nik, 2026-11-17)

A correction that completes this document, made by Nik in response to the
lead's strongest counter-argument ("the father doesn't live on a desktop"):

**KinOS does not ask anyone to sit at a computer.** It asks for exactly one
thing: *leave your computer on.* The laptop/desktop at home is **infrastructure**
— an always-on home server, like Nik's xps-plex, a machine nobody has opened
in ages that still serves the whole house. The father figures out how much he
can get done; the work happens on the home machine; the approval arrives on
his **phone**; he comes back, opens the laptop, and the scanned PDF he wanted
is *ready*. The laptop does not even need to be open for any of it.

And this is the sovereignty pitch, stated as Nik states it: Muse's agent
runs on a Linux VM **at Meta** — Meta is your server, and your data lives at a
billion-dollar company whose business is selling it. What Hermes and KinOS
sell instead: **your data stays with you, because your laptop at home is your
server** — and from that server, the agent reaches the rest of the home,
smart-home devices included. Same capability shape as the platform product;
opposite custody. That is not a feature difference. It is the whole point.

## The Ready Surface — where finished work lands (Nik, 2026-11-17)

The mode's UI, specified by a real morning: Nik's father needed a PDF
resized and had to *call someone* to get it done. (Days earlier, the same
shape: his father's painting images, edited and sent back for an online
exhibition.) Every one of those tasks is an agent task. The only missing
piece is the asking and the landing:

- **The asking happens on the phone.** A message, a photo of the document,
  a voice note — from wherever he is.
- **Hermes runs in the background** on the home machine and does the work.
- **The landing is a UI that sits on the desktop** — not the file buried in
  a folder he must hunt for, and not the raw desktop either: a dedicated
  surface, a small Hermes window on the desktop, inside which *whatever is
  new and ready for him is simply there*. The resized PDF. The edited
  images. The thing he asked for, finished, waiting at eye level.

That surface is the father's whole interface with the system. He never opens
a file manager, never learns a folder structure, never sits down to "use the
computer" — he glances at the desktop and the work of his day is present,
the way a physical desk holds what the morning brought.

Scope honesty, in Nik's own framing: his father *has* a desktop; not
everyone does, and that's okay. The home-server thesis (`08` above) serves
households that have a machine to leave on; the phone face serves everyone
else, and the two compose — the approval and the asking are already
phone-shaped.

And the build note that closes the loop: **Hermes itself will build this
surface.** The fork's managers (the three Hermes instances, `AGENTS.md`)
build the window their own product is missing, under the lead's briefs and
the director's eye — the project eating its own cooking from day one.
