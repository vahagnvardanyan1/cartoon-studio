# Production lessons

Every item here was a real failure on a real film before it was a rule. Read
this before writing a single prompt.

---

## 1. The lazy-shot problem

**Symptom:** clips look like a still image with a slight wobble. The film feels
dead even though each frame is pretty.

**Causes and fixes:**

| Cause | Fix |
|---|---|
| One vague action stretched over 8–10s | Break the shot into **timed beats**: `0–2s`, `2–4s`, `4–6s`, each with its own verb |
| Prompt is 80% style words, 20% action | Invert it. Action dominates; style is a short block at the end |
| Emotions written as adjectives ("hopeful", "sad") | Write **observable movement**: "ears sink", "brows draw together", "shoulders settle lower" |
| States instead of consequences | "The log splits, both halves leap off the block and clatter" — not "he chops wood" |
| Writing "static camera, no movement" | Never. Give every shot **one** camera move, however small |
| No film-look block | Add: 35mm film quality, professional colour grading, motion blur, halation, fine grain, shallow depth of field |
| No negative constraints | Always end with an explicit **AVOID** list |

**Shot prompt skeleton:**

```
Single continuous Ns shot, 16:9, stylized 3D animated feature film,
beginning exactly on the supplied first frame. SILENT.

SUBJECT: <character, locked description, key continuity marks>
SIZE LOCK: <who is bigger than whom, if two characters>

BEATS:
0-2s - <verb + consequence + micro-expression>
2-4s - <verb + consequence + micro-expression>
4-6s - <verb + consequence + micro-expression>

CAMERA: <one move, with an explicit end framing>
HANDS: <articulation reminder if anything is held>
LIGHT: <key direction, colour, season>
FILM LOOK: 35mm, colour grading, motion blur, halation, grain, shallow DoF
AVOID: <the specific failure modes for this shot>
```

---

## 2. Character consistency

Video models **reinvent** a character every render unless you give them
something to copy.

- **Always generate a still keyframe first** (image model), then animate that
  keyframe. Image models hold identity; video models do not.
- The character sheet must be the source of every keyframe. Never describe a
  character from memory twice — describe it once, then reference the sheet.
- Give each character **one unmistakable continuity mark** (a notched ear, a
  red sash, a marked prop) and repeat it in every prompt.
- Expect breed/build drift anyway. Check frames. If a design renders
  consistently but differs from your original sheet, consider adopting the new
  one as canon rather than fighting it every shot.

### Scale: build a two-character sheet

**The trap:** generating each character's turnaround separately, each scaled to
fill its own frame. Nothing then records that one is smaller than the other,
and every shot guesses — often making the wrong character bigger.

**The fix:** one **scale comparison sheet** with all main characters standing
side by side on the same ground line, correct relative heights, matching
contact shadows. Make that sheet the master reference. State the size
relationship as a **SIZE LOCK** line in every subsequent prompt.

### Hands: fix them at the sheet, not in the shot

**The trap:** character sheets generated with rounded paws or mittens. Then
every prop shot fails — the tool won't be gripped, the needle can't be held,
the hand is a stump. No amount of prompting fixes it downstream.

**The fix:** specify hands explicitly when building the character sheet —
*four separated fingers plus an opposable thumb, visible knuckles and joints,
short claws, pads, fur on the back of the hand*. Cite a known reference style.
Pose the sheet with hands raised and fingers spread so the construction is
visible and gets inherited.

---

## 3. Props

**The trap:** a keyframe showed an axe already buried in a chopping block,
while beat one asked the character to swing it down. The model animated the arm
and left the axe behind, floating.

**Two rules:**

1. **The start frame must show the exact state beat one begins from.** If the
   first action is a downswing, the keyframe shows the tool raised overhead in
   both hands — not resting, not planted.
2. **Write an explicit attachment rule:** "both hands stay closed around the
   handle; the tool never floats free, never separates while the arms move; he
   releases only after it is buried in the block." Then give the release a
   *reason* in the beats, so the hands become free legitimately.

Hero props also need their own reference sheet with a **distinctive marking**,
so the audience can recognise the same object across shots — and so you can
tell when the model has quietly swapped it for a generic one.

---

## 4. Camera control

