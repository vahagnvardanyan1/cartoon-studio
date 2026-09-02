---
name: clip-generation
description: Generate the video clips for an animated production, shot by shot, with keyframes, quality selection, a drift audit and an approval gate on every clip. Use when the shot list is approved, or when the user says "/clip-generation", "generate the clips", "render the shots", "start the video".
---

# Generate the clips

Render the film shot by shot. Each clip is generated from approved reference
art, inspected by you, then approved by the user before the next begins.

Read `${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md`,
`${CLAUDE_PLUGIN_ROOT}/references/video-craft.md`,
`${CLAUDE_PLUGIN_ROOT}/references/cinematography.md`,
`${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` and
`${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` first.

**This skill is the engine. `shot-loop` is the driver.** If you are working
through a film, run `shot-loop` and let it call in here per shot. Do not
generate a run of clips from this skill directly — a fault in the first will be
in all of them before anyone looks.

---

## Ask about quality first

Using AskUserQuestion so the user can just click:

**Draft quality** — low resolution for review with a full-resolution re-render
after approval (cheapest, and the draft predicts the final because it is the
same model), or full resolution straight away (fewer steps, roughly four times
the cost per attempt).

**Variants** — one take per shot, or two to choose between. Selection does more
for quality than any prompt tweak. Recommend two for character shots.

**Final resolution** — the resolutions the chosen model actually supports;
check the catalog rather than assuming.

Preflight the total and tell the user the cost. Budget against real numbers:
**~3 generations per usable shot for controlled reference-anchored work, ~10
for hard shots, ~20 for anything comedic or dialogue-heavy.** Over 40% of
finished shots end up stitched from two or more generations. That is normal,
not failure.

---

## Every shot is built the same way

### 1. Generate the start keyframe

From the approved references. **This is what holds identity** — video models
reinvent characters given only text, and frames-first is roughly 3× cheaper per
finished clip because you are not burning video credits to discover
composition.

The keyframe must show **the exact instant beat one begins from.** If beat one
is a downswing, the keyframe has the tool raised in both hands. A keyframe
showing the aftermath makes the action impossible to animate. This is Disney's
anticipation principle as a generation constraint.

It must also show **contact**: where the body meets the ground or the object,
with the soft dark occlusion shadow at the join. **If the keyframe has no
contact shadow the video model will float the character**, because nothing in
frame one says otherwise.

Carry the shot's camera block into the prompt as written: size, height, lens,
depth of field, light direction and ratio, and the staging geometry.

### 2. Generate an end keyframe for any shot with a move

Same scene, same lighting, stating only what has changed, with the final
framing pinned. **Words alone will not restrain a camera move; an end frame
will.** Both ends of a move must work as still images.

### 3. Run the silhouette test on both frames

If the pose does not read as a black shape, restage before generating motion.
This catches limbs merged into torsos, props lost against backgrounds, and two
characters occupying the same visual mass — all of which get worse in motion.

### 4. Render the clip

Submit asynchronously and poll.

Structure the prompt as **state, then instruction**:

- **State** — paste the identity string from `canon.md` byte-identical; declare
  what each character wears and holds, the continuity from the previous shot,
  and the geometric staging. Be as verbose as needed; the model has no memory
  of anything, and facts do not compete for adherence the way requirements do.
- **Instruction** — the active creative payload, **100–150 words**,
  front-loaded, in the nine-element order. Timed beats. One camera move with a
  speed word. Motion written as consequence, not mechanism.
- **Negatives** — **3–5, specific, each paired with a positive.** Check first
  whether the model has a dedicated negative field. Without one, a bare keyword
  list can be rendered *as subject matter* — "no snow" produces snow. Some
  models actively invert negatives; on those, write none and put everything in
  the positive. **20+ negatives produces stiffer, more generic output.**

Other rules that hold: give **every reference an explicit job** or it bleeds
its lighting and pacing into the shot; keep **reference strength below
maximum** or characters go stiff; and **hold colour temperature constant across
a sequence**, because lighting changes how the model reconstructs a face and a
dramatic change is a documented drift trigger.

### 5. Generate long, cut short

**Every clip is generated longer than the cut needs** — a 2.5-second shot is
still generated at 6–8 seconds. There is no way to extend a clip afterwards,
and there is always a better two seconds inside a longer take.

**The first and last second are the worst, for different reasons.** The head
carries initialisation artefacts — discard the first two frames of any chained
clip. The tail carries accumulated drift and history loss, and is where faces
morph and backgrounds reorganise. **Generate fifteen, use five, from the
middle.**

Treat every generation as a *pool of options*, not a take. Scrub it marking
usable seconds.

### 6. Inspect it yourself, and run the drift audit

Sample frames through the media tooling and look at them.

Score against the character sheet, 0–10 on six checks: **face shape · hair
length and parting · eye colour · wardrobe hue · the continuity mark · body
proportions under motion.**

