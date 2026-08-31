# Prompt templates

Copy these shapes. The structure matters more than the wording.

---

## Character sheet (turnaround)

```
A professional character model sheet for a 3D animated feature film, on a plain
flat warm light-grey studio background with soft even neutral lighting.

THE CHARACTER: <species, build, face, fur/skin, eyes, distinguishing marks>
COSTUME: <every garment, colour and detail>
CONTINUITY MARK: <the one unmistakable identifier>

HANDS: proper animated-feature character hands, NOT paws and NOT mittens —
four clearly separated fingers plus an opposable thumb, visible knuckles and
finger joints, short blunt claws, soft pads, short fur on the backs. Fingers
individually articulated and readable.

LAYOUT: the same character four times in a row, same height and scale,
relaxed neutral A-pose, empty hands:
1. front  2. three-quarter  3. profile  4. back

RENDER: <shared render spec>
AVOID: paws, mitten hands, fused fingers, extra fingers, <character-specific>,
text, letters, labels, watermark.
```

## Scale comparison sheet — do this once, for all leads together

```
A character SCALE COMPARISON sheet ... all characters side by side on the same
ground line, facing camera, full body, matching contact shadows.

RELATIVE HEIGHT IS THE ENTIRE POINT OF THIS SHEET AND MUST BE UNMISTAKABLE:
<A> is the big one. <B> is the small one. <B>'s head reaches only to about
<A>'s shoulder. Do not draw them the same height.

AVOID: equal heights, <B> as tall as <A>, ..., text, labels, height charts.
```

## Environment plate

```
An environment plate from a 3D animated feature film — NO characters at all.

THE PLACE: <architecture, materials, layout, landmarks>
SEASON AND WEATHER: <explicit, with the negative — e.g. "NO SNOW">
LIGHT: <sun height and direction, shadow length, shade colour, sky>
RENDER: <shared render spec>
AVOID: characters, people, animals, text, letters, signage, watermark.
```

## Shot keyframe (start frame)

```
A single cinematic frame from a 3D animated feature film.

CHARACTERS: reproduce EXACTLY from the reference sheet — <identity, costume,
continuity marks>. SIZE LOCK: <who is taller>.
HANDS: <articulation spec, and what they are holding, with fingers visible>

THE MOMENT: <the exact instant beat one begins from — mid-action, loaded,
about to move. Not a resting pose.>

FRAMING: <shot size, camera height, who sits where, headroom>
LIGHT: <matching the canon>
FILM LOOK: 35mm film quality, professional colour grading, halation, fine
grain, shallow depth of field, subsurface scattering.
AVOID: <season violations, prop errors, mitten hands, text, watermark>
```

## End keyframe

Same as the start frame, plus: *"the SAME scene, SAME characters, SAME set,
SAME lighting, a few seconds later in the same continuous shot"*, then state
only **what has changed**, and pin the final framing explicitly (both heads in
frame, nothing cropped).

## Silent motion shot

```
Single continuous Ns shot, 16:9, stylized 3D animated feature film, beginning
exactly on the supplied first frame and finishing exactly on the last frame.
SILENT — nobody speaks, mouths stay closed.

SIZE LOCK: <...>
BEATS:
0-2s - <verb + consequence + micro-expression>
2-4s - ...
4-6s - ...
CAMERA: <one move, explicit end framing, "no cuts">
HANDS: <articulation reminder>
LIGHT / FILM LOOK: <...>
AVOID: <speech, moving mouths, season violations, prop detachment, mitten
hands, cropped heads, extreme close-up, jitter, bent limbs, cuts, text,
watermark>
```

## Speaking shot (lip-sync model)

Portrait keyframe + the real audio file. In the prompt, name who is speaking,
say the mouth syncs to the supplied speech, and say explicitly that everyone
else keeps their mouth closed. Then inspect the output for burned-in captions.

## Options sheet — when a detail is contested

One image, four treatments of the same feature, identical in every other
respect, in a row. Describe each variant. Let the user pick a number. Converges
in one round instead of five.
