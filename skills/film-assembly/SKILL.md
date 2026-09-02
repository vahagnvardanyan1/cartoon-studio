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

Levels, from `finishing.md` §6:

| Element | Peak dB |
|---|---|
| Dialogue / narration | **−18 to −9**, target **−12** |
| Sound effects | −10 to −20 |
| Foley and ambience under dialogue | −15 to −25 |
| Music as primary element | −18 to −22 |
| Music under dialogue | −30 to −35 |

**Music sits 12–20 dB below dialogue, ambience 10–15 dB below dialogue, and
the dialogue never moves.** Delivery loudness for dialogue is −20 to −26 LUFS.

- Fade music around dialogue with volume keyframes
- Give each line a little air; do not butt lines against cuts
- **One shared light reverb across every line of dialogue.** The absence of a
  room is a major tell, and a shared reverb also glues together lines that were
  generated separately
- **EQ the synthetic voice**: high-pass at 80 Hz, boost 150–300 Hz for warmth,
  boost 1–2 kHz for clarity, cut 6–10 kHz for harshness, compress 3:1 to 4:1
- **One continuous room tone under the seams**, so the ambience does not
  restart at every cut

If a voice file reports no duration, derive it from file size and bitrate, or
declare it generously — over-declaring adds silence, under-declaring truncates
the line.

## Titles and credits

Typeset these in the edit, never in a generated frame — models mangle
lettering, especially non-Latin scripts. An opening title in the story's own
language and a closing credit crediting the original author.

## Finish the picture — the pass that decides whether it reads as a film

Follow `${CLAUDE_PLUGIN_ROOT}/references/finishing.md`. This is the cheapest
and most reliable quality gain available and almost nobody does it. When the
Runway festival jury explained what separated its finalists from ordinary AI
video, the answer was not the model — it was editing, colour grading and sound
design.

**Order matters and getting it wrong wastes the work:**

1. **Upscale first**, before grading — so you restore detail you can then
   *intentionally* soften, and so you clean compression artefacts before
   pushing contrast into them. Use a diffusion-family upscaler at low
   restoration strength; upscalers trained on real degraded footage amplify the
   temporal flicker inherent in generated video. Upscale before frame-rate
   interpolation, never after.
2. **Normalise per clip.** Waveform and vectorscope; neutralise white balance,
   set black and white points, tame oversaturation. This is where the
   deep-fried look dies, and it must be per clip because
   generation-to-generation variance is the enemy.
3. **Film emulation LUT** on its own node at **60–80% opacity**. Do not bake
   it.
4. **Blur, then grain, in that order.** Light Gaussian **0.3–0.6px first**,
   then 35mm or 16mm grain at **8–15%**. The blur kills the plastic
   over-sharpness; the grain replaces the destroyed high-frequency detail with
   organic high-frequency detail. Reversing the order gives you mush.
5. **Match every shot to a hero still** — shadow tint, highlight warmth,
   saturation, contrast. **This is what makes separately generated clips read
   as one film**, and it is the pass most often skipped. The colour script says
   which still, and where the film is *supposed* to change temperature rather
   than being corrected flat.
6. **Add motion imperfection.** Generated camera motion is too stable and too
   linear. Add the tremor in post: shoulder-mounted, a real operator's breath,
   a constant fine 1–2cm wobble. Add motion blur where movement is
   unnaturally sharp.
7. **The speed pass.** AI motion carries a built-in slow-motion bias. If the
   cut drags, run the whole film **10–15% faster** and watch it again. This is
   usually a bigger improvement than any individual reshoot.

**The hard limit, so nobody wastes an afternoon: grain and blur fix texture.
They cannot fix motion artefacts or anatomical errors.** A morphing hand is a
regeneration, not a grade note.

**Expect to composite.** Over 40% of finished shots on documented productions
are stitched from several generations. Assume it is normal.

## Run the finishing checklist

Watch the whole film once, start to finish, against the checklist at the end of
`finishing.md` — texture, face, motion, light and grade, cut, sound. Every item
on it is a named tell. Report what you find honestly rather than delivering and
hoping.

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
