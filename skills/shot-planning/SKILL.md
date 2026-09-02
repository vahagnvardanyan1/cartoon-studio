---
name: shot-planning
description: Break a story into a full shot list for animation, with camera, lens, lighting, action, dialogue, sound, duration and generation prompts for every shot. Use when reference art is approved, or when the user says "/shot-planning", "plan the shots", "make the shot list", "break this into scenes".
---

# Plan the shots

Turn the story beats into a complete shot list. This document is what the whole
generation stage executes, so it needs to be right before a single clip is
rendered.

Read `canon.md` and `assets.md`, then
`${CLAUDE_PLUGIN_ROOT}/references/cinematography.md`,
`${CLAUDE_PLUGIN_ROOT}/references/directing.md`,
`${CLAUDE_PLUGIN_ROOT}/references/lighting.md` and
`${CLAUDE_PLUGIN_ROOT}/references/editing-and-pace.md`.

---

## 1. Shot count comes first, and it is not negotiable

Before writing a single shot, compute the count from the runtime. **Target an
average shot length of 4.0–4.5 seconds.**

| Runtime | Shots |
|---|---|
| 45s | 12–14 |
| 90s | 20–24 |
| 3 min | 40–45 |

**No shot carrying a face or continuous character motion may exceed six
seconds.** Artefacts become visible in generated footage at 6–8 seconds against
10–12 in filmed footage — past that the audience stops watching the story and
starts noticing the machine. One exception, at the very end, where the length
reads as deliberate.

**Know that this is contested.** The directors of a published 95-minute AI
feature argue the opposite: that a **fifteen-second oner beats a run of
two-second cuts**, because a sustained take *"mimics a real cameraman running
through a village, which tricks the brain into forgetting the content is
AI-generated."* Both positions are held by people shipping real work.

The reconciliation, and what to plan against: **the six-second ceiling applies
to a held face.** A long take that keeps moving through space — where the
camera travels, the frame reveals, and no single face sits still in frame —
can run much longer, and one of those is worth more than four quick cuts. If
you want a long shot, earn it with motion, not with duration.

Raise it with the user when a beat could go either way rather than defaulting
silently.

If the plan comes out at seven shots for a minute, that is not a pacing
preference. It is a broken film. Re-plan it.

### The single-beat rule

**One action beat per 4–7 seconds of shot. A 10–15 second shot carries three
or four beats, maximum.**

Overloading a shot with several narrative changes degrades the output
measurably — multiple scene changes inside four seconds produce broken physics
and motion artefacts. This is a hard planning constraint, not a style
preference:

```
beats = floor(duration / 4), capped at 4
```

If a shot as written needs more beats than that, it is not one shot. Split it.
This single check prevents a whole class of mushy generation, and it is
cheapest to apply here, before anything is rendered.

Write the beats into the shot as timed spans, because that is also the format
the generation prompt takes:

```
0-2s  <verb + physical consequence + micro-expression>
2-4s  <verb + physical consequence + micro-expression>
```

### The descending ladder

Shot length shortens beat by beat through an escalation — roughly 5.5s in the
setup, 4.5 at the first turn, 3 in the middle, 2.5 at the peak — then breaks
the pattern once for the ending. **Vary lengths within each beat too.** Uniform
shot length at any tempo is itself a tell.

Put one deliberate slow passage inside the fastest beat. It is worth more than
another round of quick cuts.

---

## 2. Every scene must flip a value

Before the shots, write the beats. For each one, name four things:

- **Objective** — what the point-of-view character wants in this scene
- **Obstacle** — what resists it
- **Turn** — the moment direction changes
- **Value shift** — the charged pair that flips, with polarity:
  safe→endangered, together→alone, trust→suspicion

**A scene with no value shift should be strengthened, merged, or cut.**
Activity is not change. And **consecutive scenes must not flip the same value
in the same direction** — two scenes running hopeful→disappointed is one scene
written twice.

If you cannot name a scene's value shift, say so in the plan. That is a
finding, not something to paper over with better pictures.

---

## 3. Every shot carries a full camera block

**This is the part that decides whether the film looks professional.** "Camera:
push in" is not a camera decision. Four axes are independent and all four must
be named — size controls intimacy, height controls power, lens controls
credibility, movement controls attention.

Each shot in `shots.md` carries this, with no blanks:

