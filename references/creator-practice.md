# What working creators actually do

Field data from creators and studios who ship AI film that does not read as
slop. Gathered from their own breakdowns, newsletters, festival interviews and
one fully open-sourced feature production. Where they disagree, the
disagreement is recorded rather than averaged away — it is usually more useful
than the consensus.

---

## 1. The curation ratio — the number that matters most

**If a pipeline assumes one generation per shot, it is modelling amateur
practice.**

| Production | Generated → used | Ratio |
|---|---|---|
| 95-min feature, first 25-min segment | 16,181 → 253 shots | **64:1** |
| National broadcast advert | 300–400 → 15 clips | **~20:1** |
| Commissioned music video | 700 → 55 | **12.7:1** |
| 45-second trailer | 310 → 44 | **7:1** |
| One 90-second dialogue scene | ~150 generations | — |
| One character's face, locked | ~400 prompts / 1,600 images | — |

**Nobody credible is under about 7:1. Narrative work with characters runs
20–65:1.** The ratio scales with how much you are asking of the shot: a
landscape is cheap, a character speaking is not.

Budget the aggregate across the film, not the per-shot number, and tell the
user the real figure at the plan stage. A production planned at three attempts
per shot will run out of credits at shot nine and the user will think something
went wrong.

Two corollaries the same sources give:

- **Generate longer than you need, always.** One 48-hour-challenge finalist:
  generate ten seconds even when the cut needs three, "because you can salvage
  a usable portion from an otherwise broken animation."
- **Batch prompt-writing in fives.** From an agency practitioner: *"I always
  tell it to return 5 prompts at a time — any more than that and the quality
  starts to slip."*

---

## 2. What the good ones all do

Eight practices that appear across independent, unconnected creators. These are
the ones worth treating as rules.

### 2.1 They finish the story before generating anything

One 48-hour-challenge finalist spent **all of day one on the outline with zero
footage generated**. A feature-scale creator wrote a story bible with an
invented alphabet before any image. A serialised showrunner wrote **five
seasons** before producing episode one. The maker of the trailer that defined
the genre laid **music and text on the timeline within the first hour, before
generating a single frame.**

Amateurs generate first and look for a story in the pile.

### 2.2 Music and edit rhythm come first

> *"I can't stress enough how important it is to start with the music."*

The rhythm of the film is decided before the pictures exist, and clip motion is
then beat-matched to musical cues. A serialised creator works in **30–40 second
near-final blocks** — generating, animating and editing simultaneously —
specifically to protect pacing, rather than generating everything and
assembling at the end.

This is the same argument as the animatic, arrived at independently.

### 2.3 Image-first, never text-to-video

Near-universal. Originate a still, approve it, then animate it. The still is
where you win composition, lighting, character — and, per one feature-scale
creator, **about 90% of the final grade is already baked into the source
images** before anything moves.

The one deliberate exception is a director making surreal work who refuses
image conditioning on purpose, because he wants the model's invention. He is
making a different kind of object.

### 2.4 A locked style token block on every prompt

The 2023 trailer that started this used a fixed prompt spine where only the
subject changed. A festival entrant used **one style reference code for an
entire film**. The open-sourced feature put a **12-line technical preamble on
every single shot**: cinematography attribution, 8K photorealism, 180° shutter,
natural light only, a 60:30:10 colour ratio, pore-level skin, physics accuracy,
24fps, environmental audio only.

The variable is the subject. Everything else is constant.

### 2.5 Self-contained prompts

> *"Each prompt should fully describe the scene as if the model has no context
> of the shot before or after it."*

The open-sourced feature restates **character current state — injuries,
clothing, expression — in every single prompt.** Never assume continuity
carries. It does not.

### 2.6 Post is where the not-slop happens

The clearest statement in the field, from festival coverage:

> *"The gap between the finalists and typical AI video posted to social media
> is not primarily in generation quality — it's in editing, color grading,
> sound design, and pacing."*

Every serious creator runs a real NLE and a real grade. Not one of them
delivers raw generation.

### 2.7 They inject non-generated material

This is the practice most absent from naive pipelines and most present in
festival winners.

- A serialised creator **builds or buys the physical costume masks, photographs
  himself wearing them under real lighting**, and feeds those photographs as
  the reference instead of a text prompt.
- Another **performs every line himself to a webcam** and maps the performance
  onto his characters.
- Two studio directors shoot live-action plates on bluescreen and replace only
  the backgrounds.
