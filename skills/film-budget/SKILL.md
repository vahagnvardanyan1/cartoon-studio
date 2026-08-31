---
name: film-budget
description: Check credit balance and estimate the cost of a cartoon production or a remaining stage. Use when the user says "/film-budget", "how much will this cost", "check credits", "what's this going to cost", or before committing to a large batch of generation.
---

# Estimate cost

Give the user a real number before spending, not a guess.

## Check the balance

Call `picsart_credits` and report what is actually available, including when it
resets.

## Price the work

Use `picsart_preflight` on a representative call for each job type — one
reference image, one draft clip, one full-resolution clip, one voice line, one
music cue. Preflight validates the parameters and quotes the cost without
spending anything. Never quote from memory; prices and models change.

## Build the estimate

Count the actual work from `assets.md` and `shots.md`:

- Reference images still to generate, plus a realistic allowance for revisions
  (assume roughly one retry in three)
- Keyframes: one per shot, two for silent shots that need an end frame
- Draft clips, plus retakes
- Full-resolution renders of approved shots
- Voice lines, music cues, sound effects
- Final assembly renders, plus the inspection frames you will sample

Present it as a short table by category with a total, then state the balance
and whether it covers the work.

## Be honest about the shape of the spend

Say which parts are cheap and which are expensive, so the user can make real
choices — drafting at low resolution costs roughly a quarter of a full render,
and generating two variants of a shot to choose between costs less than
discovering a problem after twenty shots are finished.

If the balance will not cover the plan, say so before starting and propose what
to cut: fewer variants, shorter runtime, or fewer shots.
