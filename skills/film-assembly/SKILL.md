---
name: film-assembly
description: Assemble approved clips into a finished film with narration, dialogue, music, sound effects, titles and credits. Use when all clips are approved, or when the user says "/film-assembly", "assemble the film", "put it together", "make the final video".
---

# Assemble the film

Combine the approved clips into one film with a full soundtrack.

Read `${CLAUDE_PLUGIN_ROOT}/references/model-notes.md` for the compositor's
scene format — particularly the audio-track structure, which is not where you
would expect — and `${CLAUDE_PLUGIN_ROOT}/references/voice-and-audio.md` for
music, effects and the mix.

By this point the reel already contains every approved clip in place of its
still, so assembly is finishing, not construction.

## Build the picture first

Probe one clip for exact dimensions and frame rate, then concatenate all clips
in order using the compositor's montage recipe. Hard cuts by default; add
dissolves only where the shot list calls for them.

Render this picture-only cut and **inspect it** — sample frames across the
whole timeline and check that the shots are in order, that continuity holds
across the joins, and that nothing has been dropped.

## Then finish the audio

**Voice** is already recorded and approved from the voice stage. Only regenerate
a line if picture changed — and then match it using the seed and exact tag
string logged in `audio.md`.

**Music. Lock picture first.** No AI music tool scores to picture: none take a
video, hit a cue point or conform to timecode. Regenerating against a moving
cut wastes quota. Then:

- Generate **instrumental** cues deliberately longer than needed, for handles
- **Export WAV, not MP3** — MP3 artifacts survive into the mix
- **Export stems if the platform offers them.** This is the most consequential
  choice in the whole audio stage. With stems you can duck strings under
  dialogue and pull drums for a tension beat; without them you have a stereo
  bounce you can only fade
- Check the model's **maximum duration** before planning. If the film is
  longer, write cues that change with the story rather than looping one — the
  point where the music turns should be the point where the story does
- Use whatever mechanism the platform offers for **reusing a track's character**
  across cues, so the score sounds like one film rather than a playlist

**Sound design.** Effects for the specific actions in each shot, plus
atmosphere beds per location; use a looping mode for ambience where available.

**Set the project rate on day one — 48 kHz, 24-bit — and reject any asset that
does not meet it.** Upsampling does not restore a missing top octave; it will
sound dull beside library effects.

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

## Finish the picture

Raw generation is never the final picture. Treat these as pipeline stages, not
cleanup:

- **Colour grade** the whole film to one look. Along with sound and pacing,
  this is most of what separates a finished film from generated clips.
- **Upscale, if delivering above draft resolution.** Architecture matters more
  than brand: upscalers trained on real degraded footage sharpen what is there
  and so *amplify* the temporal flicker inherent in generated video. Diffusion-
  based upscalers invent plausible texture matching generated footage and are
  the right family here — run them at low restoration strength or they
  over-sharpen. Some are purpose-built for animation and process frames
  independently to avoid smearing.
- **Order matters: upscale first, then interpolate frame rate.** Interpolation
  smooths motion; it does not sharpen pixels.
- **Expect to composite.** A large share of finished shots on real productions
  are stitched from several generations. Assume it is normal, not a failure.

## Deliver

Render the final film, probe it to confirm it carries an audio track, and give
the user the URL. Then tell them honestly what is still imperfect — lip sync,
any remaining continuity drift, anything you would fix with more time. A film
delivered with a known-issues list is more useful than one delivered with a
flourish.

---

## By the time you get here, the film is already cut

If `shot-loop` ran properly, every shot has already been trimmed, mixed with
its own voice and score, approved, and appended to a running cut. This stage is
**not** where the film is first assembled — it is the finishing pass over
something the user has already watched grow.

What is actually left:

1. **One colour grade across every shot.** This is what makes separately
   generated clips read as one film, and it cannot be done per-shot inside the
   loop because it is a relative judgement across the whole thing.
2. **Film grain**, 10–15%.
3. **A global speed pass**, 10–15% faster if the cut drags — AI motion carries
   a built-in slow-motion bias.
4. **Music continuity.** Per-shot score levels set in the loop will not join up.
   Lay one continuous score across the finished cut and re-balance the ducking.
5. **Room tone across the seams**, so the ambience does not restart at each cut.
6. **Any typeset text** — titles, credits, and any words that must be correct.
   Never generated, always composited.
7. **Final watch, start to finish**, against the pace targets and the slop
   checklist in `editing-and-pace.md`.

If the film has *not* been built through the loop and you are assembling raw
clips here for the first time, say so plainly to the user: they are about to
see problems that should have been caught twenty shots ago, and the honest
options are to fix the worst of them or to re-run the loop.
