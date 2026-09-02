# Finishing

The cheapest and most reliable quality gain available, and almost nobody does
it.

When the Runway film festival jury explained what separated its finalists from
ordinary AI video, the answer was not the model. It was **editing, colour
grading and sound design.** When Coca-Cola spent 70,000 generations and roughly
twenty people on a broadcast spot, it was panned anyway — scale did not
substitute for these decisions. This file is the part of the pipeline that
decides whether the film reads as a film.

**Run it as a pass over the finished cut, not per shot.** Most of it is a
relative judgement across the whole thing and cannot be made one clip at a
time.

---

## 1. Order of operations

The order is not arbitrary and getting it wrong wastes the work.

```
1. upscale
2. per-clip normalisation
3. film emulation
4. blur, then grain
5. match every shot to a hero still
6. motion imperfection
7. speed pass
8. sound
9. titles
```

---

## 2. Upscale first, before grading

Two reasons, both mechanical:

- You upscale to restore detail that you then **intentionally soften** in step
  4. Softening noise directly gives you soft noise.
- It cleans compression artefacts *before* you push contrast into them.

**Architecture matters more than brand.** Upscalers trained on real degraded
footage sharpen what is already there — which amplifies the temporal flicker
inherent in generated video. Diffusion-based upscalers treat the job as
conditional generation and invent plausible texture matching the distribution
of generated footage. **Use the diffusion family here, at low restoration
strength**, or it over-sharpens back into plastic.

**Upscale before frame-rate interpolation, never after.** Interpolation smooths
motion; it does not sharpen pixels.

---

## 3. Grade in four passes

### Pass 1 — per-clip normalisation

Waveform and vectorscope. Neutralise white balance, set black and white points,
and **tame oversaturation**. Do this per clip, because generation-to-generation
variance is the enemy.

This pass is where you kill the **deep-fried look**. The mechanism is worth
knowing: models do RGB arithmetic rather than perceptual colour reasoning, so
over-prompting colour keywords ("teal and orange") makes them over-compensate.
The fix is at the grade, not the prompt.

### Pass 2 — film emulation

A film LUT on its own node — Kodak 2383, Fuji 3510, or an Arri LogC-to-Rec709 —
at **60–80% opacity**. Do not bake it. Drive it with lift/gamma/gain so it
stays adjustable per scene.

### Pass 3 — blur, then grain. In that order.

- **Light Gaussian blur, 0.3–0.6px, FIRST.**
- **Then 35mm or 16mm grain at 8–15% opacity.**

The order is the whole point. The blur kills the plastic over-sharpness that is
the most recognisable AI texture tell; the grain replaces the high-frequency
detail you just destroyed with *organic* high-frequency detail. Doing it the
other way round blurs the grain and you get mush.

Alternate registers: a grain plate at **20–40% opacity in Overlay** for punchy
cinematic, or **20–40% Soft Light** for gentler. A final softening pass of
0.3–0.8px. Add **slight halation on highlights**. Add subtle chromatic
aberration only if you specifically want a phone-sensor look.

### Pass 4 — match to a hero still

Pick one frame from the strongest shot in the film. Match every other shot to
it: shadow tint, highlight warmth, saturation, contrast. **This is what makes
separately generated clips read as one film**, and it is the pass most often
skipped.

The colour script (`lighting.md` §7) tells you which still to pick, and where
the film is *supposed* to change temperature rather than being corrected to
uniformity.

### The hard limit — state it so nobody wastes an afternoon

**Grain and blur fix texture. They cannot fix motion artefacts or anatomical
errors.** A morphing hand is a regeneration, not a grade note. A floating walk
is a regeneration. Do not try to grade your way out of a bad take.

---

## 4. Motion imperfection

Generated camera motion is **too stable and too linear** — no micro-vibration,
no weave, no breath. Real camera movement has all three even on a dolly.

Add it in post rather than asking the model for it. The usable spec:
**shoulder-mounted, a real operator's breath, a constant fine 1–2cm tremor.**

Add subtle motion blur wherever camera or subject movement is unnaturally
sharp.

---

## 5. The speed pass

AI motion carries a **built-in slow-motion bias**. This is a training
artefact, not a prompting failure: the model minimises risk by minimising pixel
change per frame, so "slower is safer" for temporal consistency and it defaults
there whenever motion specificity is missing.

If the finished cut drags, run the whole film **10–15% faster** and watch it
again. This is usually a bigger improvement than any individual reshoot.

At the prompt end, the fix is to **speed-encode the verb rather than adding an
adverb** — "walks" becomes "strides", "hurries", "rushes"; "moves" becomes
"darts", "sweeps", "charges" — and to add environmental consequence (dust
trailing, a coat snapping) so the model infers speed from evidence.

---

## 6. Sound

