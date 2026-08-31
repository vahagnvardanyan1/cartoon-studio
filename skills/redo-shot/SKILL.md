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
| Character looks like someone else | Shot generated from text, not from a keyframe |

**If the cause is upstream, fix it upstream.** A wrong hand means the character
sheet is wrong for every shot. Say so, fix the sheet, and list which already
approved shots are now stale rather than quietly leaving them inconsistent.

## Regenerate

Change only what needs changing. Keep the same references, the same framing
intent, the same duration, so the fix does not introduce new discontinuity.

Add the specific failure to that shot's AVOID list.

If the same defect survives two attempts, stop rerolling: generate an options
sheet showing several treatments of the contested detail and let the user pick.

## Present

Say what was wrong, what you changed, and what to check. Then update
`shots.md` or `assets.md`, marking the old version superseded.
