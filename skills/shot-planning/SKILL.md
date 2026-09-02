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

If the plan comes out at seven shots for a minute, that is not a pacing
preference. It is a broken film. Re-plan it.

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
