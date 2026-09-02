---
name: start
description: Start a new animated cartoon production from a story. Use when the user says "/start", "make a cartoon", "animate this story", "produce an animated short", "create a cartoon from this tale", or names a story they want turned into a film. Orchestrates all eight production stages with approval gates.
---

# Start a cartoon production

Run an eight-stage production from a story to a finished animated short. You
are the production lead: you research, plan, generate, inspect your own work,
and stop at every gate for approval.

## Before anything else

Read these in full before generating anything:

- `${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` — the failures that
  ruin AI animation
- `${CLAUDE_PLUGIN_ROOT}/references/video-craft.md` — why consistency is hard
  and what actually holds it
- `${CLAUDE_PLUGIN_ROOT}/references/voice-and-audio.md` — voice, dialogue and
  lip sync
- `${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` — tooling constraints

Confirm the Picsart GenAI tools are available. If they are not, say so plainly
— the production cannot run without them.

## What to ask before you start, and what not to

Ask only what you genuinely cannot proceed without:

- **The story.** Title, text, or a description.
- **The language of the voice track**, because it is the most likely thing to
  break and you will test it first.
- **Any hard constraint** the user already has — a deadline, a credit budget, a
  required format or aspect ratio, a platform it must fit.

**Do not ask how long the film should be.** The user cannot answer that before
either of you knows the story's shape, and neither can you. Runtime is an
*output* of the story breakdown, not an input to it. Research the tale, count
its beats, then **propose a runtime with your reasoning** — what a shorter cut
would lose, what a longer one would add — and let the user choose or override.

If the user volunteers a length unprompted, take it as a constraint and design
to it.

## Set up the production folder

Create a working folder for this film and keep it current throughout:

```
<film-name>/
  canon.md        story beats, continuity rules, season progression,
                  and the IDENTITY STRINGS — see below
  assets.md       every approved reference, with its URL and what it locks
  shots.md        the shot list
  audio.md        every voice line and cue: text, model, voice, seed, URL
```

`assets.md` is the spine of the production. Every approved image goes in it
with a note on what it is the authority for. When a later stage needs a
reference, it reads this file rather than remembering.

**Identity strings.** For each character, write their physical description
**once** in `canon.md` — build, face, colouring, signature clothing, continuity
mark. Every later prompt pastes that block in **byte-identical**. Rewording it
reads to the model as a different character, and is a leading cause of drift.
Only the scene instructions change between prompts.

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
| 7 | **Voice** | `voice-production` | Voice track approved |
| 8 | **Animatic** | `animatic` | **The whole film approved as a reel** |
| 9 | Clip generation | `clip-generation` | **Every clip approved, in the reel** |
| 10 | Assembly | `film-assembly` | Final film approved |

**Stages 7 and 8 are where most of the pain gets avoided.** Voice comes before
picture because lip-sync tools are audio-driven and the recorded line sets the
shot's length. The animatic comes before motion because you cannot judge a film
shot by shot — a problem of perception, not of cost.

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

**State what you cannot see.** If you have not inspected an image or clip
yourself, say so plainly rather than describing it with borrowed confidence.
Undeclared blindness is how a wrong character size, a missing hand or a season
error survives ten more shots before anyone notices.

**Review in the reel, not alone.** From the animatic onward, every approved
clip replaces its still in the story reel, and every review watches the film as
it currently stands.

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

---

## Research before anything, and research wide

For a story with any cultural specificity, run **three parallel research
agents** before writing a single prompt. This was the difference between the
first film and the second.

1. **The primary text.** Full original-language text verbatim, a line-by-line
   gloss, the exact chain of events, every character and occupation, the
   closing lines, and the verse form. Tell the agent explicitly not to fill
   gaps from similar tales — international variants of a folk motif will
   contaminate the research if you let them.
2. **The visual world.** Architecture, dress, tools, animals, landscape,
   season, and any existing adaptations. Demand citations and demand that the
   agent mark clearly where it is inferring rather than citing.
3. **The craft.** Current editing practice, generation ratios, model-specific
   prompt syntax and failure modes.

Two things this caught on *Drop of Honey* that would otherwise have shipped as
errors: the customer is a **shepherd with a bludgeon**, not a hunter with a
staff — which changes the first shot's silhouette and the murder weapon — and
the honey is **not** stored in a կարաս, which is a half-buried wine jar the
size of a person.

Ask the researchers for the **verse form** as well as the content. The metre of
*Drop of Honey* drops from eight-syllable lines to four-syllable lines at
exactly the points where the violence accelerates. The poet had already
storyboarded the edit; the shot list just had to follow him.
