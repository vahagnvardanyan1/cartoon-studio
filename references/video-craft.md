# Video generation craft

Researched August 2026. Model names churn; the mechanisms below do not.

---

## 1. Why consistency is hard — the mechanism

Video models are **stateless**. They have no memory of the previous shot and no
3D understanding of the scene. Two consequences follow, and almost every
failure traces back to one of them:

- **Errors accumulate within a clip.** Drift scales with duration. Identity
  holds notably better under ten seconds.
- **The model cannot distinguish "the camera moved" from "the object changed
  shape."** That is why backgrounds melt and faces morph during camera moves.

The correct mental target is not pixel-identical characters. It is
**perceptual continuity** — the viewer recognises the character despite minor
variation. Character drift is unsolved on every platform; plan around it rather
than expecting to defeat it.

---

## 2. The consistency stack, ranked by what actually works

**1. Frame chaining.** Export the last frame of the previous clip; use it as
the start frame of the next. The single most reliable technique available, and
it beats every prompt-side method.

**2. Multi-angle reference sets, not single portraits.** A single portrait is
adequate only for short clips with little camera movement. Three or four angles
significantly improve stability across shots and expressions. Some models take
a whole grid of angles of one subject specifically to build spatial
understanding.

**3. Dedicated identity mechanisms** where the platform offers them — per-frame
identity injection, bindable character elements, reusable character assets.
These are the closest thing to a persistent character asset in a medium that
otherwise has none. Where two characters share a frame, look for a model that
lets you attach a *separate* reference to each, or their features bleed
together.

**4. A byte-identical identity string.** Write the character's description
once — age, build, face, signature clothing — and paste it into every prompt
**unchanged**. Any rewording gets reinterpreted as a new character. Only the
scene instructions should change between prompts.

**5. Environmental continuity.** Hold lighting colour temperature, camera
distance and background consistent across a sequence. Lighting influences how
the model reconstructs facial features, so a dramatic lighting change is a
documented drift trigger. In animation this is good news — you control the
lighting design absolutely.

**6. Short clips.** Cut before the model drifts rather than fixing drift.

**Seed is not an identity lock.** It reduces variance and gives you
reproducible takes. It does not pin identity on any current model.

---

## 3. Control mechanisms — know which your model has

- **Start frame** — universal, table stakes.
- **End frame** — widely available. Words alone will not restrain a camera
  move; an end frame will. Generate both frames as stills, then prompt only the
  move that connects them.
- **Multi-keyframe (more than two)** — rare and valuable. Where available it
  turns generation into timeline direction rather than interpolation between
  two poses.
- **Reference images** — counts vary enormously between models. More is not
  automatically better; **relevance and angle coverage matter more than
  quantity**.
- **Reference addressing** — some models let you address references inline and
  assign each one a job. Use it. An unlabelled reference bleeds its lighting,
  framing *and* pacing into the shot when you only wanted its motion. Write
  the equivalent of `reference 1 = character identity only`,
  `reference 2 = camera movement only`.
- **Camera presets** — where a platform offers named camera moves, prefer them
  to prompt phrasing. Prompt-language camera control is probabilistic; presets
  are not.
- **Region editing** — the ability to fix one span or one element without
  regenerating the whole clip. This is the closest thing the medium has to a
  "small fix", and it is worth choosing a model for.
- **Motion transfer and pose control** — drive a character with a reference
  performance rather than describing the performance in words.
- **Video extension** — continue an existing clip rather than cutting.

**Governing principle:** *text is for spatial decisions; references are for
identity and temporal decisions.*

**No single model has the whole control stack.** A sensible pipeline uses a
control-rich model for blocking and a quality-rich model for finals.

---

## 4. Prompt structure

Every serious guide converges on roughly the same slots:

```
[Camera] [Subject] [Action] [Context] [Style and ambiance]
```

Two things matter more than the slot order.

**Instruction adherence decays by position.** The first two or three
instructions land almost every time. A prompt carrying eight requirements
typically honours four or five, apparently at random. **Keep the active
creative payload short — roughly 60 to 100 words — and front-load what matters
most.**

**But state should be verbose.** Feature-scale productions run prompts of
several thousand words, and the apparent contradiction resolves cleanly: that
bulk is **state re-declaration and hard rules**, not additional creative
instructions. Because the model has no memory, every generation re-declares:

- Each character's current state — clothing, condition, what they are holding
- Continuity from the previous shot
- Geometric staging — who is where, facing which way
- The hard rules and prohibitions

Keep active instructions few. Keep state complete.

