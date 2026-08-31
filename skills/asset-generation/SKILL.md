---
name: asset-generation
description: Generate approved reference art for an animated production — character sheets, scale sheets, environment plates and hero props — one asset at a time with an approval gate on each. Use when the style is locked, or when the user says "/asset-generation", "generate the references", "make the character sheets", "start the artwork".
---

# Generate reference art

Build the reference library that every shot will be generated against. One
asset at a time, each approved before the next begins.

Read `${CLAUDE_PLUGIN_ROOT}/references/production-lessons.md` and
`${CLAUDE_PLUGIN_ROOT}/references/prompt-templates.md` before starting.

## Order matters

Generate in this sequence. Each step depends on the one above it.

1. **Style keyframe** — already approved in the style stage. It is the parent
   of everything.
2. **Scale sheet** — all leads together, correct relative heights, **with
   articulated hands**. See below; this single sheet prevents two of the worst
   recurring failures.
3. **Character sheets** — one per character, generated against the scale sheet.
4. **Environment plates** — no characters in them, so they work as clean
   backgrounds and can be re-dressed for season.
5. **Hero props** — with their distinctive markings, in several states.

## The scale sheet is not optional

Generating each character separately, each scaled to fill its own frame,
records nothing about their relative size — and shots will then guess, often
making the wrong character bigger.

Generate **one sheet with all leads standing side by side** on the same ground
line with matching contact shadows, and state the height relationship as the
explicit point of the image. Make this the master character reference.

## Hands must be specified here

If a character sheet is generated with paws, mittens or featureless stumps,
every prop shot in the film will fail and no prompt will fix it downstream.

Specify on the sheet: *four separated fingers plus an opposable thumb, visible
knuckles and joints, short claws, pads, fur on the backs*. Pose the sheet with
hands raised and fingers spread so the construction is visible and inherited.

This applies to any character who will hold, carry, point, sew or grip.

## Generating each asset

- Feed the **approved parent references** as source images — that is what holds
  identity. Respect the payload cap; about two high-resolution references per
  call, and describe the rest.
- Use the templates in `prompt-templates.md`.
- End every prompt with an **AVOID** list covering that asset's likely failure
  modes, and always include `no text, no letters, no watermark`.
- **Inspect the result before presenting it.** Render it through the media
  tooling and actually look at it. Check the continuity mark, the hands, the
  proportions, the palette.

## Presenting for approval

Give the URL, then say **what to check** — the two or three things most likely
to be wrong on this specific asset. Not "what do you think?".

Then stop. Wait. Do not generate the next asset.

**If rejected:** revise the prompt and regenerate the *same* asset. If the same
flaw appears twice, stop guessing — generate an **options sheet** showing four
treatments of the contested detail in one image and let the user pick.

**If approved:** record it in `assets.md` with its URL and what it is the
authority for. If it supersedes an earlier asset, mark the old one superseded
so nothing downstream uses it.

## When an approved asset later turns out wrong

Fix it at the source and **regenerate everything derived from it**. A character
sheet corrected after ten shots means those ten shots are wrong. Say so plainly
rather than letting the inconsistency ship.

## Gate

Do not begin video generation until every essential asset is approved. Confirm
the complete list with the user before moving on.