```
SHOT      SQ0010_SH0020
JOB       <one sentence: what this shot is FOR>
SIZE      MCU
HEIGHT    shoulder, level
LENS      85mm
DOF       shallow; background falls off at 2m
MOVE      locked      (or: slow push in, landing on <X> as the line ends)
LIGHT     key 3/4 back camera-left, 4:1, hard, motivated by the window, 3200K
AXIS      A screen-left, B screen-right; line runs along the counter
DIRECTION he entered from frame left and stays left of her
IN-FRAME  <what the first frame is>
OUT-FRAME <what the last frame is>
DURATION  <seconds>
CAST      <who is in it>
PLATE     <which approved environment plate>
REFS      <which approved sheets this shot wires in>
CUE       <which voice line lands on it>
SOUND     <effects, atmosphere, what the score is doing>
CUT ON    <the movement the outgoing cut lands on>
```

**The JOB line is not decoration.** A shot that cannot state its job in one
sentence should be merged with its neighbour or cut — "shot list names angles
but not what each shot is for" is a named root cause of incoherent output.

**IN-FRAME and OUT-FRAME are not optional on any shot with a move.** Both ends
of a move must work as still images; the middle is transit. In this pipeline
that is literal — you will generate both as stills and let the model
interpolate. Words alone will not restrain a camera move.

### Choosing the values, briefly

- **Escalate the size ladder toward the turn.** The biggest close-up in a scene
  lands where the value flips.
- **Never cut adjacent rungs from the same position** (MS→MCU). Change angle by
  ≥30°, or change size by a full rung, or both.
- **Give a character a lens the way you give them a costume**, and change it
  when they change.
- **Move for one of five reasons only:** to reveal space, to follow, to build
  tension, to change emotional proximity, to mark a decision. Otherwise lock
  it off. A locked frame returned to twice is a rhyme; a film of drifting
  push-ins is a slideshow with ambition.
- **One primary move per shot**, with a speed word attached.

---

## 4. Coverage budget

Per 22 shots: 1 establishing, 5–6 mediums, 6–7 close-ups, 2–3 extreme
close-ups, 3–4 inserts, and **4–5 dedicated reaction shots.**

If fewer than four are pure reactions, comedy will underperform — and a
reaction close-up is also the cheapest and most reliable shot the models
produce. When the budget is tight, spend it here.

**Tight for dialogue, wide only to establish.** From an agency practitioner
who shoots a great deal of it: *"stay tight with medium shots and closeup shots
for talking, it will look wayyyyy better than wide shots."* The reason is
mechanical — a face at wide size is a small part of the frame, so the model
allocates it less detail and it drifts first. Establish the geography wide,
then go tight and stay there for the conversation.

For any scene between two people, the default coverage is: master, two-shot,
OTS A, OTS B, clean single A, clean single B, inserts, reactions. **Save the
drop from OTS pairs to clean singles for the turn** — it is the most reliable
coverage gesture in the language.

Coverage tightens as stakes rise. Each rung of an escalation is framed closer
than the one below it.

---

## 5. Screen grammar — decided here, not while generating

These are camera problems, not performance problems, and they matter more in
animation than live action because there is no incidental real geography to
orient the viewer.

- **The line.** Declare the axis of action per location in `canon.md`, and keep
  every setup on one side of it. Crossing it makes the audience feel the
  characters have swapped places. The five legitimate crossings are in
  `cinematography.md` §3.1.
- **The 30° rule.** Successive shots of the same subject move at least 30°
  around it, or the brain reads a jump cut.
- **Screen direction.** Exit frame right, enter the next shot frame left. In a
  chase, pursuer and pursued travel in the *same* direction — opposite
  directions read as collision.
- **Eyelines** must match in direction *and vertical angle*. If one character
  is short and the other tall, one single tilts up and the other tilts down.
  Failing the vertical is the most common eyeline error in this medium.
- **Silhouette.** Every key pose must read as a black shape. If it doesn't,
  restage it.

**Write the geometry into the text of every prompt in that location**, not just
the first. The model has no memory of it: "shop on the RIGHT of frame, lane
running off to the LEFT, he enters from the LEFT."

---

## 6. Never plan a two-shot in which two characters speak

Lip-sync takes one portrait per pass, and the video model will not move mouths
on its own — it ignores the instruction outright and returns closed faces.

