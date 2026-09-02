# Editing and pace

Researched September 2026, after a 60-second film came back "lazy and boring"
and the fault turned out to be structural, not cosmetic.

---

## 1. The number that matters

That film had **7 shots in 60 seconds — an 8.5 second average shot length.**

| | ASL |
|---|---|
| Hollywood studio era, 1930–60 | 8–11s |
| 1970s comedies (*Animal House*, *Freaky Friday*, *Hair*) | 4.5–4.9s |
| Contemporary mainstream | 3–6s |
| Action | ~4.0s |
| TV commercials | 1–2s |

We had cut a comedy at the pace of *Rear Window*. No amount of prompt craft
rescues that — it is boring before a single frame reaches an image model.

**And AI footage is worse than live action here.** Attention drifts on AI
motion at **6–8 seconds**, against 10–12 for filmed footage, because the motion
is unnaturally smooth and synthetic faces reveal themselves under sustained
attention. Every shot in that film was held past the point where the audience
starts noticing the machine.

### Targets

- **ASL 4.0–4.5 seconds.**
- **Hard ceiling of 6 seconds on any shot containing a face or continuous
  character motion.** One deliberate exception, at the end.
- **Vary shot lengths across a 1–8 second range.** Uniform shot length is
  itself a recognised AI-slop tell — a fast film cut to a metronome still
  reads dead.

### Shot count, derived

| Runtime | Shots |
|---|---|
| 45s | 12–14 |
| 90s | 20–24 |
| 3 min | 40–45 |

If the shot count for a runtime is materially below this, stop and re-plan.
The problem is not fixable later.

---

## 2. The descending ladder

Shot length should **shorten beat by beat** through an escalating story, then
break the pattern once at the end. A worked example from a 27-shot,
108-second film:

| Beat | Shots | Avg | Function |
|---|---|---|---|
| Setup | 4 | 5.3s | establish, plant the faces |
| First escalation | 5 | 4.0s | inserts arrive, close-ups start |
| Acceleration | 6 | 3.0s | close-up dominant, cut on action |
| Peak | 10 | 2.4s | inserts, reactions, repetition-with-variation |
| Button | 2 | 5.0s | the only shots that slow down |

Two refinements that matter more than the average:

- **Contrast beats speed.** Hitchcock's shower sequence alternates long and
  short. Pure uniformity at any tempo goes numb.
- **One deliberate slow passage inside the fastest beat** is worth more than
  another round of quick cuts. On one production a formal, ceremonial passage
  ran at 5 seconds a shot in the middle of a 2.4-second sequence, and the
  violence afterwards landed harder because of it.

---

## 3. Generate long, cut short

Documented production data from a 3-minute AI-animated episode:

- **164 generations → 41 final clips.** ~25% selection rate.
- **~3 generations per usable shot** on average; some need 8+.
- **~5 usable seconds out of each 15-second generation.**
- **Over 40% of finished shots were composites** — the best seconds of two or
  more generations of the same prompt stitched together.

### Rules

1. **Generate every clip longer than the cut needs.** A shot cut at 2.5s should
   still be generated at 6–8s. There is no way to extend later, and there is
   always a better two seconds somewhere in a longer take.
2. **Budget shots × 3 for generations, × 4 for comfort.** A 22-shot film is
   ~66–88 generations, not 22.
3. **Expect to Frankenstein.** Roughly a third of finished shots will be
   assembled from fragments. Plan for it rather than treating it as failure.
4. **Do not ask one generation to contain a montage.** A documented review
   caught a prompt scripting "18 cuts in 15 seconds" that exceeded the model.
   One shot per generation.

---

## 4. Coverage

A scene stays alive because there is somewhere to cut to. For every beat,
the standard order is: master → progressively tighter singles on A →
reverse on B → inserts and cutaways. A simple two-hander is ~8 setups.

**Budget for a 22-shot film:**

