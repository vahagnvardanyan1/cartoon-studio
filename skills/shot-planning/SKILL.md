---
name: shot-planning
description: Break a story into a full shot list for animation, with camera, action, dialogue, sound, duration and generation prompts for every shot. Use when reference art is approved, or when the user says "/shot-planning", "plan the shots", "make the shot list", "break this into scenes".
---

# Plan the shots

Turn the story beats into a complete shot list. This document is what the whole
generation stage executes, so it needs to be right before a single clip is
rendered.

Read `canon.md` and `assets.md` first.

## Structure the film

Group shots into acts that follow the story's own shape. Give the turn and the
ending room; compress the setup. A three-minute film is roughly 20–24 shots at
6–12 seconds each.

Use repetition deliberately where the story repeats: an identical framing
returned to with only the weather and a character's posture changed is the
cheapest and strongest way to show time passing.

## Every shot needs

- **Number and title**
- **Plot** — what happens, one or two sentences
- **Cast** — who appears
- **Location and time of day** — naming the approved environment plate
- **Action and emotion** — as observable movement, not adjectives
- **Camera** — angle and one movement, with an explicit end framing
- **Dialogue or narration** — in the film's language, with a translation
- **Sound** — effects and atmosphere, and what the score is doing
- **Duration**
- **Reference assets** — which approved images this shot is built from
- **Generation prompt** — written to the template, with timed beats

## Write the prompts properly

Follow `${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md`. Every shot
prompt carries timed beats, one camera move, the size lock, the hands
reminder, the film-look block and an AVOID list.

Note for each shot whether it is **speaking** or **silent** — they take
different generation paths, and the count of each determines the budget.

## Continuity rules

Restate at the top of the list, and then enforce in every prompt:

- The season and light progression, and that it only moves one direction
- Each character's continuity mark
- Each hero prop's marking
- The landmark that anchors wide shots, and on which side
- Anything that must never appear (a hat on a bare-headed character, snow in
  autumn)

## Be honest about additions

If you invent a beat the source does not contain — a moment of proof, a
reaction shot, a visual gag — **say so explicitly** and explain what it buys
and what it costs in fidelity. Let the user decide whether to keep it.

## Output

Write `shots.md`, and publish it as an artifact if the session supports it —
it is a reference document the user will return to throughout generation.

Present it and get approval before rendering anything.
