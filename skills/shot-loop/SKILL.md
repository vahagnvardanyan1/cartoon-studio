---
name: shot-loop
description: Build a film one shot at a time — for each shot in story order, make what it needs, generate its keyframe and clip, cut it with its own audio, and get it approved before starting the next. Use after the animatic is approved, or when the user says "/shot-loop", "next shot", "go to the next video", "one at a time", "let's do shot 3".
---

# The shot loop

The film is built **one shot at a time, in story order.** You finish a shot
completely — including its sound — show the user that piece of film, and only
then start the next.

This replaces generating all the keyframes, then all the clips, then the mix.
That order looks efficient and is not: a fault in the first shot's costume,
screen direction or season is invisible until assembly, by which point it is in
twenty shots.

## Before the loop starts

The shared canon must already be locked and approved: style key, character
sheets, scale sheet, location plates, hero props, shot list, every voice line,
and the animatic. If any of those is still open, stop — you are in Phase A and
the loop will just spread the uncertainty.

Read `assets.md` and `canon.md` at the top of every shot. Do not work from
memory; identity strings are pasted byte-identical from the file.

## One turn of the loop

### 1. Read the shot

From `shots.md`: what happens, who is in it, its planned length, its camera
move, which voice cue lands on it, and which references it wires in.

**Check it against two rules before generating anything:**

- **Does more than one character speak in this shot?** If so the shot is wrong
  — lip-sync takes one portrait at a time and the video model will not move
  mouths on its own. Break it into singles now, before generating. See
  `clip-generation`.
- **Does it carry a face for more than six seconds?** Then it is too long. Split
  it or trim the plan.

### 2. Make only what this shot needs

Anything shared was made in Phase A. Here you make the shot-specific things and
nothing else: a keyframe, an end frame if the shot has a camera move, and
occasionally one prop or one insert plate that appears nowhere else.

Wire in the references named in the shot list — the plate, the character
sheets, the scale sheet for any two-hander. Restate the location geometry and
the screen direction in the prompt text; the model has no memory of either.

**Inspect the keyframe before using it.** Contact-sheet it and look. Check it
against the canon: costume, hair, season, light direction, screen direction,
no text in frame.

### 3. Generate the clip

Generated **longer than the cut needs** — a 2.5-second shot is still generated
at 6–8 seconds, because there is no way to extend later and there is always a
better two seconds inside a longer take.

Audio decision, made per shot:

- **No dialogue** → `generateAudio: true`, with the sound described explicitly
  in its own block in the prompt, including what must *not* be there.
- **Dialogue, one speaker on screen** → lip-sync model, real recorded audio.
- **Dialogue, nobody's face visible** → silent clip, voice laid in at step 4.

### 4. Cut the segment — with its sound

**This is the step that makes the loop worth running.** Assemble the shot into
a rendered segment: trimmed to its planned length, with its voice line, its
effects and the score at the right level.

If a spoken line spans this shot and the next, the segment is **both shots**.
Never cut a sentence in half at a shot boundary — the user will hear a broken
mix and review the wrong thing.

### 5. Show it and stop

Give the user the rendered segment and **say what to check** — the two or three
things most likely to be wrong in this specific shot, not a general request for
thoughts. Name anything you already know is imperfect before they find it.

Then stop. Do not start the next shot.

### 6. On approval

Append the segment to the running cut, update `shots.md` with the approved
URLs, and begin the next shot.

## When a shot fails

**Diagnose before regenerating.** Ask which layer the fault lives in:

| Fault | Layer | Fix |
|---|---|---|
| Costume, face, proportion wrong | the character sheet | rebuild the sheet, then every shot that used it |
| Geometry, season, light wrong | the plate | rebuild the plate |
| Pose, action, framing wrong | the keyframe | rebuild the keyframe only |
| Motion wrong, frames fine | the clip prompt | re-run the clip |
| Words wrong | the recording | re-record, then re-sync |

A fault two layers up will come back in the next shot and the one after. If the
same detail is wrong twice, **stop generating shots and go look at the
reference** — that is where it lives.

## Keep the loop honest

- **Never generate the next shot before this one is approved.**
- **Never show a silent clip** as a review unit.
- **Never batch**, however tempting it is when clips take minutes each. Use the
  waiting time to check the previous segment against the canon, not to fire the
  next three.
- **Report drift you can see yourself** before the user does.