- A festival winner built on **twenty-year-old archival photographs**.
- A feature-scale creator hires **real voice actors, a real composer and a real
  foley artist**.

The real element is load-bearing, not decorative. At one major festival, every
winning entry had injected something not generated.

### 2.8 They design the world around the model's weaknesses

- Cartoon aliens sidestep the uncanny valley; a retro VHS grade turns
  generation artefacts into a deliberate house style. **The constraint becomes
  the look.**
- A director replaced a gun with a stick so the restyled output kept a
  handmade quality.
- Another leans into the uncanny entirely, because fighting it produces the
  worst results.

When a model is bad at something, the professional move is usually to design
the shot so it is not asked — not to fight it with a longer prompt.

### 2.9 They already knew how to make films

The strongest single predictor in the data. Fifteen years of commercials. Ten
years of music videos. Film school plus a decade in production. An
Oscar-nominated director. A film school for AI reports that **95% of its
students already work in entertainment or advertising.**

> *"If you don't understand the basics, AI visuals look like student films."*

> *"AI doesn't replace filmmaking. It replaces the physical shoot."*

---

## 3. Where they disagree

Present these as choices, not rules. A pipeline that picks a side without
saying so is lying to its user.

| Question | One camp | The other |
|---|---|---|
| **Upscaling** | **Never.** One feature-scale creator refuses it outright: it exaggerates artefacts, oversharpens, and corrupts the aesthetic. | **Yes, selectively.** Others upscale twice — once early, once at the end — and a major AI film school teaches it as standard. |
| **Shot length** | Cut fast; artefacts surface at 6–8 seconds. | The open-sourced feature argues **15-second oners beat 2-second cuts**, because a long take *"mimics a real cameraman running through a village, which tricks the brain into forgetting the content is AI-generated."* |
| **Grids for character sheets** | *"You don't need to do the 3x3 grid for a character sheet. It actually hurts your consistency"* — use two high-res shots, close-up and wide, on off-white with soft light. | Other production workflows generate 2×2 grids at volume precisely to hold continuity. |
| **Newest model** | Chase the frontier. | One creator deliberately uses an **older version** of his image model on aesthetic grounds, and a festival entrant's lesson was *"our greatest breakthroughs come not from expanding our options, but from diving deeper with fewer tools."* |
| **Photoreal as the goal** | The open-sourced feature specifies "8K IMAX photorealistic, pore-level skin detail." | Festival evidence runs the other way: stylisation and restraint win, "funny but ugly" beat "beautiful but empty", and photoreal is a trap. |
| **Synthetic voice** | Used everywhere, and fine. | One creator uses **only human voice actors** for flagship work: *"real performers still bring something that's hard to replicate."* |
| **Structure before generation** | Front-load hard — script, boards, references, reel. | One Oscar-nominated director **skipped script, storyboard and treatment entirely** and went shot by shot. It worked for a three-day mood piece. Nobody makes ninety minutes that way. |

**How to use this table:** when a user's project sits near one of these
questions, name the trade-off and let them choose. The wrong move is to have a
silent default.

---

## 4. Techniques worth stealing outright

Each of these appears in three or more independent sources.

**Location plate → composite → reference.** Generate the empty location plate
first. Composite the character into it. Then use *that composite* as the
reference for every subsequent shot in that location. It carries geometry,
light and character in one image.

**Screenshot the last frame of the approved shot and use it as the reference
for the next.** The cheapest continuity mechanism that exists, and it is
universal among people who publish their process.

**Stress-test the location before committing to it.** *"The location isn't just
a background — it's a technical anchor that dictates the quality of the acting
the AI can perform."* A location the model renders badly will degrade every
performance staged in it, and you will misdiagnose it as an acting problem.

**Tight for dialogue, wide only to establish.** *"Stay tight with medium shots
and closeup shots for talking, it will look wayyyyy better than wide shots."*

**Do not crowd dialogue in a prompt.** *"If the dialogue is too crowded in a
single prompt, the AI tends to speed up the performance, leading to slop-like
movements."* Write deliberate pauses between lines.

**Break the action into explicit beats inside the prompt.** The open-sourced
feature uses **six beats for a fifteen-second shot**. It prevents the model
compressing or speeding up the performance.

**Never prompt for film grain.** Grain asked for in a prompt is **baked into
the pixels** and will not survive an upscale or a grade. Generate clean, then
add grain in post — using **scanned grain plates rather than synthetic**, in
Overlay or Soft Light.

