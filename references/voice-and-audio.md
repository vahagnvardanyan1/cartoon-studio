# Voice, dialogue and audio

Researched August 2026. Model specifics change; the structural findings don't.

---

## 1. The order of operations

**Record the voice before generating the picture.** This is not borrowed
tradition — the tools demand it. Lip-sync models take an audio file as their
driving input; the audio determines the shot's length. Generating picture first
and fitting voice afterwards means fighting the tool.

Consequence: **the recorded line sets the shot duration**, not your shot list.
Plan durations after the voice exists.

---

## 2. Choosing a voice model

Do not cast from a benchmark leaderboard. Those boards measure short, neutral,
agent-style speech — naturalness and intelligibility. They do not measure
sustained character acting, shouting, crying, or a ninety-second monologue. A
model can top the arena and be useless for a villain's soliloquy.

**Audition on your own lines, in your own language, and let a native speaker
choose blind.**

Broad shape of the field: one family leads on expressive character work and
performance direction; another leads on raw naturalness and low latency; several
open models are competitive but carry licence traps (research-only licences,
watermarked output). Verify the licence before shipping a festival film.

---

## 3. Non-English and low-resource languages

This is where most productions come unstuck.

**Language support ≠ accent support.** Vendors publish the first and not the
second. A model can produce every phoneme correctly and still sound
unmistakably foreign, because multilingual models carry a strong English
phonetic bias that leaks through as:

- **Prosody carry-over** — English stress and intonation persist across the
  language boundary. For a language with predominantly word-final stress, an
  English-biased model will front-stress and a native ear hears it instantly.
- **Phonetic substitution** — contrasts that don't exist in English get
  collapsed (aspirated versus unaspirated stops, for example).
- **Numbers, dates, acronyms and loanwords** — the documented worst category.

**Check support per model version, not per vendor.** Language rosters differ
enormously between versions of the same family, and the flagship expressive
model often supports far more languages than the stable long-form one. That
matters: it can force you onto a model with a shorter character limit and a
greater tendency to hallucinate, purely because it is the only one that speaks
your language.

**Also check the documented language list for *cloning*, separately.** Cloning
support often follows a different model's roster than synthesis does. If your
language is outside it, cloning is unvalidated territory.

### An evaluation protocol you can hand a native speaker

Build an adversarial test set **before** casting. Not nice sentences:

- Proper nouns — character names, place names, invented words
- Numbers, dates, currency, times
- Code-switching — loanwords and brand names embedded in the dialogue
- Long sentences with subordinate clauses, where prosody collapses first
- Emotional extremes — shouting, whispering, crying
- Text at several lengths, to find where quality degrades

Then run a **blind A/B with vendor names hidden**, scoring separately for:
segmental accuracy, lexical stress, sentence prosody, foreign-accent rating,
and naturalness. The accent rating is the one that decides the project.

A cheap automated screen: synthesise, transcribe with a strong ASR in that
language, compare against the source text. This catches gross mispronunciation
and dropped words at scale, so the native speaker's time goes to prosody. It
does not catch accent.

**Lock a pronunciation dictionary early** if the platform supports one. For a
film full of invented names this is not optional. Where it isn't supported,
budget time for per-line phonetic respelling.

---

## 4. Voice cloning — and the constraint people miss

**A clone carries timbre, not accent.** Clone a speaker of one language and ask
for another, and you get the target language spoken with the source speaker's
accent. If you want native-sounding speech, **your reference speaker must be a
native speaker of that language.** This is a casting decision made in
pre-production, not a problem solved in post by trying another model.

Instant cloning wants one to two minutes of audio; professional cloning wants
thirty minutes to three hours and trains a dedicated model. Fidelity differs
accordingly — but check which cloning tier is actually compatible with the
expressive model you need, because the highest-fidelity clone is sometimes not
optimised for the most directable model.

**Recording spec for a usable clone:** proper microphone into an interface, pop
filter, treated room with no reverb (baked-in room cannot be removed),
consistent level, single speaker, no background noise, uncompressed if
possible. Consistency in equals consistency out.

**Under-appreciated:** clones learn cadence, pauses and breathing. Hand a model
two minutes of calm narration and it will resist shouting. **Record reference
material in the emotional register the film needs**, and record range if the
character has range.

**Consent and rights.** Get written, signed releases covering: creation of a
model from the performer's voice; the specific project and any sequels or
marketing; territory and duration; whether the model is deleted at wrap; and —
the one people forget — **whether the voice may be used in languages the
performer does not speak.** Keep the source recordings with the releases.

**Never let a vendor hold your only master.** Platforms shut down, sometimes
with days of notice and no export tooling. Archive the raw WAVs and, where you
have them, the source recordings.

---

## 5. Directing a performance

Modern expressive TTS is directed through the text, not through sliders.

**Inline performance tags** in square brackets — laughs, whispers, sighs,
sarcastic, excited, crying — and they stack. Some platforms also offer
*wrapping* tags that scope an effect to an exact span rather than hoping its
influence decays correctly; prefer those where available.

**Punctuation is a control surface.** Ellipses give pauses, capitalisation
gives emphasis.

**Stability settings involve a real tradeoff.** The most expressive setting is
also the one that hallucinates content; the most stable one ignores your
direction. Work in the middle by default, and reserve the expressive end for
short high-emotion lines you will listen to individually. Never use it for
unattended long-form.