### Layer order

**Dialogue → foley → ambience → score.** Built in that order, mixed in that
priority.

### Levels

| Element | Peak dB | Notes |
|---|---|---|
| Dialogue / narration | **−18 to −9**, target **−12** | the dialogue never moves |
| Sound effects | −10 to −20 | |
| Foley and ambience under dialogue | −15 to −25 | |
| Music as primary element | −18 to −22 | |
| Music under dialogue | −30 to −35 | |

Delivery loudness: dialogue **−20 to −26 LUFS**; ambient around −30 LUFS.

**The rule that survives all the unit confusion: music sits 12–20 dB below
dialogue, ambience 10–15 dB below dialogue, and the dialogue never moves.**

### EQ for synthetic voice

AI-generated speech has a characteristic thin, brittle signature. Five moves
fix most of it:

- **High-pass at 80 Hz** — removes synthetic low rumble
- **Boost 150–300 Hz** — warmth, where AI voice is characteristically thin
- **Boost 1–2 kHz** — clarity
- **Cut 6–10 kHz** — softens synthetic harshness and sibilance
- **Compress 3:1 to 4:1**

And one that matters more than all of them: **a light room reverb, shared
across every line.** The absence of a room is a major tell, and a single shared
reverb also glues together lines that were generated separately. Keep it light.

### Room tone across the seams

Lay one continuous ambience bed under the whole film so the room does not
restart at every cut. Separately generated clips each carry their own implied
acoustic; a shared bed is what hides the difference.

### Native model audio

Usually a liability, with real exceptions.

- **Keep it** for ambience where the model is good at it, and **always as a
  temp track** — even bad native audio tells you where the beats landed.
- **Keep it** for any sound synchronised to motion the model actually rendered:
  an impact, a footfall, a door. No separately generated effects bed will match
  that sync.
- **Replace it** for anything else. It is thin because models compress the
  audio branch heavily, prioritising compute on pixels — reduced frequency
  depth, inconsistent room tone, flattened dynamics.
- Even when keeping it, **run compression and low end into it.**

Two prompt traps: **never describe background music in a video prompt** — it
generates at excessive volume and cannot be unmixed. And expect some models to
burn in subtitles; inspect for them.

### Direction for the voice model

- **Stability 35–45%** is the single most important control. Lower is more
  expressive; higher is flat and robotic. **Most amateur output is
  over-stabilised.**
- Similarity 70–85%. Style exaggeration 0–10%. Speaker boost on.
- **Punctuation is performance notation** — ellipses for hesitation, em-dashes
  for rhythm breaks, capitals for emphasis, full stops for hard landings.
- **Break long passages into sections and generate them separately.** This
  directly addresses the flat metronomic "TTS plateau" cadence, because each
  chunk gets its own arc.
- Spell out numbers. No emoji, no special characters.

---

## 7. Titles

**Every word on screen is typeset in the edit. Never generated.** Models mangle
lettering, and non-Latin scripts come back as convincing-looking nonsense. This
is not a preference; it is the only reliable route.

That includes titles, credits, signage that must be readable, subtitles, and
any diegetic text the story depends on. If a shot needs unreadable background
text, generate it; if it needs *readable* text, composite it.

---

## 8. The finishing checklist

Watch the whole film once, start to finish, against this list. Every item is a
named tell.

**Texture**
- [ ] No plastic or waxy skin — is there grain, is there a blur pass
- [ ] No repeating texture tiling across large surfaces
- [ ] No gibberish text anywhere in frame
- [ ] Reflections agree with the scene geometry

**Face**
- [ ] Characters blink, at natural intervals
- [ ] Eyes carry a catchlight
- [ ] No black void mouths
- [ ] No face drift within a shot — the character at the end is the character
      at the start
- [ ] Lip closure on b, p, m consonants

**Motion**
- [ ] Nothing glides without weight or contact settling
- [ ] No limbs or cloth bending past natural limits
- [ ] No action completing faster than its clip
- [ ] Camera motion has weave, not machine-smoothness
- [ ] No background extras with impossible gaits

**Light and grade**
- [ ] Every scene has a direction of light, not "pleasant cloudy afternoon"
- [ ] Saturation tamed; no deep-fried reds and teals
- [ ] Shadows and colour temperature agree across cuts within a scene
- [ ] Every shot matched to the hero still

**Cut**
- [ ] Average shot length on target; no face held past six seconds
- [ ] Cuts land on motion, not at rest
- [ ] Screen direction consistent
- [ ] No two adjacent shots from within 30° of each other

**Sound**
- [ ] One continuous room tone under the seams
- [ ] One shared reverb across all dialogue
- [ ] Music 12–20 dB under dialogue and staying there
- [ ] Nothing in the mix competing with a spoken word