**Timed beats are the highest-leverage single technique.** Break the shot into
two- or three-second spans, each with its own verb and consequence:

```
0-2s  <verb + physical consequence + micro-expression>
2-4s  <verb + physical consequence + micro-expression>
4-6s  <verb + physical consequence + micro-expression>
```

Without this, a model given one vague action and eight seconds will idle.

**One camera move per clip.** Stacking moves produces jitter, drift and ugly
splits. If a sequence genuinely needs two moves, mark the cut explicitly.

**For image-to-video, do not re-describe what is already in the image.** Spend
the whole prompt on motion.

**Describe physics explicitly.** Models do not infer implied physical behaviour
— how cloth falls, how a struck object reacts, where debris goes.

---

## 5. Negative prompting — model-dependent, and a real trap

- Some models offer a **dedicated negative field**. Bare keyword lists work
  there.
- Others have **no negative field at all**. In those, a bare keyword list can
  be **rendered as subject matter** — asking for "no snow" can produce snow.
- For any model without a dedicated field, use **grammatical prohibition** ("a
  landscape with no buildings") or, better, **describe the desired positive
  state** instead.

Positive phrasing is the safer default everywhere: write "locked camera", not
"no camera movement".

**Check whether your model has a negative field before writing AVOID lists.**
If it doesn't, convert them to positive descriptions.

---

## 6. Failure modes and what to do

| Failure | Cause | What actually helps |
|---|---|---|
| Character drift between shots | Statelessness | Frame chaining, multi-angle refs, identical identity string, clips under 10s |
| Drift *within* a clip | Error accumulation over duration | Shorter clips; cut before the drift |
| Melting backgrounds, morphing | No 3D understanding | One camera move; camera presets over prompt phrasing; simple reference backgrounds |
| Only some instructions honoured | Adherence decays by position | Fewer active instructions, front-loaded |
| Reference bleeds unwanted qualities | Unassigned reference role | Give every reference one explicit job |
| Characters look like cardboard cutouts | Reference strength at maximum | Reduce it; leave room to adapt to new light and pose |
| Prop detaches from the hand | Start frame showed the wrong state | The keyframe must show the state beat one begins from; write an explicit attachment rule; give the release a reason |
| Hands | Universal weakness | **Design around it.** Stylised hands are far more forgiving than photoreal ones. Avoid shots where a hand manipulates a small object as a story beat |
| Garbled on-screen text | Still unreliable in video | **All text, titles and logos in post.** Non-negotiable |
| Multi-character staging falls apart | The hardest documented case | Stage so only two characters share a frame; per-character reference attachment; expect many iterations |
| Failed generations cost real money | Iteration, not generation, is the cost driver | Draft tiers; select; finish only the winners |

---

## 7. Stylised animation specifically

Public benchmarks for stylised-3D-cartoon and anthropomorphic characters barely
exist — most "best for animation" comparisons silently substitute *image*
models for video models. Treat all rankings in this area as directional and
**run your own bake-off**.

A three-shot protocol settles in a day what the literature cannot answer:
a close-up, a full-body action shot, and a multi-character interaction, using
your actual character designs, generated on each candidate model and scored
blind.

Two genuine advantages of the stylised register worth exploiting:

- **Hands are much more forgiving.** Simplified cartoon hands sidestep the
  medium's most persistent weakness.
- **You control lighting absolutely**, which is one of the strongest levers on
  identity stability.

---

## 8. Finishing

**Raw generation is never the final picture.** Every independent source lands
here. Colour, stabilisation, artifact cleanup and compositing are pipeline
stages, not cleanup.

**Expect to composite.** A large share of final shots on documented
productions are stitched from multiple generations plus other elements. Assume
it is normal.

**Upscaling — architecture matters more than brand.** Upscalers trained on
real degraded footage sharpen what is already there, which *amplifies the
temporal flicker inherent in generated video*. Diffusion-based upscalers treat
the job as conditional generation and invent plausible texture that matches the
distribution of generated footage. **For AI-generated stylised content, use the
diffusion family**, and run it at low restoration strength or it over-sharpens.
Some upscalers are purpose-built for animation and process frames independently
to avoid smearing cel-like content.

**Order matters: upscale first, then interpolate frame rate.** Interpolation
smooths motion; it does not sharpen pixels.

**Track provenance shot by shot** back to source materials. Required for chain
of title, and increasingly required by platforms that will distribute the work.

---

## 9. Economics

- **Iteration is the cost driver, not generation.** Draft cheap, finish
  expensive. Use whatever draft or fast tier the model offers.
- **Expect several takes per shot**, and many more on complex multi-character
  staging. Budget the aggregate, not the per-shot number.
- **Selection is the craft.** Generate wide, then let a human cut.
- **Verify prices at the endpoint you will actually bill against.** Published
  per-second figures for the same model vary by an order of magnitude across
  secondary sources.
- Some models charge *less* when supplied with reference video, and some
  include audio whether you ask for it or not. Read the pricing carefully —
  the intuitive assumptions are often wrong.

---

## 10. Why clips drift — the mechanism, and the numbers

Drift is not bad luck. It has a published mechanism with two components:

- **History forgetting.** The mutual information between the current output and
  the preceding frames decays. The model loses the context that defined the
  shot — including the instruction. "Pan left" gets forgotten in favour of
  whatever pixel pattern now dominates the recent frames.
- **Temporal degradation.** Quality falls as the *cumulative sum of per-step
  errors*, compounding from noise initialisation, score estimation and
  discretisation. A small mistake in frame 50 is a bigger one in frame 51.

Onset is generally **past five to ten seconds**, earlier under load. Reported
thresholds worth planning against:

- **Character drift begins around shot 4–5** in complex scenes with four or
  more speaking subjects.
- **Lip-sync degrades on sentences over ten words**, worst at phrase endings.
- **Multi-clip consistency degrades past thirty seconds** on most models.

The paper's own finding — *incorporating more past frames monotonically
alleviates history forgetting* — is exactly why the production answer is
**keyframe anchoring**: chunk the shot and anchor each chunk to a ground-truth
frame rather than letting the model free-run.

**The practical consequence: the first and last second of every generation are
the worst, for different reasons.** The head carries initialisation artefacts —
discard the first two frames of any extended or chained clip. The tail carries
accumulated drift and history loss — it is where faces morph and backgrounds
reorganise. **Generate fifteen, use five, from the middle.**

---

## 11. Reference slots — allocate them deliberately

Where a model takes multiple reference images, an unallocated set wastes them.
A working scheme for four slots:

| Slot | Content | Anchors |
|---|---|---|
| 1 | hero portrait, frontal | identity. Locked at project start, reused verbatim forever |
| 2 | three-quarter, 45° rotation of the same character | identity under rotation |
| 3 | wardrobe close-up | colour and texture |
| 4 | the previous shot's final frame | lighting continuity |

**Angular diversity is the requirement.** Two or three references at similar
angles produce poor results; close-up plus full body plus side profile
eliminates drift by the third shot.

Keep reference strength **below maximum**, or characters go stiff and cannot
adapt to new light or pose.

---

## 12. Seeds

Same seed plus same prompt plus same settings gives the same output. In video
the seed influences **motion patterns and temporal coherence across the whole
clip**, not just the first frame.

The workflow: find a good result, record its seed, lock it, then **change
exactly one variable at a time.** Four to eight random seeds for exploration;
two or three targeted seeds for production refinement.

**A seed is not an identity lock.** It reduces variance and gives reproducible
takes. It does not pin a character across shots on any current model.

---

## 13. The drift audit

Score every generated shot against the character sheet, 0–10 on six checks:

1. face shape
2. hair length and parting
3. eye colour
4. wardrobe hue
5. the distinguishing detail — the scar, the earring, the continuity mark
6. body proportions under motion

**Accept at 7. Below 6, regenerate changing one variable — not the whole
prompt.** Rewriting the whole prompt loses the information about what was
already working.

If the same check fails twice across different shots, the fault is in the
reference, not the prompt. Stop generating and rebuild the sheet.

---

## 14. How many generations a shot actually takes

Plan against these. They are the difference between a budget and a hope.

| Situation | Generations per usable shot |
|---|---|
| Controlled, reference-anchored, storyboarded | **~3**, ~25% selection rate |
| Hard shots — complex staging, multiple characters | **~10** |
| Uncontrolled, comedic, dialogue-heavy text-to-video | **~20** (~5% hit rate) |

Documented productions, for scale: a three-minute episode ran **164 clips
generated to 41 in the final cut**; a national-broadcast advert ran **300–400
generations to 15 usable clips**; a ninety-second short took roughly 400
generations.

**Over 40% of finished shots on documented productions are stitched from two or
more generations.** Treat composite shots as normal, not as failure.

**Frames-first is roughly 3× cheaper than prompt-first** per finished clip,
because you are not burning video credits to discover composition. Approve
every start frame before spending a video credit.

**Text-to-video is still right** for exploration where you do not yet know what
the shot is, for abstract material with no fixed subject, and when you
specifically want the model's motion invention rather than your own.
