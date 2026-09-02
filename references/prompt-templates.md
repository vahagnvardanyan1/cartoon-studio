# Prompts

Structure matters more than wording. Two rules govern everything below:

> **A prompt only carries what gets written into it. Everything left out still
> gets decided — just by the model instead of by you.**

> **Text is for spatial decisions. References are for identity and temporal
> decisions.**

---

## 1. The nine elements, in order

Models weight early tokens more heavily, so the order is part of the
instruction. Write every image and video prompt in this sequence:

```
1. Camera        size, height, angle, movement (one), with a speed word
2. Lens          focal length; spherical or anamorphic; depth of field
3. Light         the named source, its direction, its quality, its Kelvin
4. Palette       named values, or the tonal mode
5. Composition   who is where, facing which way, what is in the foreground
6. Atmosphere    the physical stuff — haze density, dust, rain, smoke
7. Mood          the emotional register, stated separately from atmosphere
8. Attribution   a film or DP reference, paired with the trait you want from it
9. Negatives     3–5, specific, model-permitting
```

Keeping 6 and 7 separate matters. "Haze" is a thing in the air the model can
render; "melancholy" is a instruction about grade and performance. Merged, they
produce neither.

## 2. Length

| Words | First-attempt success | Use for |
|---|---|---|
| 30–60 | ~55% | exploration, B-roll |
| **80–150** | **~72%** | **the production default** |
| 200–350 | ~68% | hero shots needing maximum control |
| 400+ | falls off | over-constrained; instructions start conflicting |

**Peak is 100–150 words. Prompt length is a control dial, not a quality dial.**

This is the *active creative payload*. State re-declaration — the identity
strings, the geometry, the continuity — sits outside that budget and should be
complete however long it runs. The distinction is real: instruction adherence
decays by position, so a prompt carrying eight *requirements* honours four or
five at random, but a prompt carrying eight *facts* is fine.

**Every prompt is fully self-contained.** Re-describe the setting, the
character and the tone in every one. Assume zero context from adjacent shots,
because there is none.

---

## 3. Replace every vague adjective

The words that do nothing: *cinematic, dynamic, moody, beautiful, epic, high
quality, stunning, masterpiece.* Each of them hands a decision back to the
model.

| Instead of | Write |
|---|---|
| "dynamic cinematic lighting" | "overcast 6000K daylight through fog as key, soft and directionless; headlights the only warm practical" |
| "moody close-up" | "close-up, slow dolly in, 85mm, shallow depth of field, warm 2800K from the bar practicals only, split-toned amber and emerald, light haze" |
| "she looks sad" | "her jaw sets, she looks down and away, one slow blink, breath held" |
| "he moves quickly" | "he strides, coat snapping, dust trailing from his heels" |
| "beautiful landscape" | "low sun at 5° elevation raking across the ridge, long shadows, 9,000K shade in the valley" |

**Emotion must be tied to a visible action.** "Flat emotion" in generated video
traces to prompts that state the scene idea but never a visible expression. Name
the gaze, the held breath, the sigh.

---

## 4. Camera language models actually obey

Use these terms. They are the vocabulary the video models were documented
against.

`dolly in` · `dolly out` · `pan left/right` · `whip pan` · `tilt up/down` ·
`truck left/right` · `orbit` · `crane up` · `handheld` · `gimbal` ·
`locked-off static`

Four rules:

- **Never write "zoom in."** Models read it as pixel enlargement. Write "dolly
  in" or "push in", and add "perspective shifts naturally with parallax."
- **Attach a speed or duration to every movement term** — "slow", "deliberate",
  "steady", "rapid", or "slow 5-second pan right."
- **One primary camera move per generation.** For a multi-phase move, describe
  *what is in frame at each phase* rather than stacking movement verbs.
- **Establish the camera-subject relation with a verb** — the camera *follows*,
  *matches*, *reveals*.

A dolly zoom needs its mechanism spelled out: "camera dollies back while the
lens zooms in simultaneously."

---

## 5. Motion that reads as physical

**Describe outcomes, not mechanisms.** "Knee bends at 45 degrees, foot lifts
ten inches" confuses the model. Consequence language works:

