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

## Output

Record the style in `canon.md` and the approved keyframe URL in `assets.md`,
marked as the master reference.

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
changes. On *Drop of Honey* a flat illuminated-manuscript sequence worked
beside stylised 3D and would have shattered beside photography; the fix kept
the idea and changed the execution to **a real manuscript photographed on the
same lens**, written portion turned away and out of focus so no lettering
appears.

A register break should read as a change of **subject**, not a change of
medium.