Push-ins run away. A shot asked to "end at a medium" will happily finish on a
nostril, with heads cropped out of frame.

- Words alone do not restrain the camera. **Generate an end keyframe** and pass
  it alongside the start frame. The camera then must travel from A to B.
- Even with an end frame, the *middle* of the move can overshoot. If it does,
  start wider so the whole arc sits lower.
- For two-character shots, say explicitly: *both heads stay fully in frame for
  the entire shot; never crop a head; never end on one face.*

---

## 5. Continuity canon

Write the canon down **before** generating, and repeat the relevant line in
every single prompt. Otherwise the season, time of day and weather drift shot
to shot — snow appearing halfway through an autumn scene, afternoon becoming
dusk.

Minimum canon to record:

- Season and weather progression, beat by beat, and the direction it moves
- Time of day and the direction of the key light
- Which landmark anchors wide shots, and on which side of frame
- Each character's continuity mark and colour temperature
- Every prop's distinguishing feature

Then add a hard negative to prompts: `AVOID: snow` in autumn shots, and so on.
Positive description is not enough; the model needs the prohibition.

---

## 6. Speech, dialogue and lip sync

This is the area with the most traps.

- **Video models re-synthesise supplied speech.** Feeding a video model a
  dialogue track as a reference produces invented gibberish that merely
  *sounds* like the language. **Never** feed non-English dialogue to a general
  video model expecting playback.
- **Use a dedicated lip-sync model for speaking shots.** Models built for
  portrait + audio (avatar / audio-driven-portrait types) preserve the actual
  audio file and sync the mouth to it. They also tend to output at higher
  resolution than the draft pipeline.
- **Check the lip-sync output for burned-in subtitles.** Some avatar models
  hard-code caption overlays — often garbled, often in the wrong script —
  directly into the picture. Inspect a frame before accepting the clip.
- **Speaking-shot length is set by the audio**, not by your shot list. Plan for
  that; let the line dictate the cut.
- **Silent shots are the safe default.** Render action silent with frame
  control, then lay narration and score over them in the edit. Approximate
  sync with correct language beats perfect sync with nonsense.

### Non-English voice

- Confirm the language is actually supported before building an audio plan
  around a model. Support varies enormously between versions of the same
  family.
- **Language codes are inconsistent.** A documented ISO code may be rejected
  where a shorter variant works. If a code errors, try the two-letter form.
- **Audition several voice models on one identical sentence** and let a native
  speaker choose. This costs almost nothing and settles the question in one
  round.
- A human recording is always an option, and for a culturally significant text
  it may be the right one. Twenty short lines take twenty minutes.

---

## 7. On-screen text

Image and video models mangle lettering, especially non-Latin scripts.

**Never generate text inside a frame.** Put `no text, no letters, no signage,
no watermark` in every AVOID list. Titles, credits and any on-screen words are
typeset during assembly, where they will be correct.

---

## 8. Working economically

- **Draft at low resolution, finish at high.** A 480p draft costs roughly a
  quarter of a 1080p render. Use the same model for both so the draft predicts
  the final — only the resolution changes.
- **Generate variants and select.** Professional AI film work is heavy
  selection, not first takes. Two drafts of every character shot, keep the
  better one.
- **Preflight before spending.** Validate parameters and quote cost first.
- **When a detail is contested, generate an options sheet** — one image showing
  four treatments of the same feature — and let the user pick. One round
  instead of five.

---

## 9. Verify your own work

You cannot judge a film you have not looked at.

- Sample frames from every finished clip and **actually inspect them** before
  presenting. Check the continuity marks, the hands, the scale, the season, the
  final framing.
- Report what is wrong before the user finds it. A named flaw builds trust; a
  hidden one destroys it.
- If the generated media cannot be viewed directly, render a contact sheet of
  frames through the media tooling and look at that.

---

## 10. Approval discipline

- **One asset at a time.** Generate, present, wait. Never batch through an
  approval gate.
- **Never start a stage without approving the previous one.** A character
  approved late is a character every downstream shot has to be redone for.
- Present each asset with **what to check** — the two or three things most
  likely to be wrong — rather than a general "what do you think?".
- When something is rejected, fix the *cause*, not the symptom. A wrong hand in
  one shot means the character sheet is wrong in every shot.
