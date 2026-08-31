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

> /start Hovhannes Tumanyan's Armenian tale «Շունն ու Կատուն»

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
| `/clip-generation` | Renders the clips, shot by shot |
| `/film-assembly` | Adds voice, music, titles and delivers the film |

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
6. **Shot planning** — the full shot list with camera, action and dialogue.
7. **Clip generation** — drafts first, then final quality once approved.
8. **Assembly** — voices, music, sound, titles, and the finished film.

## A note on cultural accuracy

If the story uses a word, object or custom Claude does not properly understand,
it will stop and ask you rather than guess. Guessing is how a folk tale quietly
turns into something else.

## Where the hard-won knowledge lives

`references/production-lessons.md` is the important file. It records the
specific mistakes that ruin AI-generated animation — lifeless shots, characters
who change size or breed between cuts, props that detach from hands, foreign
speech turned to gibberish — and exactly how to avoid each one. It was written
from a real production where every one of those went wrong first.
