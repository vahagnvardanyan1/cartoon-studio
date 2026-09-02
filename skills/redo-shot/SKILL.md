---
name: redo-shot
description: Regenerate a specific shot or reference asset that has a problem, diagnosing the cause before re-rendering. Use when the user says "/redo-shot", "fix shot 5", "regenerate that", "this one is bad", "redo the cat sheet", or reports a defect in a specific clip or image.
---

# Redo a shot or asset

Fix one item properly. A reroll without a diagnosis usually reproduces the same
fault.

## Diagnose before regenerating

**Look at it first.** Sample frames from the clip through the media tooling and
inspect them. Identify the actual defect rather than accepting a general "it's
bad" — the user often names a symptom whose cause is elsewhere.

Ask the user what specifically is wrong if it is not visible to you.

## Find the real cause

Check `${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` — most defects
are a known failure with a known fix. In particular:

| Symptom | Actual cause |
|---|---|
| Nothing happens; it feels static | No timed beats; camera told to hold still |
| Prop floats free of the hand | Start keyframe showed the wrong state |
| Hands are stumps | The **character sheet** is wrong, not the shot |
| A character is the wrong size | No scale sheet, or no size lock in the prompt |
| Shot ends in a cropped close-up | No end keyframe |
| Speech is gibberish | Audio was fed to a general video model |
| Wrong season or weather | Canon not restated, and no negative in the AVOID list |
| Character looks like someone else, but prettier and more generic | The prompt **re-described the face** while a reference was attached. Under i2i a written description competes with the reference and pulls toward an averaged face. Describe pose and light only; add the identity lock list |
| Character looks like someone else, no reference attached | Shot generated from text — or the identity string was **paraphrased** instead of pasted byte-identical |
| The continuity mark is on the wrong side | The model mirrored the frame. Check whether the screen direction flipped with it — it usually has |
| A thing you forbade appears anyway | Bare keyword AVOID list on a model with **no dedicated negative field** — it can render the list as subject matter. Convert to positive description |
| Only some of your directions happened | Too many active instructions; adherence decays by position. Cut to the two or three that matter |
| Reference bled unwanted lighting or pacing | Reference given no explicit job |
| Character stiff, cannot adapt to the light | Reference strength at maximum |
| Drift appears mid-clip | Clip too long; cut before the drift rather than fixing it |

**If the cause is upstream, fix it upstream.** A wrong hand means the character
sheet is wrong for every shot. Say so, fix the sheet, and list which already
approved shots are now stale rather than quietly leaving them inconsistent.

## Repair from the cheapest end first

Once you know the layer, fix at that layer — but when two fixes would both
work, **do the cheap one first and re-check.**

| Cost | Artifact | When |
|---|---|---|
| lowest | the clip prompt | motion wrong, frames fine |
| low | the keyframe | pose, framing, contact, staging wrong |
| medium | the clip, re-run at a different seed | intermittent artefacts |
| high | the plate | geometry, season, light direction wrong |
| highest | the character sheet | face, build, costume, proportion wrong — **and every shot that used it is now stale** |

Say the cost ordering out loud when you propose a fix. "I can re-run the clip
prompt for one generation, or rebuild the sheet, which fixes it properly but
invalidates the four shots already approved" is a decision the user should make
with the number in front of them.

## Regenerate

Change **exactly one variable** — not the whole prompt. Rewriting the prompt
wholesale throws away the information about what was already working, and is
why the second attempt is often worse than the first.

Change only what needs changing. Keep the same references, the same framing
intent, the same duration, so the fix does not introduce new discontinuity.

Add the specific failure to that shot's AVOID list.

If the same defect survives two attempts, stop rerolling: generate an options
sheet showing several treatments of the contested detail and let the user pick.

## Present

Say what was wrong, what you changed, and what to check. Then update
`shots.md` or `assets.md`, marking the old version superseded.
