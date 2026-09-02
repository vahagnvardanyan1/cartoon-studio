# Lighting

The most under-specified thing in an AI-generated film, and the one that most
reliably makes it look cheap.

The characteristic tell has a name: **"pleasant cloudy afternoon everywhere"**
— every subject lit identically, diffuse, no motivated key, no direction, no
shadow with a shape. A model given no lighting instruction defaults to it,
because it is the safest average of everything it was trained on. Lighting is
therefore not a finishing touch in this pipeline. It is a thing you must state
or lose.

---

## 1. State the source, never the mood

The single most useful substitution in the whole handbook:

> ❌ "dynamic cinematic lighting"
> ✅ "Overcast 6000K daylight through fog as key, soft and directionless.
>    Headlights as the only warm practical."

Vague adjectives do not remove a decision from the model. They hand it over.
A prompt only carries what is written into it; everything left out still gets
decided, just by the model instead of by you.

For every shot, name four things:

1. **The source** — sun, window, fire, lamp, open door, sky
2. **Its direction** — relative to the camera, in words a model can act on
3. **Its quality** — hard or soft, and what makes it so
4. **Its colour** — in Kelvin or as a named condition

---

## 2. Three-point, and the ratio that carries the drama

- **Key** — the primary source, the one that defines the character. Typically
  **45° off the lens axis** in plan, elevated **30–45°**. It sets the shadow
  pattern and therefore the mood.
- **Fill** — opposite side of the lens from the key, near lens height, opening
  the shadow side. **25–45% of key for a cinematic look; 85–95% for polished
  commercial or comedy.**
- **Back / rim** — behind and to the side, conventionally on the key side aimed
  back toward the fill side. It offsets the flattening the key and fill cause.
  **Rim is the difference between a subject *in* a space and a subject pasted
  onto one** — and in a generated pipeline it is the cheapest single
  instruction that stops a character looking composited.

### Key-to-fill ratio

Ratio = (key + fill) : fill. Each stop is a doubling.

| Stops | Ratio | Look | Says |
|---|---|---|---|
| 0 | **1:1** | flat, near shadowless | safety, honesty, comedy, children's, clinical |
| 1 | **2:1** | soft defined shadows | naturalism with dimension. Drama default |
| 2 | **4:1** | strong shadows, striking highlights | heightened drama, moral ambiguity |
| 3 | **8:1** | stark, half the face gone | noir, horror, threat, concealment |
| 4+ | **16:1+** | silhouette territory | menace, anonymity, the unknowable |

**Genre shorthand:** comedy 1:1–2:1 · drama 2:1–4:1 · noir and horror 8:1+.

**Genre is carried more by ratio and hardness than by colour.** Pick the genre,
then the ratio and hardness, then the palette — in that order.

---

## 3. Hard and soft

Quality is set by **apparent source size relative to the subject**. A big
source close is soft; a small source far is hard. The sun is enormous and 93
million miles away, so it is hard; a cloud layer is a huge near source, so it
is soft. The diagnostic is the **shadow edge**: sharp is hard, gradual is soft.

- **Hard** — high contrast, sharp-edged shadow *shapes*, directional, and it
  **reveals texture** at raking angles: pores, stubble, dust, weathered wood.
  Implies exposure, judgement, harshness, age, guilt. *In a generated pipeline
  hard raking light is also the most effective single defence against plastic
  skin*, because it forces the model to render surface relief.
- **Soft** — low contrast, often sourceless, **conceals texture**. Implies
  youth, innocence, memory, safety, romance. Overuse of soft light is half of
  why AI footage looks waxy.

**Inverse square law, with numbers:** intensity = 1/d². A 1K open-face gives
1,000 fc at 4 ft and 250 fc at 8 ft — a 75% loss for a doubled distance. The
consequence is a *blocking* constraint: a big source far away gives an actor a
wide zone of even exposure; a small source close forces exposure to change with
every step.

---

## 4. Direction

- **Frontal / on-axis** — flattens, erases modelling, hides texture. Exposed,
  interrogated, or (soft) idealised. News and beauty use it; drama avoids it.
