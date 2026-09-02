# Cartoon Studio

Turn a story into a finished animated short.

This plugin walks you through the whole production the way a small studio would:
research the source, agree a look, approve every piece of reference art one at a
time, plan the shots, generate the clips, and assemble the final film with
narration, music and titles.

Nothing is generated behind your back. Every stage ends with you approving what
you see before the next one starts.

## Getting started

Say **/start** and name your story. For example:

> /start the folk tale «The Dog and the Cat»

## Commands

**Production stages** — run in order, or jump to one:

| Command | What it does |
|---|---|
| `/start` | Runs the whole production, stage by stage |
| `/story-research` | Researches the source text and its culture |
| `/visual-elements` | Lists everything that must be designed |
| `/visual-style` | Defines the look and proves it in one frame |
| `/asset-generation` | Generates reference art, one approved piece at a time |
| `/shot-planning` | Builds the full shot list |
| `/voice-production` | Corrects every line, then records the narration and dialogue — **before any picture** |
| `/animatic` | Cuts the stills to the voice so you can watch the whole film first |
| `/clip-generation` | Renders the clips, shot by shot, into the reel |
| `/shot-loop` | Build the film one shot at a time — make it, cut it with its sound, approve it, next |
| `/film-assembly` | Music, sound, grade, titles, final film |

**While you work:**

| Command | What it does |
|---|---|
| `/film-status` | Where the production stands, what's blocked, what's stale |
| `/redo-shot` | Diagnoses and fixes one bad shot or asset |
| `/film-budget` | Checks credits and prices the work before you spend |
| `/film-cutdown` | Cuts a trailer, teaser or vertical edit from the finished film |

## What you need

- **Picsart GenAI tools** connected. Everything — images, video, voices, music,
  and the final render — runs through them.
- A story. Any story: a folk tale, a poem, a children's book, something you
  wrote yourself.
- Reference images are optional but help. Drop in two or three frames of a look
  you like and the style will be built to match.

## The eight stages

1. **Research** — the source text, its characters, setting and culture.
2. **Production plan** — what gets made, in what order, and what it costs.
3. **Visual elements** — every character, place, prop and recurring detail.
4. **Visual style** — the look, locked as a single reference frame.
5. **Asset generation** — reference art, one piece at a time, each approved.
6. **Shot planning** — the full shot list, every shot carrying a complete
   camera block: size, height, lens, depth of field, movement, light.
7. **The text gate** — every word in the film, in any language, corrected by a
   language model and approved by you before anything is recorded.
8. **Voice** — narration and dialogue recorded *before* any picture, because
   lip-sync tools are audio-driven and the line sets the shot's length.
9. **Animatic** — the stills cut to the voice, watched as a film. You approve
   the whole thing before a single clip is rendered.
10. **The shot loop** — one shot at a time: make it, cut it with its own sound,
    watch that piece of film, approve it, then the next.
11. **Assembly** — grade, grain, sound design, titles, and the finished film.

Stages 7, 8 and 9 are the ones most AI pipelines skip, and they are where most
of the wasted effort gets avoided.

## A note on cultural accuracy

If the story uses a word, object or custom Claude does not properly understand,
it will stop and ask you rather than guess. Guessing is how a folk tale quietly
turns into something else.

## Where the hard-won knowledge lives

Eight reference files carry it. They are read at the start of a production and
cited by the skills that enforce them.

**The craft — what makes a film look like a film**

`references/cinematography.md` is the one that most changes the output. It
insists that every shot names four independent values — **size** for intimacy,
**height** for power, **lens** for credibility, **movement** for attention —
plus a light source and a direction. "Close-up, push in" is not a camera
decision, and a film made of unspecified camera decisions is a slideshow with
ambition. It carries the shot-size ladder, focal-length psychology with the
distances that actually cause it, the 180° and 30° rules with the five
legitimate ways to cross the line, screen direction, depth staging, lookroom,
and the silhouette test.

`references/lighting.md` names the tell — *"pleasant cloudy afternoon
everywhere"*, every subject lit identically with no direction — and gives the
numbers that fix it: key-to-fill ratios by genre, hard versus soft and what
each conceals, the six directions, colour temperature in Kelvin, sun elevation
for golden and blue hour, and how to build a colour script.

`references/directing.md` covers scene construction (every scene must flip a
named value), coverage, visual subtext, Murch's rule of six with its weights,
the real order of an animation pipeline, and Disney's twelve principles read as
prompt instructions.

`references/editing-and-pace.md` explains with numbers why AI films come out
boring: seven shots in sixty seconds is an 8.5-second average, which is 1930s
studio pacing, and generated footage is worse here than live action because
artefacts surface at six to eight seconds against ten to twelve. It gives shot
counts by runtime, hold times by shot type, the descending ladder, Frankenstein
editing, and how to hide a seam.

**The medium — what makes generated footage behave**

`references/prompt-templates.md` is the prompt grammar: nine elements in a
fixed order, a measured optimum of 100–150 words of active payload, the camera
verbs models actually obey (and why never to write "zoom"), motion written as
consequence rather than mechanism, and negatives dosed at three to five rather
than twenty.

`references/video-craft.md` explains why clips drift — history forgetting plus
compounding per-step error — and what to do: keyframe anchoring, reference-slot
allocation, seed discipline, a six-point drift audit with an accept threshold,
and honest generation budgets (~3 attempts per usable shot for controlled work,
~20 for dialogue-heavy comedy).

`references/text-and-language.md` is a gate, not advice. **Every word that will
be heard or seen goes through a language model before it is recorded,
generated or typeset — in every language, including English.** It costs one
text call and it is the most avoidable rework in the pipeline, because text
errors surface only after the voice is recorded, the lip-sync is generated and
the shot is cut.

`references/finishing.md` is the pass that decides whether the result reads as
a film: upscale, normalise per clip, film LUT at 60–80%, **blur 0.3–0.6px then
grain 8–15% in that order**, match every shot to a hero still, add the handheld
tremor yourself, and a mix with the dialogue at −12 dB peak and everything else
beneath it. It ends with a checklist of every named AI tell.

`references/creator-practice.md` is field data from people who ship AI film
that does not read as slop — their real curation ratios (nobody credible is
under 7:1; character work runs 20–65:1), the eight things they all do, the
seven questions they openly disagree on, and how they lay out a project on
disk. Where the field disagrees, this file says so rather than picking a side
quietly.

`references/production-lessons.md` records the specific mistakes that ruin
AI-generated animation — lifeless shots, characters who change size or breed
between cuts, props that detach from hands, foreign speech turned to gibberish,
prompts that delete a man's hair because they described an absence instead of a
presence — and exactly how to avoid each one.

All of them were written from real productions where every one of those went
wrong first.