**Accept at 7. Below 6, regenerate changing exactly one variable** — not the
whole prompt, which throws away the information about what was working.

Then check the shot-specific things: the hands, the relative scale, the season,
the prop marking, the light direction against the canon, the screen direction,
and the final framing. **Never present a clip you have not looked at.**

### 7. Present it

With what you found — including what is wrong. Then stop and wait.

---

## Speaking shots take a different path

A general video model **re-synthesises** any audio you give it, turning
dialogue into convincing-sounding nonsense. Catastrophic for a non-English
film, and not fixable by prompting.

**Verified failure:** a shot prompted with *"both men speak in turn — generate
the mouth movement from this description"* came back with both men's mouths
completely closed for ten seconds. The instruction was ignored outright.
Laying real dialogue under it produced the worst possible result: voices coming
out of shut faces.

**Treat every line of dialogue as requiring a lip-sync model, without
exception.**

- Pass the approved portrait keyframe and the **real recorded audio**. It
  passes through untouched and drives the mouth, so a non-English language
  survives exactly as recorded.
- **Portrait requirements:** front-facing or 10–20° off, even soft lighting
  with **no shadow line crossing the lips**, mouth unobstructed by hair or
  hands, neutral resting expression, simple background. Extreme angles and
  low-resolution crops fail.
- **Audio prep is where most failures originate:** trim leading and trailing
  silence, denoise, normalise without clipping, no music in the driving track.
- **Prompt for the three things that separate convincing from uncanny:**
  natural blinks, minimal gestures, subtle micro-expressions. Gestures too big
  and a dead unblinking stare are the two most common tells.
- **Check the model documents support for your character type.** Many lip-sync
  tools depend on a human face detector and explicitly do not support animals
  or non-humanoid characters. This is architectural; prompting cannot fix it.
- **Inspect for burned-in captions** — some models hard-code subtitle overlays,
  often garbled, into the picture.
- Watch for teeth flicker, mouth-region blur where the face crop is lower
  resolution than the frame, and degradation at profile angles.
- **Lip-sync degrades past about ten words per sentence**, worst at phrase
  endings. Split long lines across shots.
- The editorial fallback: **trim to the synchronised sections and cut away from
  the rest.** A talking head convincing for three seconds and cut away from
  beats one that is 80% convincing for eight.

### The consequence for coverage

The lip-sync model takes **one portrait**. So a two-hander where both characters
speak cannot be a two-shot. Cover the exchange in singles:

| | |
|---|---|
| wide | the approach or the situation — silent |
| single A | character A speaks → lip-sync |
| single B | character B answers → lip-sync |
| two-shot | the physical beat between them — silent |

Plan this at the shot list stage. If the shot list has a two-hander with two
speakers in it, it is already wrong.

---

## Audio, decided per shot

**No dialogue → native clip audio on.** The model's own sound is synchronised
to the motion it actually rendered, which no separately generated effects bed
can match. Describe the sound explicitly in its own block, and always say what
must not be there:

```
SOUND: the hard dull crack of wood striking, a single sharp yelp cut off
instantly, a heavy body hitting dry ground, then ragged breathing and a dry
wind. No music, no speech.
```

Check the default — on some models native audio is **on unless turned off**, so
a shot that must be silent needs it disabled by hand.

**Never describe background music in a video prompt.** It generates at
excessive volume and cannot be unmixed.

**Never pass speech to a general video model's audio reference field.** It
treats supplied audio as a *style* reference and re-synthesises it.

---

## Continuity across clips

Where two shots are continuous, use the previous clip's last frame as the next
clip's start frame — the single most reliable consistency technique available.

Allocate reference slots deliberately rather than filling them: hero portrait
frontal, three-quarter, wardrobe close-up, previous shot's final frame.
**Angular diversity is the requirement** — several references at similar angles
produce poor consistency.

Watch for drift as you go. **If drift appears twice, the reference is at fault,
not the prompt** — go back and fix the sheet, and be honest that shots already
rendered will need redoing.

---

## Operational

- Video is **async**. Fire, then poll. A draft clip is 2–4 minutes.
- Expect occasional `timeout while fetching resource` on the reference image.
  Re-fire the same job.
- Expect concurrency limits on parallel lip-sync jobs. Fire them serially.
- Draft everything at low resolution. It is the same model at roughly a quarter
  the cost, so the draft predicts the final honestly. Re-run only the keepers.

## Approval

One clip, one review, one approval, then the next. Never batch.

**The review unit is never a bare clip.** A silent clip cannot be judged; the
user approves things from picture alone that fall apart the moment the voice
goes on. Hand every clip back to `shot-loop` to be cut with its audio before it
is shown.

On rejection, diagnose the actual cause before regenerating — inspect the
frames and name what went wrong rather than rerolling and hoping. Say plainly
when you have not been able to view something yourself.

Record every approved clip URL, with its duration, in `shots.md`.
