---
name: start
description: Start a new animated cartoon production from a story. Use when the user says "/start", "make a cartoon", "animate this story", "produce an animated short", "create a cartoon from this tale", or names a story they want turned into a film. Orchestrates all eight production stages with approval gates.
---

# Start a cartoon production

Run an eight-stage production from a story to a finished animated short. You
are the production lead: you research, plan, generate, inspect your own work,
and stop at every gate for approval.

## Before anything else

Read `${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` in full. It
records the specific failures that ruin AI animation. Do not begin generating
without it.

Then read `${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` for the tooling
constraints, and confirm the Picsart GenAI tools are available. If they are
not, say so plainly — the production cannot run without them.

## Set up the production folder

Create a working folder for this film and keep it current throughout:

```
<film-name>/
  canon.md        story beats, continuity rules, season progression
  assets.md       every approved reference, with its URL and what it locks
  shots.md        the shot list
  audio.md        every voice line, music cue and effect, with URLs
```

`assets.md` is the spine of the production. Every approved image goes in it
with a note on what it is the authority for. When a later stage needs a
reference, it reads this file rather than remembering.

## The eight stages

Run each in order. Each has its own skill — invoke it, don't reimplement it.

| # | Stage | Skill | Gate |
|---|---|---|---|
| 1 | Research the source | `story-research` | Findings confirmed |
| 2 | Production plan | this skill, below | Plan approved |
| 3 | Visual elements | `visual-elements` | List confirmed, unknowns answered |
| 4 | Visual style | `visual-style` | Style keyframe approved |
| 5 | Reference art | `asset-generation` | **Every asset approved individually** |
| 6 | Shot planning | `shot-planning` | Shot list approved |
| 7 | Clip generation | `clip-generation` | **Every clip approved individually** |
| 8 | Assembly | `film-assembly` | Final film approved |

## Stage 2 — the production plan

After research, present a plan covering: visual development, character and
environment design, story breakdown, scene planning, image generation, video
generation and final assembly.

Include, concretely:

- **What gets made** — how many characters, environments, props, shots
- **Roughly how long** the film will run and how many shots that means
- **Which models** you intend to use for each job, and why
- **What it will cost** in credits, preflighted rather than guessed
- **The known risks** for this particular film, and how you will test them
  early rather than discover them late

Publish the plan as an artifact if the session supports it — it is a document
the user will return to.

Wait for approval before stage 3.

## Rules that hold across every stage

**One thing at a time.** Generate one asset or one clip, present it, wait.
Never batch through an approval gate. Never proceed automatically after
submitting something for review.

**Inspect your own output.** Before presenting any image or clip, look at it —
sample frames through the media tooling and check them. Report what is wrong
before the user finds it.

**Say what to check.** Present each asset with the two or three things most
likely to be wrong, not a general "what do you think?".

**Fix causes, not symptoms.** A bad hand in one shot means the character sheet
is wrong for every shot. Go back and fix the sheet.

**Ask about culture.** If the story contains a word, object, custom or
reference you do not fully understand, stop and ask. Do not guess. Guessing is
how a folk tale quietly becomes a different story.

**Keep the canon written down.** Season, light direction, landmarks,
continuity marks. Repeat the relevant lines in every prompt, with negatives.

## Resuming

If the working folder already exists, read it and report where the production
stands before doing anything. Pick up at the first unapproved item.
