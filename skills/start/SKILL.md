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

**The craft** — what makes a film look like a film:

- `${CLAUDE_PLUGIN_ROOT}/references/cinematography.md` — the four camera axes,
  lens language, blocking, screen grammar
- `${CLAUDE_PLUGIN_ROOT}/references/lighting.md` — sources, ratios, colour
  temperature, the colour script
- `${CLAUDE_PLUGIN_ROOT}/references/directing.md` — scene construction,
  coverage, the animation pipeline, Murch's rule of six
- `${CLAUDE_PLUGIN_ROOT}/references/editing-and-pace.md` — shot counts, hold
  times, hiding the seams

**The medium** — what makes generated footage behave:

- `${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md` — the prompt grammar
- `${CLAUDE_PLUGIN_ROOT}/references/video-craft.md` — drift, consistency,
  generation budgets
- `${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` — the failures that
  ruin AI animation
- `${CLAUDE_PLUGIN_ROOT}/references/text-and-language.md` — the text gate
- `${CLAUDE_PLUGIN_ROOT}/references/voice-and-audio.md` — voice, dialogue and
  lip sync
- `${CLAUDE_PLUGIN_ROOT}/references/finishing.md` — grade, grain, mix, the
  finishing checklist
- `${CLAUDE_PLUGIN_ROOT}/references/creator-practice.md` — what people
  shipping real work actually do, the true curation ratios, and where they
  disagree with each other
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
  canon.md        story beats, continuity rules, season progression, the axis
                  of action and light direction per location, and the
                  IDENTITY STRINGS — see below
  script.md       every word in the film, corrected and approved, plus casting
  assets.md       every approved reference, with its URL and what it locks
  shots.md        the shot list, with a full camera block per shot
  audio.md        every take: text, model, voice, seed, stability, URL