| Type | Count |
|---|---|
| Establishing | 1 |
| Medium | 5–6 |
| Close-up | 6–7 |
| Extreme close-up | 2–3 |
| Insert / cutaway | 3–4 |
| Dedicated reaction | 4–5 |

**If fewer than four shots are pure reactions, comedy will underperform.**
Laughter more often comes from the reaction than the punchline, and a reaction
close-up is also the cheapest, most reliable, least artifact-prone shot an AI
model can produce. Plant the reaction face during setup so the payoff has
somewhere to land.

**Coverage tightens as stakes rise.** Each rung of an escalation should be
framed closer than the one below it.

---

## 5. Cut on action — and why it matters more here

Start a movement in shot A, complete it in shot B. The motion hides the cut.

For AI assembly this is not a nicety, it is structural: the continuity breaks
between separately generated clips are large and constant — lighting shifts,
small design drift, changed grain. **A cut placed on a strong movement is a cut
the viewer's eye does not audit.** Put every swing, throw, door-slam and fall
on a cut.

Corollary: if a subject exits frame in A and enters in B, the entrance must
match the exit's screen direction and rhythm.

---

## 6. Screen direction across separately generated clips

The model has no memory of your geometry, so the geometry goes in the text of
**every** shot prompt: "the shop on the RIGHT of frame, the lane running off
to the LEFT, he enters from the LEFT."

Two practical notes learned the hard way:

- **Check what the model actually produces before enforcing your spec.** On the
  one production film five frames had independently agreed on shop-right, and
  the written spec was the outlier. The majority was the better composition.
  Adopt it and rebuild the one frame that disagrees.
- **Cross the line only on a strong movement**, or via a neutral head-on shot
  or an insert with no screen direction.

---

## 7. Accelerating a comic escalation

- Progressive shortening of shot length — the descending staircase above.
- **Match cut / cutting on action** — the invisible accelerator.
- **Smash cut** — hard cut from loud and busy to quiet, or the reverse.
- **Repetition with variation** — repeat a framing exactly, change one element.
  Cheap in AI: one prompt, one variable swapped, gives a rule-of-three run.
  A catalogue of objects being snatched up reads as three identical insert
  framings with three different objects in them.
- **Hold on a reaction** — the one place to exceed the ASL ceiling.
- **Perceived pace is about how fast plot arrives**, not only cut rate. A fast
  cut over a static idea still reads slow.

Professional comedy editors work to **six frames — a quarter of a second.**
Cut tight, almost clipping the end of the punchline.

---

## 8. Post, always

Three passes that separate finished from generated:

1. **One colour grade across every clip.** This is what makes separately
   generated shots read as one film. Non-negotiable.
2. **Film grain at 10–15% opacity.** Kills the plastic-skin tell.
3. **Speed up 10–15%.** AI motion has a built-in slow-motion bias. Never ask
   for slow motion unless it is a gag — and never slow a clip down to fit
   audio, which is exactly the mistake that made the first film worse.

---

## 9. The slop checklist

Hold every prompt and every assembled cut against this.

**Structural**
- Every shot centre-framed and eye-level → at least four distinct compositions
- All shots the same length → vary 1–8s
- One static idea per shot → give each a beginning and end state
- Single camera angle throughout → named failure mode, "breaks momentum"
- No reaction shots → four minimum
- Lighting or background physics shifting between cuts → fix at the reference
  layer, then grade

**Motion and image**
- Unnaturally smooth camera → add gentle shake, speed-ramp 10–15%
- Plastic skin → grain
- Flat uncanny lighting → name the light source and its direction
- Hand morphs → frame hands deliberately or compose them out
- Gibberish in-frame text → forbid text in every prompt, overlay real text
- Repeating texture tiling → choose varied surfaces
- Background extras walking on one leg → keep crowds simple

**Audio**
- Metronomic TTS with no breath → generate each line separately, direct it
- Missing room tone → the most common amateur giveaway; every shot needs a bed
- Music chosen by keyword rather than emotional fit

---

## Murch's Rule of Six — the priority order for any cut

