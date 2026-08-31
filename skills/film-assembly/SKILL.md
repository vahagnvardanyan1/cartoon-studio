---
name: film-assembly
description: Assemble approved clips into a finished film with narration, dialogue, music, sound effects, titles and credits. Use when all clips are approved, or when the user says "/film-assembly", "assemble the film", "put it together", "make the final video".
---

# Assemble the film

Combine the approved clips into one film with a full soundtrack.

Read `${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` for the compositor's
scene format — particularly the audio-track structure, which is not where you
would expect.

## Build the picture first

Probe one clip for exact dimensions and frame rate, then concatenate all clips
in order using the compositor's montage recipe. Hard cuts by default; add
dissolves only where the shot list calls for them.

Render this picture-only cut and **inspect it** — sample frames across the
whole timeline and check that the shots are in order, that continuity holds
across the joins, and that nothing has been dropped.

## Then build the audio

**Voice.** Generate every narration and dialogue line with the approved voice
model. Verify the language is genuinely supported and audition voices on one
identical sentence before committing — let a native speaker choose. Use
distinct voices for narrator and characters.

**Music.** Check the music model's maximum duration before planning cues. If
the film is longer, write two or more cues that change with the story rather
than looping one — the point where the music turns should be the point where
the story does.

**Sound design.** Effects for the specific actions in each shot, plus
atmosphere beds per location.

## Mix it

Place each audio track at its timecode in the compositor's top-level `audio`
array — **not** as layers. The validator accepts audio layers and the renderer
then refuses them.

- Voice sits at full level
- Music sits well under it, around 25–30 percent
- Fade music in and out around dialogue with volume keyframes
- Give each line a little air; do not butt lines against cuts

If a voice file reports no duration, derive it from file size and bitrate, or
declare it generously — over-declaring adds silence, under-declaring truncates
the line.

## Titles and credits

Typeset these in the edit, never in a generated frame — models mangle
lettering, especially non-Latin scripts. An opening title in the story's own
language and a closing credit crediting the original author.

## Deliver

Render the final film, probe it to confirm it carries an audio track, and give
the user the URL. Then tell them honestly what is still imperfect — lip sync,
any remaining continuity drift, anything you would fix with more time. A film
delivered with a known-issues list is more useful than one delivered with a
flourish.
