---
name: shot-planning
description: Break a story into a full shot list for animation, with camera, action, dialogue, sound, duration and generation prompts for every shot. Use when reference art is approved, or when the user says "/shot-planning", "plan the shots", "make the shot list", "break this into scenes".
---

# Plan the shots

Turn the story beats into a complete shot list. This document is what the whole
generation stage executes, so it needs to be right before a single clip is
rendered.

Read `canon.md` and `assets.md` first.

## Structure the film

Group shots into acts that follow the story's own shape. Give the turn and the
ending room; compress the setup. A three-minute film is roughly 20–24 shots at
6–12 seconds each.

Use repetition deliberately where the story repeats: an identical framing
returned to with only the weather and a character's posture changed is the
cheapest and strongest way to show time passing.

## Every shot needs

- **Number and title** — number in tens (`SQ0010_SH0020`) so shots can be
  inserted later without renumbering the reel
- **Plot** — what happens, one or two sentences
- **Cast** — who appears
- **Location and time of day** — naming the approved environment plate
- **Action and emotion** — as observable movement, not adjectives
- **Camera** — angle and one movement, with an explicit end framing
- **Dialogue or narration** — in the film's language, with a translation
- **Sound** — effects and atmosphere, and what the score is doing
- **Duration** — provisional for speaking shots; the recorded line will set the
  real length in the voice stage
- **Reference assets** — which approved images this shot is built from
- **Generation prompt** — written to the template, with timed beats

## Write the prompts properly

Follow `${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md`. Every shot
prompt carries timed beats, one camera move, the size lock, the hands
reminder, the film-look block and an AVOID list.

Note for each shot whether it is **speaking** or **silent** — they take
different generation paths, and the count of each determines the budget.

## Staging and screen grammar

Decide these in planning, not while generating — they are camera problems, not
performance problems, and they matter more in animation than live action
because there is no incidental real geography to orient the viewer.

- **The line.** Keep the camera on one side of the axis between two characters
  for the length of a scene, so one stays screen-left and the other screen-
  right. Crossing it makes the audience feel the characters have swapped.
- **Screen direction.** A character travelling left-to-right keeps travelling
  left-to-right across cuts, or the audience reads it as turning back.
- **Eyelines.** Where a character looks must agree with where the other one is
  in the geography you established.
- **Silhouette.** Each key pose should read as a black shape. If it doesn't,
  restage it.

## Continuity rules

Restate at the top of the list, and then enforce in every prompt:

- The season and light progression, and that it only moves one direction
- Each character's continuity mark
- Each hero prop's marking
- The landmark that anchors wide shots, and on which side
- Anything that must never appear (a hat on a bare-headed character, snow in
  autumn)

## Be honest about additions

If you invent a beat the source does not contain — a moment of proof, a
reaction shot, a visual gag — **say so explicitly** and explain what it buys
and what it costs in fidelity. Let the user decide whether to keep it.

## Output

Write `shots.md`, and publish it as an artifact if the session supports it —
it is a reference document the user will return to throughout generation.

Present it and get approval before rendering anything.

---

## Shot count comes first, and it is not negotiable

Before writing a single shot, compute the count from the runtime. **Average
shot length of 4.0–4.5 seconds** is the target — see `editing-and-pace.md`
for why, and for the evidence.

| Runtime | Shots |
|---|---|
| 45s | 12–14 |
| 90s | 20–24 |
| 3 min | 40–45 |

**No shot containing a face or continuous character motion may exceed six
seconds.** AI motion loses the viewer at 6–8 seconds — past that they stop
watching the story and start noticing the machine. Allow yourself exactly one
exception, at the very end, where the length reads as deliberate.

If the plan comes out at 7 shots for a minute, it is not a pacing preference,
it is a broken film. Re-plan it.

## Build a descending ladder

Shot length shortens beat by beat through an escalation — roughly 5.5s in the
setup, 4.5 in the first turn, 3 in the middle, 2.5 at the peak — then breaks
the pattern once for the ending. Vary lengths **within** each beat too;
uniform shot length at any tempo is itself an AI-slop tell.

Put one deliberate slow passage inside the fastest beat. It is worth more than
another round of quick cuts.

## Coverage budget

Per 22 shots: 1 establishing, 5–6 mediums, 6–7 close-ups, 2–3 extreme
close-ups, 3–4 inserts, and **4–5 dedicated reaction shots**. If fewer than
four are pure reactions, comedy will underperform — and a reaction close-up is
also the cheapest and most reliable shot an AI model can produce.

Coverage tightens as stakes rise. Each rung of an escalation is framed closer
than the one below it.

## Put the cut on a movement

Every swing, throw, fall, door-slam and hand-off should land on a cut. The
continuity breaks between separately generated clips are large; motion is what
stops the eye auditing them. Mark the cut point in the shot list.

## Write screen direction into every shot

The model has no memory of your geometry. "Shop on the RIGHT of frame, lane
running off to the LEFT, he enters from the LEFT" goes in the text of every
prompt in that location — not just the first.

## Never plan a two-shot in which two characters speak

Lip-sync needs one portrait per pass, so a two-hander with two speakers cannot
be lip-synced and the video model will not move the mouths on its own — it
ignores the instruction outright and returns closed faces.

Every exchange gets covered in **singles**: a wide for the situation, a single
on each speaker, and a two-shot only for the silent physical beat between them.
That is normal shot/reverse-shot coverage, it doubles the shot count in the
right direction, and it is the only structure that lets both voices be real.
