---
name: visual-style
description: Define and lock the visual style for an animated production, then prove it with a single style keyframe. Use after the visual elements are listed, or when the user says "/visual-style", "define the look", "choose a style", "what should this look like".
---

# Define the visual style

Agree the look, then prove it in one image before building anything on top
of it.

## If the user supplied reference images

Analyse them and describe what you see, specifically: rendering approach,
character proportions, eye and face construction, palette, lighting, texture
density, camera language. Build the style from those rather than from your own
preference.

Ask whether the references are **the look to match** or merely nearby — that
distinction matters, and users often mean one when they say the other.

## The available style

**Feature 3D** — the polished, warm, soft-shaded look of a modern animated
feature. Stylized realism: physically plausible light with cartoon-appealing
forms.

- **Rendering** — soft global illumination, subsurface scattering in fur and
  skin, shallow cinematic depth of field, gentle bloom in warm light. Never
  photoreal, never plastic.
- **Proportions** — heroic-cartoon build, heads slightly oversized, roughly
  1:4.5 head to body. Silhouettes readable in pure black.
- **Faces** — large eyes with visible iris detail and a wet specular highlight;
  strongly readable brows carrying most of the acting.
- **Texture** — high micro-detail where it reads: individual fur strands in rim
  light, woven cloth, weathered stone. Backgrounds slightly softened so
  characters carry the frame.
- **Camera** — grounded and motivated. Slow push-ins for intimacy, locked
  frames for repetition, handheld only for chaos, one kinetic move reserved for
  the climax.

Adapt the palette, cultural detail and lighting to the story. The rendering
approach stays constant.

## Then define, specific to this film

- **Colour palette** — six to eight named values, drawn from the story's own
  world
- **Lighting and atmosphere** — key direction and colour per act
- **Cultural elements** — the specific architecture, textile, ornament
- **Mood** — how the film should feel, and where that feeling changes

## Prove it with one keyframe

Before any character or environment work, generate **a single style keyframe**:
the most characteristic moment in the film, with the leads in it, at full
quality. One image locks palette, render quality, texture treatment and
proportions together.

Get it approved before anything else is built. Everything downstream inherits
from it, so this is the cheapest possible place to course-correct.

If the film's season or palette later changes, **regenerate this keyframe
first**, then rebuild anything derived from it. A stale master keyframe
silently poisons every shot built against it.

## Then build the colour script

Once the style key is approved, build a **colour script**: a strip of small
images, one per story beat, mapping value, hue and lighting across the whole
film. Thumbnail size. One generation per beat, in a single pass.

Its purpose, in Ralph Eggleston's words about the Pixar practice, is to hold
"the emotional core of what we're trying to say visually with colour, value and
lighting." **You should be able to read the story's arc from it with the images
too small to identify.**

It does two concrete jobs here:

1. It stops every scene coming out the same temperature — which, with
   unmotivated lighting, is most of why generated films look flat.
2. It gives the finishing grade a target. The final grade matches every shot to
   a hero still; the colour script decides which still, and where the film is
   *supposed* to change temperature rather than being corrected to uniformity.

Present it as one image strip and get it approved with the style.

## Write down the light

In `canon.md`, per location and per act: the key source, its direction, its
quality, its ratio and its Kelvin. Also the **axis of action** per location —
what is on the left, what is on the right, which way characters enter.

Both get pasted into every prompt set in that location. The model has no memory
of either, and light direction and screen direction are two of the three
continuity classes that break an audience's spatial model rather than merely
denting credibility.

## Output

Record the style in `canon.md`, the approved keyframe URL in `assets.md` marked
as the master reference, and the colour script strip alongside it.

Write the **universal style block** into `canon.md` too — the fixed text
prepended byte-identical to every prompt in the film. It names the format, the
render register *and its negation*, the shutter, the texture spec and the
attribution. See `${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md` §7. It
is what makes twenty separately generated shots read as one production, and it
must never be paraphrased.

---

## Offer directions as an options sheet, never iterate on one

If the user rejects the style key, do not adjust it and re-run. Generate **the
same subject in three or four clearly different registers in one pass** and let
them point at one. The comparison is the deliverable.

Directions worth having ready, each named with real reference points so the
model has something to aim at:

- **Photoreal live action** — "shot on 65mm, anamorphic, shallow depth of
  field, natural light only, subtle film grain, restrained cinematic colour
  grade, real weathered materials, no stylisation of any kind"
- **Graphic painterly 3D** — the Spider-Verse / *Last Wish* register: ink
  outlines of varying weight, halftone and brushstroke over the forms, flat
  blocked colour, hard-edged shadow shapes
- **Painted-texture 3D** — the *Arcane* register: visible brushwork and canvas
  grain over dimensional form, no outlines, deep saturated coloured shadows
- **Flat graphic 2D** — Cartoon Saloon: flat shapes, limited palette,
  decorative pattern, paper grain, deliberate off-register colour

"Stylised 3D animated feature with soft global illumination" is the default
that reads as a decade old. Do not offer it as the only option.

## The register decision cascades — re-audit after it changes

Any planned deviation from the main style has to be re-checked when the style
changes. On one production a flat-illustration sequence worked
beside stylised 3D and would have shattered beside photography; the fix kept
the idea and changed the execution to **a real manuscript photographed on the
same lens**, written portion turned away and out of focus so no lettering
appears.

A register break should read as a change of **subject**, not a change of
medium.
