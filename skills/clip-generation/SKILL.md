---
name: clip-generation
description: Generate the video clips for an animated production, shot by shot, with keyframes, quality selection and an approval gate on every clip. Use when the shot list is approved, or when the user says "/clip-generation", "generate the clips", "render the shots", "start the video".
---

# Generate the clips

Render the film shot by shot. Each clip is generated from approved reference
art, inspected by you, then approved by the user before the next begins.

Read `${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` and
`${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` first.

## Ask about quality first

Before rendering anything, ask the user how they want to work, using
AskUserQuestion so they can just click:

**Draft quality** — offer low resolution for review with a full-resolution
re-render after approval (cheapest, and the draft predicts the final because
it is the same model), or full resolution straight away (fewer steps, roughly
four times the cost per attempt).

**Variants** — offer one take per shot, or two takes to choose between.
Selection does more for quality than any prompt tweak. Recommend two for
character shots.

**Final resolution** — offer the resolutions the chosen model actually
supports; check the catalog rather than assuming.

Preflight the total and tell the user the cost before starting.

## Every shot is built the same way

**1. Generate a start keyframe** with the image model, from the approved
references. This is what holds identity — video models reinvent characters
given only text.

The keyframe must show **the exact state the first beat begins from**. If beat
one is a downswing, the keyframe has the tool raised in both hands. A keyframe
showing the aftermath makes the action impossible to animate.

**2. For silent shots, generate an end keyframe too.** Same scene, same
lighting, stating only what has changed, with the final framing pinned. Passing
both frames is the only reliable way to stop a push-in running away into a
cropped close-up.

**3. Render the clip.** Submit asynchronously and poll. Use timed beats, one
camera move, the size lock, the hands reminder and the AVOID list.

**4. Inspect it yourself.** Sample frames through the media tooling and look at
them. Check: the continuity mark, the hands, the relative scale, the season,
the prop marking, and the final framing. Never present a clip you have not
looked at.

**5. Present it** with what you found — including what is wrong. Then stop and
wait.

## Speaking shots take a different path

A general video model **re-synthesises** any audio you give it, turning
dialogue into convincing-sounding nonsense. This is catastrophic for a
non-English film and is not fixable by prompting.

For shots where a character speaks:

- Generate the line with the approved voice model first
- Use a **dedicated lip-sync model** (portrait plus audio) — these play the
  real file and sync the mouth to it
- Name who speaks and state that everyone else keeps their mouth closed
- **Check the output for burned-in captions** — some avatar models hard-code
  garbled subtitle overlays into the picture
- Let the **audio length set the shot length**

For everything else, render silent and lay the voice over it in assembly.
Approximate sync with correct language beats perfect sync with gibberish.

## Continuity across clips

Where two shots are continuous, use the previous clip's last frame as the next
clip's start frame.

Watch for drift as you go: a character's build, a colour, a hat that appears
where it should not. If drift appears twice, the reference is at fault, not the
prompt — go back and fix the sheet, and be honest that shots already rendered
will need redoing.

## Approval

One clip, one review, one approval, then the next. Never batch. On rejection,
diagnose the actual cause before regenerating — inspect the frames and name
what went wrong rather than rerolling and hoping.

Record every approved clip URL, with its duration, in `shots.md`.
