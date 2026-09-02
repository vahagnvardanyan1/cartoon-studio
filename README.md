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
| `/voice-production` | Records the narration and dialogue — **before any picture** |
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
6. **Shot planning** — the full shot list with camera, action and staging.
7. **Voice** — narration and dialogue recorded *before* any picture, because
   lip-sync tools are audio-driven and the line sets the shot's length.
8. **Animatic** — the stills cut to the voice, watched as a film. You approve
   the whole thing before a single clip is rendered.
9. **Clip generation** — drafts first, each one cut into the reel as it lands.
10. **Assembly** — music, sound design, grade, titles, and the finished film.

Stages 7 and 8 are the ones most AI pipelines skip, and they are where most of
the wasted effort gets avoided.

## A note on cultural accuracy

If the story uses a word, object or custom Claude does not properly understand,
it will stop and ask you rather than guess. Guessing is how a folk tale quietly
turns into something else.

## Where the hard-won knowledge lives

Two files carry most of it.

`references/editing-and-pace.md` is where to start. It explains, with numbers,
why AI-generated films come out boring: seven shots in sixty seconds is an
8.5-second average shot length, which is 1930s studio pacing, and AI footage is
worse than live action here because viewers begin noticing the machine at six
to eight seconds. It gives shot counts by runtime, the descending shot-length
ladder, the generate-long-cut-short ratios that professionals actually work to,
a coverage budget, and a checklist of the tells that mark a film as generated.

`references/production-lessons.md` records the specific mistakes that ruin
AI-generated animation — lifeless shots, characters who change size or breed
between cuts, props that detach from hands, foreign speech turned to gibberish,
prompts that delete a man's hair because they described an absence instead of a
presence — and exactly how to avoid each one.

Both were written from real productions where every one of those went wrong
first.