**Highest resolution is not always best.** One practitioner on his image model:
**2K keeps the film grain; 4K is "too smooth" and "not that cinematic yet."**
Test rather than assuming the top setting wins.

**Low-poly 3D blocking for spatial truth.** Block the scene in Blender with
coloured shapes for characters, then hand that to an LLM to write the prompts
from. Solves staging and screen direction before any pixel is generated.

---

## 5. Prompt structure at feature scale

The open-sourced feature's prompts have a **median length of about 16,500
characters — roughly 3,000 words.** That appears to contradict the measured
100–150 word optimum, and it does not. The 3,000 words are almost entirely
**state**, not instruction. Their seven sections:

1. **Character current state** — injuries, clothing, expression, what changed
2. **Scene continuation context** — what just happened
3. **Shot intent** — the director's note; what this shot is for
4. **Geometry and staging** — positions, distances, who faces where
5. **Dialogue and sound effects**
6. **Action, broken into six beats** for a fifteen-second shot
7. **Key rules and prohibitions**

Only sections 3 and 6 are the active creative payload, and those stay short.
Sections 1, 2, 4 and 7 are facts, and facts do not compete for adherence the
way requirements do.

**Keep active instructions few. Keep state complete.** That is the whole rule,
and a feature production at 3,000 words per shot is obeying it, not breaking
it.

One documented failure of this structure is worth knowing by name: **"prompt
fatigue"** — a character reacting in the wrong emotional register because
section 1 underspecified their state, not because the model failed.

---

## 6. Project structure on disk

Thinly documented across the field, but what exists is consistent.

**One folder per scene.** The open-sourced feature used **108 scene folders**,
each holding that scene's prompts, keyframes, assets and canvases, with **every
generation record retained** — all 115,446 of them.

**Name files so they sort and survive being seen out of context:**

```
S01-SH02-Keyframe-V1-Review
S01-SH02-Video-V3-Approved
S03-SH01-FinalFrame-Reference
```

`Scene – Shot – AssetType – Version – Status`. An agency practitioner uses a
simpler variant: `14 - C - Quinn saying Hello` — shot number, variant letter,
what happens.

**Keep reusable references centralised and linked, never duplicated per shot.**
Characters, locations and props live in one place; shots point at them. A
duplicated reference is a reference that will drift.

**Do not overwrite the source before approval.** Keep the original and the
revision together with version numbers, and **record why a take was selected**
— that note is what makes a later reviewer able to trust the choice.

**Track derivation.** For every asset, which text, image or video produced it.

**Treat the character canon as read-only once references are locked.** Editing
it mid-production silently invalidates everything generated before the edit.

**Log the seed every time.** Without it a line or a shot cannot be matched
later, and matching is exactly what you will need after a picture change.

---

## 7. The tools that keep appearing

Worth knowing what serious workflows are actually built on — and note how much
of it is not AI.

**Not AI, and these carry the quality:** DaVinci Resolve for grade and finish ·
Adobe Premiere for edit · After Effects for cleanup and transitions · Blender
for low-poly previs blocking · a dedicated film-emulation plugin for grain,
halation and filmic colour response · scanned grain plates · Figma, Milanote or
Miro for the shot board · licensed music libraries, preferred over generated
music for anything client-facing.

**AI, at time of writing:** image models used as origination versus as
retouch — one creator's rule is *"no image starts in [the editing model], it is
just our Photoshop"* · a small set of video models chosen per shot type rather
than one for everything · dedicated lip-sync and performance-transfer tools ·
a music generator used as a first pass and then humanised · upscalers, if you
upscale at all.

The consistent shape: **many tools, each doing one job.** One creator reports
touching **fifteen to twenty-five different tools** across a single pipeline.

---

## 8. The two quotes to keep

> *"Most AI content is what people call 'slop.' The technology has a kind of
> default visual style, and if you just press the button and accept whatever it
> generates, you end up with generic sci-fi imagery that looks like everything
> else. It actually takes a lot of work to push the AI away from that baseline
> and impose a specific creative vision."*

> *"AI is not going to behave the way you want. It's like wet clay. You
> understand the medium, you know how to manipulate it, but it has a mind of
> its own."*

---

## A note on sourcing

The largest dataset here comes from a studio that open-sourced an entire
feature production — every prompt, keyframe and generation record. Its
engineering numbers are the best public data available. Its prestige claims are
marketing and were disputed by the festival it named. Treat the two
differently.

Several ratios are single-production figures rather than averages. They agree
with each other across very different productions, which is why they are
reported, but they are evidence rather than proof.