Every exchange gets covered in **singles**: a wide for the situation, a single
on each speaker, and a two-shot only for the silent physical beat between them.
That is normal shot/reverse-shot coverage, it doubles the shot count in the
right direction, and it is the only structure that lets both voices be real.

---

## 7. Put the cut on a movement

Every swing, throw, fall, door-slam and hand-off lands on a cut. The continuity
breaks between separately generated clips are large, and motion is what stops
the eye auditing them. **Mark the cut point in the shot list** — that is what
the CUT ON field is for.

Artefacts read at rest and vanish in motion. A cut placed at a rest beat is a
cut placed where the joins are most visible.

---

## 8. Continuity rules

Restate at the top of the list, then enforce in every prompt:

- The season and light progression, and that it only moves one direction
- Each character's continuity mark
- Each hero prop's marking
- The landmark that anchors wide shots, and on which side
- The key-light direction per location and per act
- Anything that must never appear

---

## 9. Be honest about additions

If you invent a beat the source does not contain — a moment of proof, a
reaction shot, a visual gag — **say so explicitly** and explain what it buys
and what it costs in fidelity. Let the user decide whether to keep it.

---

## Output

Write `shots.md`, and publish it as an artifact if the session supports it.
Present it and get approval before rendering anything.

Note for each shot whether it is **speaking** or **silent** — they take
different generation paths, and the count of each determines the budget.

Write the prompts to `${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md`:
nine elements in order, 100–150 words of active payload, timed beats, one
camera move with a speed word, motion as consequence, 3–5 specific negatives.

---

## Consider a storyboard grid for dense action

For a montage, a fight, a chase or any passage where **tension comes from cut
density rather than from any single shot**, there is a second route worth
knowing.

Instead of planning sixteen shots as text and generating sixteen clips,
generate **one image**: a 4×4 grid of numbered panels, each labelled with its
shot size, its camera move and a one-word rhythm note. Then hand that grid to
the video model as the reference and ask it to follow the cells in order.

```
Compose a 4x4 storyboard grid (16 numbered cells) for this sequence: <action>

CHARACTER: use @Image1's identity throughout, asymmetric details preserved on
the correct side.
LOCATION: use @Image2's spatial layout.

Each cell labels: SHOT # (1-16) · SIZE (WIDE / MS / CU / ECU) · CAMERA-MOVE
arrow (push, pull, whip, dolly, crash-zoom, handheld) · one-word RHYTHM note
(BEAT / IMPACT / RECOVERY / RESET).

Vary shot size aggressively — never two WIDEs in a row. Land every IMPACT on
a CU or ECU. Numbered cells, clear gutters between panels.
```

The claim behind it is worth testing on your model before relying on it: a
video model anchors its motion plan to the visual reference, so a grid of
sixteen drawn cells gives it sixteen visual targets, whereas **text
descriptions of shots get averaged into mush.**

Three things make this worth the trouble even if you do not generate from it:

- **The grid is a far better approval artifact than a text shot list.** The
  user can see the cut density and the shot-size variation at a glance. Render
  it at 3840×2160 or the panels blur and neither the model nor the user can
  read them.
- **Repair is cheap and targeted.** If one panel reads badly, regenerate the
  grid with that cell's note emphasised — not the video.
- **It enforces the rule it states.** "Never two WIDEs in a row" and "land
  every IMPACT on a CU" are visible in a grid and invisible in a list.

For longer sequences, chain two grids and **put the last cell of grid A into
the first cell of grid B as a continuity anchor.**

Do not use this for dialogue, for anything needing lip-sync, or for a beat
whose whole point is one sustained shot.

---

## Done criteria

The shot list is finished when:

1. Every shot has a complete camera block with no blanks.
2. Every shot has a one-sentence JOB.
3. Every beat has a named value shift, and no two consecutive beats flip the
   same value in the same direction.
4. Shot count matches the runtime target and the average shot length is 4.0–4.5s.
5. No shot carrying a face exceeds six seconds, except at most one at the end.
6. No shot exceeds `floor(duration / 4)` beats, capped at 4.
7. No two-shot has two speakers in it.
8. Every shot names the movement its outgoing cut lands on.
9. The coverage budget is met, including four or more pure reaction shots.
10. Every location has its axis of action and light direction declared.

If any is false, say which. A shot list that fails one of these produces a film
that fails in a way nobody can point at afterwards.
