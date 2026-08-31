---
name: animatic
description: Build a story reel from approved keyframes and the recorded voice, and watch the whole film before generating any clips. Use after voices are recorded, or when the user says "/animatic", "make the story reel", "cut the animatic", "let's see the whole thing first".
---

# Build the animatic

Cut the approved keyframe stills to the recorded voice and watch the film end
to end **before spending anything on motion**.

## Why this exists

In live action a script is a fair proxy for the film — actors and locations
fill in the rest. In animation everything on screen is manufactured, so there
is no cheap way to discover whether the film works. The animatic is **the only
full-film simulation available before the expensive stage**, and it is built
from the cheapest material you have: stills you already generated and a voice
track you already recorded.

It answers questions nothing upstream can: how long the film really is, whether
it has a rhythm, whether a beat lands, whether the whole thing is boring.

Note this argument does not depend on regeneration being expensive. It depends
on the fact that **you cannot judge a film shot by shot** — which is about how
people watch, not about production cost.

## Build it

1. **Generate the start keyframe for every shot** if not already done. These
   are the stills the clips will be animated from anyway, so this is not
   throwaway work — it is the same work, done earlier.
2. **Hold each still for its shot's duration**, which for speaking shots is the
   length of the recorded line.
3. **Lay the voice track underneath** at its timecodes.
4. Add a temporary music bed if one exists.
5. Render it as one continuous film.

Use the compositor's montage recipe with the stills as clips.

## Watch it, and say what you see

Sample frames across the whole timeline and inspect them. Then report honestly:

- **Runtime** against target
- **Pacing** — which stretches drag, which beats are rushed
- **Clarity** — does the story read from picture and voice alone
- **Coverage** — any beat that has no shot, any shot that earns nothing
- **Continuity** — season, time of day, screen direction across the cuts

Recommend cuts. A shot that is not carrying its length in the animatic will not
carry it once animated — it will just cost more.

## Gate

The user approves the animatic **as a film** before clip generation begins.
Changes made here cost one still each. The same change after rendering costs a
clip, and after assembly costs the edit.

## Keep it alive

Do not discard it. As each clip is approved it **replaces its still in the
reel**, so the reel evolves from all-stills to all-motion and always represents
the current state of the film. Every subsequent review watches the film as it
stands, not a clip in isolation.