| | Criterion | Weight |
|---|---|---|
| 1 | **Emotion** — does the cut preserve what the audience should feel here? | **51%** |
| 2 | **Story** — does it advance the story? | **23%** |
| 3 | **Rhythm** — is it rhythmically right? | **10%** |
| 4 | **Eye-trace** — does it respect where the eye is looking? | **7%** |
| 5 | **Two-dimensional plane** — 180° rule, screen direction | **5%** |
| 6 | **Three-dimensional space** — the physical geography | **4%** |

**"If you have to sacrifice certain of those six things to make a cut,
sacrifice your way up, item by item, from the bottom."** A cut that is
emotionally right survives a spatial violation; a spatially perfect cut does
not survive being emotionally wrong.

If a cut fails only on 4, 5 or 6 — make it. If it fails on 1 or 2, find a
different cut however clean the geography.

In a generated pipeline the temptation is to cut where the footage is
cleanest. **The footage is not the criterion.**

---

## Hold times, specifically for generated footage

| Shot type | Hold |
|---|---|
| Opening shot | 2–4s |
| Character close-up | 2–5s — static AI faces become a problem around 4s |
| Medium | 3–6s |
| Two-shot with interaction | 4–8s — attention is distributed, so faces get less scrutiny |
| Action | 2–4s |

**Artefacts become visible at 6–8 seconds in generated footage versus 10–12 in
filmed footage.** And the observation that matters most: **hyper-smooth,
artefact-free motion itself triggers conscious awareness of synthetic origin
when held too long.** You cannot fix that by generating better. Only by cutting
sooner.

Shot size sets a *floor* as well as a ceiling: a wide needs about two seconds
for the audience to read it; a close-up can live at half a second. If your
average shot length is dropping, your framings must be tightening, or the
audience is being starved.

---

## Frankenstein editing

**Most shots are not one shot.** Over 40% of finished shots on documented
productions are stitched from two or more generations of the same prompt.

1. **Over-generate with variation** — same prompt, small changes to seed,
   phrasing or reference.
2. **Mine fragments.** Scrub every generation marking *usable seconds*: the
   half-second eyeline that works, the two-second hand move, the lighting beat.
   You are not looking for a good take. You are looking for good seconds.
3. **Hide the seams** — cut on action, on a sound effect, on a whip, or under
   an audio bridge.

---

## Hiding the drift

The principle: **give the audience a point of concentration that is not where
your cut is most evident.**

- **Cut mid-motion, never at rest.** Artefacts read at rest and vanish in
  motion. Place the cut at the strongest motion moment available.
- **Occlusion wipes** — let something cross frame and cut behind it.
- **Whip pans** — the frame is already destroyed by motion blur, so it will
  carry any join.
- **Audio bridges** — carry sound across the cut so the ear says "continuous"
  while the eye gets new pixels.
- **On an extended or chained clip, discard the first two frames** and put the
  cut at the strongest motion inside the overlap.

---

## Pacing is a curve, not a constant

Plot the target average shot length **per sequence** before cutting, then check
the actual curve after. Long breathing shots for setup and reflection,
contracting into rapid cutting at the climax, and one deliberate break in the
pattern at the end.

Uniform shot length at any tempo is itself a tell.

Two cue types drive the curve: **auditory** — cut on musical structure — and
**visual** — cut on movement inside the frame.

---

## L-cuts and J-cuts

- **L-cut** — picture cuts first, the outgoing audio continues over the new
  image. The audience is visually in the new place but still tethered to the
  last one. **Make this the default in dialogue coverage**: it lets you show
  the listener's reaction under the speaker's line, and the real moment often
  lives in the reaction.
- **J-cut** — the incoming audio starts before the picture cuts. Anticipation,
  or dread. Prepares the audience for the next scene before showing it.

Overlap lengths: start at about **half a second** for a dialogue split; up to
**two seconds** for a J-cut into a major sequence. The test: **if you can feel
the overlap but not see it, it is working.**

In a generated pipeline these do double duty — an audio overlap is also the
cheapest possible seam-hider.