- **3/4 front (~45°, the standard key)** — most modelling for least mystery.
  Produces the named patterns: **loop** (a small nose-shadow loop on the
  cheek), **Rembrandt** (a lit triangle on the shadow cheek under the eye),
  **butterfly** (source high and on-axis, symmetrical shadow under the nose —
  glamour).
- **Side / split (90°)** — half lit, half dark. Duality, secrecy, a character
  with two faces.
- **Back / rim** — separation, halo, sanctity or menace depending on fill.
  Full backlight with no fill is silhouette: anonymity, threat, archetype.
- **Under-light** — inverts every shadow the visual system expects. The primal
  wrongness cue. Motivated naturally by firelight, a screen, footlights.
- **Top light** — eyes go into dark sockets. Institutional, dehumanising.

### Motivated lighting

**Every light in a shot must have a diegetic parent, or the film must have
declared that it is stylised.** To motivate an instrument, match the source on
four properties: **direction, colour temperature, quality, intensity.** A
practical in frame must read as the *cause* of the key — exposed a stop or two
over key, without blooming.

Writing "motivated by the window camera-left" into a prompt does more work than
any amount of "beautiful lighting", because it forces the model to commit to a
direction and then be consistent with it across the frame.

---

## 5. Colour temperature and time of day

| Source | Kelvin |
|---|---|
| Candle | 1,900 |
| Household bulb | 2,800–2,900 |
| Tungsten | 3,200 |
| Sunrise / golden hour | 3,000–3,500 |
| Fluorescent | 3,500–4,300 |
| Moonlight | ~4,100 |
| HMI | 4,600–6,500 |
| Midday sun | 5,600 |
| Overcast | ~7,000 |
| Open shade | 9,000+ |

Sun elevation, which is what actually defines the named hours:

- **Golden hour** — sun +6° to −4°. Low, warm, soft, long raking shadows.
  Memory, nostalgia, grace, endings.
- **Blue hour** — sun −4° to −6°. **15–30 minutes only.** Deep blue, cold,
  saturated, near shadowless, with an orange gradient at the horizon.
  Melancholy, transition, the world before it wakes.
- **Civil twilight** — 0° to −6°. Objects still readable; skies run red through
  magenta to blue.
- **Nautical twilight** — −6° to −12°. Dark blue, horizon still readable. The
  true night-for-night window if you want any ambient at all.
- **Astronomical** — −12° to −18°. Silhouettes only.

**Night-for-night:** keep the ambient base low and *cool* — a moon key at
4,100–5,600K, usually gelled bluer than reality because audiences expect blue
moonlight — then let **warm practicals** carve the frame. The contrast between
cool ambient and warm practical is what makes night read as night rather than
as underexposure. Writing only "night" gets you underexposure.

**Midday** is top-heavy hard light with eye-socket shadows: cruelty,
exhaustion, bureaucracy, truth without mercy.

---

## 6. Lighting as continuity

Light direction is one of the three continuity classes that break the
audience's **spatial model** (with eyeline and screen direction), as opposed to
merely denting credibility. Fix it ruthlessly.

- **The key side must not flip between a shot and its reverse.**
- **Shadow length must agree with the stated time of day** across every shot in
  a scene.
- **Hold colour temperature constant across a sequence.** This is not only a
  continuity matter: lighting changes how a video model reconstructs a face, so
  a dramatic lighting change between shots is a documented character-drift
  trigger.
- Write the light direction into `canon.md` per location, per act, and paste it
  into every prompt. Like the axis of action, the model has no memory of it.

---

## 7. The colour script

Before any shot is generated, build a **colour script**: a strip of small
images, one per beat, mapping value, hue and lighting across the whole film.

Its purpose is stated best by Ralph Eggleston, who made Pixar's: it holds "the
emotional core of what we're trying to say visually with colour, value and
lighting." **A colour script is an emotional graph of the film rendered as
chroma and value — you should be able to read the story's arc from it with the
images too small to identify.**

Two practical consequences in this pipeline:

1. It is the artefact that stops every scene coming out the same temperature,
   which is the second half of why generated films look flat.
2. It gives the finishing grade a target. Pass 4 of the grade (see
   `finishing.md`) matches every shot to a hero still; the colour script is
   what decides which still.

Build it from the style key and the beat list, at thumbnail size, in one pass.
It costs one generation per beat and it is the cheapest structural decision in
the film.