- **Contact and deformation** — "boots sink into deep mud", "displaced clumps",
  "sand spray", "the plank flexes under him"
- **Verbs that encode mass** — sinks, trenches, plants, braces, plows
- **Impact** — "firm contact", "impact vibration"
- **Physics as instruction** — "with weight", "natural hesitation", "contact
  settling"
- **Sensory consequence** — "dust particles hang", "steam rises", "cloth
  rustles"

**Weight-first composition** is the deeper trick: fix the physics in the *still*
before you animate. The keyframe should already show surface compression, the
soft dark **ambient occlusion where two surfaces meet**, and anatomical tension
consistent with the load being carried. **If the keyframe has no contact
shadow, the video model will float the character**, because nothing in frame
one says otherwise.

### Timed beats

The highest-leverage single technique. Break the shot into two-second spans,
each with its own verb and consequence:

```
0-2s   <verb + physical consequence + micro-expression>
2-4s   <verb + physical consequence + micro-expression>
4-6s   <verb + physical consequence + micro-expression>
```

Without this, a model given one vague action and eight seconds will idle for
six of them.

### Fixing the slow-motion bias

Models default to slow because minimising pixel change per frame is the safest
route to temporal consistency. Adverbs do not fix it. Three things do:

1. **Speed-encode the verb** — walks → strides, hurries, rushes.
2. **Add environmental motion cues** — the model infers speed from consequence.
3. **Give the camera a matched velocity** — "camera tracks at matching
   velocity."

---

## 6. Negatives

**Check whether your model has a dedicated negative field before writing any
AVOID list.** Three cases:

- **A dedicated negative field** — keyword lists work.
- **No negative field** — a bare keyword list can be rendered *as subject
  matter*. "No snow" produces snow. Use grammatical prohibition ("a landscape
  with no buildings") or, better, describe the positive state.
- **A model that actively inverts them.** Some do. Write "he is NOT crying" and
  it does the opposite. On those models write no negatives at all and put
  everything in the positive.

**Dosage: 3–5 core negatives per shot, each paired with a positive
counterpart** — "no harsh sunlight — sunny day, slightly backlit". **20+
negatives produces stiffer, more generic output**, because you have pushed the
sample toward the bland centre of the distribution.

Broad quality terms — *bad quality, ugly, low resolution* — do nothing. They
are too abstract to constrain the sampler. Name specific failure modes instead:

| Shot type | Negatives worth having |
|---|---|
| Human close-up | no facial warping, no uncanny expressions, no exaggerated features |
| Motion | no rubbery stretch, no floaty hover, no jitter, no extreme speed |
| Stability | no camera drift, no sudden zooms, no flicker, no changing facial features |
| Editorial drift | no montage, no cutaways, no unprompted cuts |
| Anything with words | no text, no letters, no subtitles, no watermark |

**Positive phrasing is the safer default everywhere.** Write "locked camera",
not "no camera movement".

---

## 7. The universal style block

Prepend a fixed block to every prompt in the film, byte-identical. It is what
makes twenty separately generated shots read as one production.

```
<format>. <render register — and what it is NOT>.
24fps, 180° shutter. <texture spec>.
<DP or film attribution, paired with the trait wanted from it>.
```

A worked example of the shape:

```
8K IMAX. Photorealistic — no 3D render, no game engine.
24fps, 180° shutter, pore-level skin realism.
Lubezki × Deakins.
```

Note what it does: it names the format, it names the register **and its
negation**, it pins the shutter (which is what stops video-ish motion), it
demands surface texture by name, and it attributes. Write yours once, at the
style stage, and never paraphrase it.

---

## 7b. Identity: the rule flips between text-to-image and image-to-image

**This is the most commonly-got-wrong thing in the whole pipeline, and the two
halves of it contradict each other.**

### Text-to-image, no reference attached

The verbatim identity string is the *only* thing carrying continuity. Paste it
byte-identical into every prompt. Any rewording is read as a new character.

### Image-to-image / edit / any call with a reference image attached

**Do not re-describe the person.** A written description of a face competes with
the reference and pulls the result toward a new face — a generic, beautified,
averaged one. Identity comes from the reference image *only*.

```
❌  "a man in his forties with thick dark hair greying at the temples
     and a short dark beard, standing at the counter"
✅  "the man from reference image 1, standing at the counter, three-quarter
     to camera, lit from the window camera-left"
```

**What you are still allowed to describe:** head orientation · facial angle ·
expression · lighting direction · framing · pose · what he is holding ·
where he is. **What you must not describe:** age · build · hair · beard ·
colouring · face shape — every attribute already visible in the reference.

Append the lock list instead:

```
Preserve the exact facial identity from the reference image.
Do not modify eye shape or spacing, nose structure, jawline, cheekbones,
or face proportions. Identity must remain identical to the reference.
```

And the negatives that target this specific failure:

```
different person · altered face · changed facial features · new identity ·
generic face · beautified face · plastic skin · face distortion
```

**Identity preservation outranks style.** If the two conflict, keep the face.

### Which one applies where in this pipeline

| Stage | Mode | Rule |
|---|---|---|
| Character sheet | t2i | verbatim identity string |
| Scale sheet | t2i | verbatim identity strings for all leads |
| Environment plate | t2i | no characters at all |
| **Shot keyframe** | **i2i, sheets attached** | **pose, framing and light only. Never the face** |
| Clip | i2v, keyframe attached | motion only — do not re-describe anything already in the frame |
| Lip-sync | portrait attached | who speaks, blinks, gestures. Never the face |

Most of the film is built in the right-hand mode. The natural thing to write is
the wrong thing.

---

## 7c. Give every reference an explicit role

Passing several references without saying what each is *for* is a documented
failure mode: the model averages them, or takes lighting from the one you
wanted only motion from. Name the job inline.

| Purpose | Phrasing |
|---|---|
| First frame | `@Image1 as the first frame` |
| Last frame | `@Image2 as the last frame` |
| Character identity | `@Image1's character as the subject` |
| Scene / background | `scene references @Image3` |
| Wardrobe | `wearing the outfit from @Image2` |
| Camera movement | `reference @Video1's camera movement` |
| Action / choreography | `reference @Video1's action choreography` |
| Rhythm / tempo | `video rhythm references @Video1` |
| Prop appearance | `prop details reference @Image4` |

Combined:

```
@Image1's character as the subject, scene references @Image2,
reference @Video1's camera movement only
```

**Never write a bare "reference @Video1."** Specify *what* to reference —
camera, action, effects, rhythm — or it brings all of them.

A fixed convention for this pipeline, so prompts stay legible across a
production:

```
@Image1  identity anchor      the character sheet
@Image2  environment plate    geometry, light, screen direction
@Image3  style / scale        the style key or the scale sheet
@Image4  continuity           the previous shot's final frame
```

And an explicit consistency block inside the prompt when a shot has more than
one character or crosses a cut:

```
CONSISTENCY RULES
- Same character throughout — the face of @Image1 in every frame
- Same wardrobe across the entire shot
- Same environment and light direction as @Image2
- Asymmetric marks on the correct side
```

---

## 7d. Asymmetric continuity marks

Give every character at least one **asymmetric** identifying detail: a scar
over the *right* eyebrow, a glove on the *left* hand only, a satchel on one
shoulder, a patch on one knee, one rolled sleeve.

Two reasons, and the second is the real one:

1. Asymmetry gives the model a hard landmark to preserve, and identity drift
   between shots is the most commonly reported failure when characters are
   described only symmetrically.
2. **It converts drift from a judgement into a binary check.** "The face looks
   a bit off" is unfalsifiable and gets waved through. "The scar is on the left
   in shot 7 and the right in shot 4" is objectively wrong, catchable in a
   contact sheet, and impossible to argue with.

Write it into the character sheet, into the identity string, and into the
drift audit. Add `Asymmetric identifying details preserved on the correct side`
to keyframe prompts.

A mirrored mark is also a *diagnosis*: it means the model flipped the frame,
which usually means the screen direction went with it.

---

## 8. Templates

### Character sheet (turnaround)

```
A professional character model sheet for <register>, plain flat warm light-grey
studio background, soft even neutral lighting.

THE CHARACTER: <age, build, face, colouring, hair, distinguishing marks>
COSTUME: <every garment, colour and detail>
CONTINUITY MARK: <the one unmistakable identifier>
HANDS: <articulation spec — separated fingers, visible knuckles and joints>

LAYOUT: the same character four times in a row, same height and scale,
relaxed neutral A-pose, empty hands:
1. front  2. three-quarter  3. profile  4. back

<universal style block>
AVOID: fused fingers, extra fingers, text, letters, labels, watermark.
```

**Angular diversity is required, not decorative.** Two or three references at
similar angles produce poor consistency; front plus three-quarter plus profile
eliminates most drift by the third shot.

### Scale sheet — once, all leads together

```
A character SCALE COMPARISON sheet — all characters side by side on the same
ground line, facing camera, full body, matching contact shadows.

RELATIVE HEIGHT IS THE ENTIRE POINT OF THIS SHEET AND MUST BE UNMISTAKABLE:
<A> is the big one. <B> is the small one. <B>'s head reaches only to about
<A>'s shoulder. Do not draw them the same height.

AVOID: equal heights, <B> as tall as <A>, text, labels, height charts.
```

### Environment plate

```
An environment plate — NO characters at all.

THE PLACE: <architecture, materials, layout, landmarks>
GEOMETRY: <what is on the left, what is on the right, where the exits are>
SEASON AND WEATHER: <explicit, with the negation>
LIGHT: <source, direction, elevation, shadow length, shade colour, Kelvin>
<universal style block>
AVOID: characters, people, animals, text, letters, signage, watermark.
```

The GEOMETRY line is what later prompts paste in to hold screen direction.

### Shot keyframe (start frame)

```
A single frame from <register>.

CAMERA: <size>, <height>, <angle>, <lens>mm, <depth of field>
LIGHT: <source, direction, quality, ratio, Kelvin>
CHARACTERS: <identity strings, byte-identical from canon.md>
SIZE LOCK: <who is taller>
HANDS: <articulation, and exactly what they hold, fingers visible>
STAGING: <who is where, facing which way; the axis; screen direction>

THE MOMENT: <the exact instant beat one begins from — mid-action, loaded,
about to move. Never a resting pose.>

CONTACT: <where body meets ground or object, with the occlusion shadow>
<universal style block>
AVOID: <3–5 specific failure modes>
```

Two lines earn their place. **THE MOMENT** is Disney's anticipation principle
as a prompt instruction — a keyframe showing the aftermath makes the action
impossible to animate. **CONTACT** is what stops the character floating.

### End keyframe

The start frame, plus: *"the SAME scene, SAME characters, SAME set, SAME
lighting, a few seconds later in the same continuous shot"* — then state **only
what has changed**, and pin the final framing explicitly.

Words alone will not restrain a camera move. An end frame will.

### Motion shot

```
Single continuous <N>s shot, <aspect>, beginning exactly on the supplied first
frame and finishing exactly on the last frame.

BEATS:
0-2s  <verb + consequence + micro-expression>
2-4s  <verb + consequence + micro-expression>
4-6s  <verb + consequence + micro-expression>

CAMERA: <one move, with a speed word, and its end framing>. No cuts.
PHYSICS: <weight, contact, follow-through on loose parts>
SOUND: <explicit — what is there, and what must not be>
AVOID: <3–5 specific>
```

For image-to-video, **do not re-describe what is already in the image.** Spend
the whole payload on motion.

### Speaking shot

Portrait keyframe plus the real recorded audio, into a lip-sync model. In the
prompt: name who speaks, say the mouth syncs to the supplied speech, say
everyone else keeps their mouth closed, and ask explicitly for **natural
blinks**, **minimal gestures** and **subtle micro-expressions** — those three
are what separate convincing from uncanny.

Portrait requirements: front-facing or **10–20° off**, even soft lighting with
**no shadow line crossing the lips**, mouth unobstructed, neutral resting
expression, simple background. Extreme angles and low-resolution crops fail.

Audio prep matters more than the prompt: trim leading and trailing silence,
denoise, normalise without clipping, no music in the driving track.

### Options sheet — when a detail is contested

One image, four treatments of the same feature, identical in every other
respect, in a row. Let the user pick a number. Converges in one round instead
of five.
