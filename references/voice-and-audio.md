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

---

## Dialogue, not only narration

A verse tale is not automatically narration. the source text's one production has
the greeting written as a real exchange and both killings as shouted lines —
and the first plan flattened all of it into a narrator talking over pictures.
The user's note was blunt and correct: *"people should speak, not only
telling."*

**Read the source and pull out everything spoken in a character's voice.**
Give those lines to characters, keep the rest for the narrator. A folk tale
usually contains far more dialogue than it first appears to.

Cast a **distinct voice per speaker**, including crowds. On the one production
film that was five: a narrator, two principals, a crowd, and a cold official
reader for a pair of formal proclamations. That last one carried the satire —
the text switches from village dialect into chancery prose, and if both come
out of the same mouth the joke disappears.

---

## Let the voice change the shot COUNT, not the shot LENGTH

The most important scheduling rule in this plugin.

When a recorded line comes back longer than its planned shot, there are two
ways to absorb it:

- **Stretch the shot.** This is what the first film did — it slowed three
  clips down to fit the audio, making a slow film slower. Never do this.
- **Add shots.** Split the beat into more, shorter shots under the same
  narration.

On one production a rapid catalogue of objects came back at 13 seconds against
a 3-second shot. Beat 4 was re-planned from three shots into four sub-beats of
two or three shots each. The film grew from 22 shots to 26 and from 87 seconds
to 99 — **and the average shot length did not move.** That is the correct
outcome.

Re-record instead when the line is simply too slowly read: tighter direction
(`[rattling off a list at speed, barely pausing for breath]`) and fewer lines
cut a 13-second take to 6.

---

## Audio tags actually work — use them

Eleven v3 takes bracketed direction inline, in English, inside non-English
text. Three categories: emotions `[curious] [crying] [mischievously]`,
delivery `[whispers] [shouts]`, reactions `[laughs] [sighs] [clears throat]`.

```
[warmly, an old village storyteller beginning a tale] <first line…>
[rattling off a list at speed, barely pausing for breath] <catalogue line…>
[a cry of grief turning instantly into fury, shouting] <the cry…>
[cold, official, reading a proclamation aloud from a scroll] <the decree…>
```

Check every take for two failures: **the tag being spoken aloud** instead of
acted, and any word mispronounced. Less-trodden languages need all five runs
listened to, not the first.

---

## Where the sound actually comes from now

Three layers, in this order of preference:

1. **Native clip audio** — `generateAudio: true` on every non-dialogue shot,
   with the sound described in the prompt. Synced to the real motion.
2. **Real recorded dialogue** — driven through OmniHuman on close-ups so the
   mouth matches, laid in the edit on wider shots.
3. **A separately generated bed** — only for what the clips cannot carry:
   the score, and a continuous ambience if the native beds do not join up.

The old approach of building an effects library and syncing it by hand is now
the fallback, not the default.

**One structural trick worth stealing.** Generate the same sound twice, in two
different emotional contexts, and let the contrast do the work. In *Drop of
production a single insect buzzes on the same spot twice, seventy seconds
apart — the first time under a warm inhabited ambience, the second over nothing
but dead wind. The audience hears the difference before noticing
it.

---

## Normalise non-English text with a language model first

The Picsart catalogue carries text models under `mode: "text"` — `gpt-5.5`,
`claude-opus-4-8`, `gemini-3-pro` and the Gemini Flash tiers. Call them the
same way as any other model, with `picsart_generate`.

**Every non-English line goes through one before it is recorded**, and it is
mandatory when the source is old or dialectal.

### Why

A folk tale worth adapting is usually a century old, and its printed text is
full of things that belong to the page rather than the mouth: archaic
orthography, dialect forms, and metrical marks. One clear case: a 1909 verse
text wrote its reduced vowels out explicitly, purely to fill the syllable count
for the metre. Preserving that spelling is correct for a printed edition and
wrong for a soundtrack — the TTS fights it and a native speaker hears something
stilted.

**Fidelity to the source spelling is not a virtue in a recording.** Meaning and
register are.

### How to prompt it

```
Rewrite these lines from <source dialect/period> into clean, natural, modern
<language> that a native speaker finds correct and that TTS pronounces
properly. Keep meaning and imagery. It need NOT be verbatim. Keep the register:
<who is speaking, and how>.

Example of the exact standard wanted:
BEFORE: <one original line>
AFTER:  <the corrected version>

Return ONLY a numbered list of corrected <language>. No commentary, no English.
```

The **worked before/after pair carries almost all the weight.** If the user has
already corrected one line themselves, that correction is the example — paste
it in verbatim and the model matches the standard for the rest.

Keep the batch to eight or ten lines. A longer prompt timed out at 60 seconds
on the MCP call more than once.

### It finds real errors

This is not only a style pass. On one production it caught the wrong word for a common tool — an actual wrong word that had propagated into
the shot list, the narration and an image prompt without anyone noticing.

### The user is the authority, not the model

Print the before and after side by side, show it, and ask whether anything is
still wrong **before** recording. The language model is a first pass over text
in a language you may not read. It is not the final word, and presenting it as
one is how a confident error reaches the finished film.