```

**Name every asset so it sorts and survives being seen out of context:**

```
S01-SH02-Keyframe-V1-Review
S01-SH02-Video-V3-Approved
S03-SH01-FinalFrame-Reference
```

`Scene – Shot – AssetType – Version – Status`. Keep reusable references —
characters, locations, props — **centralised and linked, never duplicated per
shot**; a duplicated reference is a reference that will drift.

**Never overwrite a source before approval.** Keep the original and the
revision together with version numbers, and **record why a take was selected**.
That note is what lets a later reviewer — including you, next session — trust
the choice.

**Track derivation:** for every asset, which text, image or clip produced it.
**Log the seed every time.** Without it you cannot match a regenerated line or
shot after a picture change, and matching is exactly what you will need.

**Treat the canon as read-only once references are locked.** Editing it
mid-production silently invalidates everything generated before the edit. If it
must change, say which approved assets are now stale.

`assets.md` is the spine of the production. Every approved image goes in it
with a note on what it is the authority for. When a later stage needs a
reference, it reads this file rather than remembering.

**Identity strings.** For each character, write their physical description
**once** in `canon.md` — build, face, colouring, signature clothing, continuity
mark. Every later prompt pastes that block in **byte-identical**. Rewording it
reads to the model as a different character, and is a leading cause of drift.
Only the scene instructions change between prompts.

## Two phases, not one long pipeline

The production runs in two shapes, and confusing them is how films come out
inconsistent or come out late.

### Phase A — the foundations, built once for the whole film

These are **shared**. Every shot inherits them, so they must be locked before
any shot exists. Doing them per-shot guarantees the film will not match itself.

| # | Stage | Skill | Gate |
|---|---|---|---|
| 1 | Research the source | `story-research` | Findings confirmed |
| 2 | Production plan | this skill, below | Plan approved |
| 3 | Visual elements | `visual-elements` | List confirmed, unknowns answered |
| 4 | Visual style | `visual-style` | Style key approved |
| 5 | Shared reference art | `asset-generation` | **Every asset approved individually** |
| 6 | Shot planning | `shot-planning` | Shot list approved, every shot carrying a full camera block |
| 7 | **The text gate** | `voice-production` | **Every word corrected and approved — see below** |
| 8 | Voice | `voice-production` | Every line approved |
| 9 | Animatic | `animatic` | **The whole film approved as a reel** |

Stage 5 covers only what more than one shot needs: the style key, the character
sheets, the scale sheet, the location plates, the hero props. **Anything only
one shot needs is not made here** — it is made inside that shot's turn in
Phase B, where you can see what the shot actually requires.

Stages 7 and 8 are where most of the pain gets avoided. Voice comes before
picture because lip-sync tools are audio-driven and the recorded line sets the
shot's length. The animatic comes before motion because you cannot judge a film
shot by shot — a problem of perception, not of cost.

### Phase B — the shot loop, one shot at a time, in story order

| Stage | Skill | Gate |
|---|---|---|
| 10 | **The shot loop** | `shot-loop` | **Each segment approved before the next starts** |
| 11 | Final assembly | `film-assembly` | Final film approved |

Phase B is a **loop, not a batch.** For each shot in turn: make whatever that
shot alone needs, generate its keyframe, generate its clip, cut it together
with its own voice and score, show the user *that piece of film*, and only then
move to the next shot.

**Never generate ahead of the gate.** Batching a beat's worth of clips before
the first one is approved is how a wrong hat, a wrong screen direction or a
wrong season propagates through four shots before anyone looks. It happened;
it cost a day.

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
submitting something for review. When you reach a gate, **end your turn** —
do not ask a question and keep working underneath it.

**Put the gate at the cheap/expensive boundary, and say that is where it is.**
Explore wide and cheap, stop, let the user pick, then commit expensively on the
one they picked. A gate placed after the expensive call is not a gate.

**Enumerate the choices when you stop.** "Which of these four?" with the four
named beats "what do you think?" — the user should be able to answer with one
word.

**Set a per-call cost ceiling and honour it inside the loop.** Agree a number
with the user at the plan stage — the cost of a single generation above which
you stop and ask rather than proceeding. A budget estimated up front is not the
same as a gate that fires on the one expensive call in the middle of a run.

**Never pad to hit a number.** If the story yields eleven beats and the plan
said twelve, deliver eleven and say so. If a search returns three usable
references and you asked for five, return three. Padding is how weak material
ends up being the thing people judge the film on.

**Inspect your own output.** Before presenting any image or clip, look at it —
sample frames through the media tooling and check them. Report what is wrong
before the user finds it.

**Say what to check.** Present each asset with the two or three things most
likely to be wrong, not a general "what do you think?".

**State what you cannot see.** If you have not inspected an image or clip
yourself, say so plainly rather than describing it with borrowed confidence.
Undeclared blindness is how a wrong character size, a missing hand or a season
error survives ten more shots before anyone notices.

**Review the mix, never a bare clip.** A silent clip cannot be judged — the
user has no way to tell whether the film works from picture alone, and will
approve things that fall apart the moment the voice goes on. Every review is a
rendered segment with its dialogue, narration, effects and score already in it.

**Review in narration units.** If one spoken line runs across two shots, those
two shots are a single reviewable unit. Cutting a sentence in half to fit a
shot boundary makes the segment sound broken and the user will flag the mix
rather than the shot.

**Keep a running cut.** Each approved segment is appended to the film so far,
and the user can watch everything up to now at any point. That is what catches
drift between beats — a thing no single segment can show.

**Budget the real curation ratio.** Character-driven narrative work runs
**20–65 generations per usable shot**; nobody shipping credible work is under
about 7:1. A production planned at three attempts per shot runs out of credits
around shot nine. Tell the user the real number at the plan stage —
`creator-practice.md` §1 has the evidence.

**Every word goes through the text gate — in every language, including
English.** Nothing is recorded, generated or typeset until the lines have been
through a language model and the user has approved the result. See
`${CLAUDE_PLUGIN_ROOT}/references/text-and-language.md`. This costs one text
call and it is the single most avoidable source of rework in the pipeline,
because text errors surface only after the voice is recorded, the lip-sync is
generated and the shot is cut.

**Specify all four camera axes on every shot.** Size, height, lens, movement —
plus the light source and its direction. "Close-up, push in" is not a camera
decision and it is the reason generated films look like slideshows. See
`${CLAUDE_PLUGIN_ROOT}/references/cinematography.md`.

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

Two things this caught on one production that would otherwise have shipped as
errors: the visitor turned out to be **a herdsman carrying a bludgeon**, not a
hunter with a staff — which changed the first shot's silhouette and the murder
weapon — and
the commodity being sold is **not** kept in the vessel everyone assumes, which
turned out to be a half-buried wine jar the size of a person.

Ask the researchers for the **verse form** as well as the content. The metre of
one production drops from eight-syllable lines to four-syllable lines at
exactly the points where the violence accelerates. The poet had already
storyboarded the edit; the shot list just had to follow him.
