---
name: clip-generation
description: Generate the video clips for an animated production, shot by shot, with keyframes, quality selection and an approval gate on every clip. Use when the shot list is approved, or when the user says "/clip-generation", "generate the clips", "render the shots", "start the video".
---

# Generate the clips

Render the film shot by shot. Each clip is generated from approved reference
art, inspected by you, then approved by the user before the next begins.

Read `${CLAUDE_PLUGIN_ROOT}/references/video-craft.md`,
`${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` and
`${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` first.

By this point the voice is recorded and the animatic is approved. Each clip
replaces its still in the reel as it lands.

## Ask about quality first

Before rendering anything, ask the user how they want to work, using
AskUserQuestion so they can just click:

**Draft quality** — offer low resolution for review with a full-resolution
re-render after approval (cheapest, and the draft predicts the final because
it is the same model), or full resolution straight away (fewer steps, roughly
four times the cost per attempt).

**Variants** — offer one take per shot, or two takes to choose between.
Selection does more for quality than any prompt tweak; generating wide and
letting a human cut is the craft, not a fallback. Recommend two for character
shots. Budget the aggregate across the film, not the per-shot number — complex
multi-character staging can consume many times what a landscape does.

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

**3. Render the clip.** Submit asynchronously and poll.

Structure every prompt as **state, then instruction**:

- **State** — paste the identity string from `canon.md` byte-identical; declare
  what each character is wearing and holding, the continuity from the previous
  shot, and the geometric staging. Be as verbose as needed; the model has no
  memory of anything.
- **Instruction** — the active creative payload, roughly 60 to 100 words,
  front-loaded. Adherence decays by position: a prompt carrying eight
  requirements honours four or five at random. Timed beats, one camera move.
- **Prohibitions** — but check first whether the model has a **dedicated
  negative field**. If it does not, a bare keyword list can be rendered *as
  subject matter* — asking for "no snow" produces snow. Without a negative
  field, use grammatical prohibition or, better, describe the positive state.

Other rules that hold: give **every reference an explicit job** or it bleeds
its lighting and pacing into the shot; keep **reference strength below maximum**
or characters go stiff and cannot adapt to new light; **cap clip length**,
since drift scales with duration; and **hold lighting colour temperature
constant** across a sequence, because lighting affects how the model
reconstructs a face.

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

For shots where a character speaks, the voice already exists from stage 7.

- Use a **dedicated lip-sync model**. Unlike general video models, these play
  the supplied file unaltered and sync the mouth to it.
- **Check that the model documents support for your character type.** Many
  lip-sync tools depend on a human face detector and **explicitly do not
  support animals or non-humanoid characters** — a stylised animal simply does
  not register and you get a no-op or garbage. This is architectural; prompting
  cannot fix it. Choose a model that documents non-human range.
- Name who speaks and state that everyone else keeps their mouth closed.
- **Inspect for burned-in captions** — some models hard-code subtitle overlays,
  often garbled, into the picture.
- Watch for the universal artifacts: teeth flicker, mouth-region blur where the
  face crop is lower resolution than the frame, visible seams on moving
  cameras, and degradation at profile angles.
- The audio already set the shot length in stage 7.

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

One clip, one review, one approval, then the next. Never batch.

**Cut each approved clip into the reel in place of its still, and review it
there.** A shot judged alone tells you almost nothing about whether it works.

On rejection, diagnose the actual cause before regenerating — inspect the
frames and name what went wrong rather than rerolling and hoping. And say
plainly when you have not been able to view something yourself.

Record every approved clip URL, with its duration, in `shots.md`.