**Very short inputs produce inconsistent results.** Expressive models want a
few hundred characters of context. Generating one short line at a time is
exactly the wrong shape. **Generate a scene chunk with surrounding dialogue,
then cut out the line you need** — the surrounding text conditions the prosody,
which is why the line then sounds like it belongs in the scene rather than read
cold.

**Use a dialogue endpoint for two-handers where one exists.** Generating each
character's lines separately and cutting them together produces the classic
"two people reading in different rooms" flatness. A model that sees the whole
exchange produces genuinely reactive performances.

### Takes, and logging them

- **The seed is your take number.** Fix it for reproducibility; vary it with
  identical text and direction to get different takes of the same intent. That
  separates "the model rolled badly" from "my direction is wrong."
- **Generate five to ten takes on any hero line.** It costs cents. Editorial
  attention is the expensive resource.
- **Vary one axis at a time** when a line is not working: seed, then stability,
  then tags, then punctuation, then rewrite. Changing several teaches nothing.
- **Log model ID, voice ID, seed, stability, and the exact text with its tags.**
  You will need to regenerate a line weeks later after a picture change, and
  without that record you cannot match it. A CSV per scene is enough.
- **Pin the model version explicitly.** Vendors update models silently.

---

## 6. Lip sync

### Two architectures, and conflating them causes most bad results

**Mouth-region replacement** takes existing video and replaces only the mouth.
Your footage, performance, lighting and camera move survive.

**Audio-driven generation** takes a still image plus audio and generates the
whole performance — head, body, sometimes gesture and environment. Your
original framing does not survive.

**In both families the audio you supply passes through unaltered.** These are
video models; they do not re-synthesise speech. Feed them an approved WAV.

Note the contrast with **general video-generation models**, which treat a
supplied audio file as a *style reference* and will invent convincing-sounding
nonsense in its place. Never hand dialogue to a general video model expecting
playback.

### The trap for animated films

**Many lip-sync tools explicitly do not support animals or non-humanoid
characters.** The reason is architectural, not tuning: mouth-replacement tools
depend on a human face detector and landmark model. A stylised animal, a robot,
a character with non-human eye spacing simply does not register, and you get a
silent no-op or garbage. No amount of prompting fixes it.

**Check for documented non-human support before choosing.** At least one
audio-driven model advertises animals, illustration, claymation and 3D
characters explicitly, offers much longer durations, and costs less per second
than the general-purpose alternatives. Performance-transfer tools that take a
driving video also tend to claim non-human support.

### Artifacts to inspect for

Teeth are the most common tell — flicker, wrong count, morphing. Then: identity
drift over long shots; mouth-region blur where the face crop resolution is
lower than the frame; visible seams at the inpaint boundary, worst on moving
cameras; occlusion failures where a hand or prop crosses the mouth; stiff or
over-dramatic gesture; and sharp degradation at profile and extreme angles.

**Some tools also burn caption overlays into the output.** Inspect a frame
before accepting any clip.

---

## 7. Music

**No AI music tool scores to picture.** None take a video, hit a cue point, or
conform to timecode. So the workflow is DAW-centric:

1. **Lock picture first.** Regenerating against a moving cut burns your quota.
2. Generate **instrumental** cues deliberately longer than needed — you want
   handles.
3. **Export WAV, not MP3.** MP3 artifacts survive into the final mix.
4. **Export stems if the platform offers them.** This is the single most
   important choice. With stems you can duck strings under dialogue and pull
   drums for a tension beat. Without them you have a stereo bounce you can only
   fade.
5. Conform in the DAW — time-stretch to hit points, use section editing to
   reach length.
6. For **thematic consistency**, use whatever mechanism the platform offers for
   reusing a track's character across cues. A score needs recurring motifs; a
   fixed, carefully written style prompt plus that mechanism is how you get
   cues that belong to the same film rather than a playlist.

**Check the maximum duration before planning cues.** If the film is longer than
the model's ceiling, write cues that *change with the story* rather than looping
one — the point where the music turns should be the point where the story does.

**Licensing is the highest-risk area in the whole audio pipeline.** A festival
or distributor will ask for a cue sheet and chain of title; "I generated it" is
not chain of title. Prefer platforms whose training data is licensed and whose
terms name film and television explicitly. Note that some platforms watermark
all output, and that per-user commercial rights can remain ambiguous even after
a vendor settles with rights holders. **Get the terms in writing, dated,
archived, for the exact plan tier you generated on.**

---

## 8. Sound effects

Generate effects for the specific actions in each shot, plus atmosphere beds
per location. Where a platform offers a looping mode, use it for ambience.

**Sample rate is the recurring trap.** Film delivery is 48 kHz, 24-bit. Some
generators output well below that, and upsampling does not restore the missing
top octave — it will sound dull next to library effects. **Decide the project
rate on day one and reject any asset that does not meet it**, rather than
resampling at the mix.

Where a platform exposes a prompt-adherence control, generate variants at both
ends: literal for specific events, loose for texture.

**Emerging and worth prototyping:** video-to-audio models that generate
temporally aligned foley from picture. Mostly research code today and generally
below finishing spec, but even a rough pass gives you a **sync map** showing
where events land, which you then replace with proper effects.

---

## 9. Mix

- Dialogue at full level; music well under it, roughly a quarter to a third.
- Fade music around dialogue rather than riding it flat.
- Give each line air; do not butt lines against cuts.
- Keep every raw generation. Never let the only copy be post-processed.
- Deliver at the project's sample rate and check loudness against the target
  standard for the platform.
