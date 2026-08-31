---
name: voice-production
description: Script, cast, direct and record the narration and dialogue for an animated production — before any clips are generated. Use after the shot list is approved, or when the user says "/voice-production", "record the voices", "do the narration", "cast the voices", "generate the dialogue".
---

# Produce the voice

Record the voice **before** generating picture. This is not borrowed tradition
— lip-sync tools take audio as their driving input and the recorded line sets
the shot's length. Generating picture first means fighting the tool, and it is
what makes lip sync unfixable later.

Read `${CLAUDE_PLUGIN_ROOT}/references/voice-and-audio.md` first.

## 1. Write the lines

Extract every narration and dialogue line from the shot list. Write them in the
film's language with a translation. Keep them short and speakable — a line that
reads well and says badly is a common failure.

Mark each line with its speaker and its shot.

## 2. Confirm the language is genuinely supported

Check support **per model version**, not per vendor. Rosters differ enormously
between versions of the same family, and the flagship expressive model often
supports many more languages than the stable long-form one — which can force
you onto a model with a tighter character limit and more hallucination.

Check the **cloning** language list separately; it often follows a different
model's roster than synthesis does.

## 3. Audition, and let a native speaker choose

Never cast from a benchmark leaderboard — those measure short neutral
agent-style speech, not character acting.

Generate **the same real line from the film** on every candidate model.
Present them unlabelled and ask the user to pick by ear. For a
non-English film, insist on a native speaker's judgement and ask them to listen
for **lexical stress** and **accent**, not just intelligibility — an
English-biased model gets every phoneme right and still sounds foreign.

If nothing is good enough, say so and propose a human recording. For a
culturally significant text this is often the right answer, and twenty short
lines take twenty minutes.

## 4. If the user records their own voice

Use the recording **directly**. Do not clone it into the target language unless
the reference speaker is already a native speaker of that language — a clone
carries timbre, not accent.

Recording spec: proper microphone, pop filter, quiet untreated-sounding room
avoided (baked-in reverb cannot be removed), consistent level, one speaker,
uncompressed.

## 5. Generate properly

- **Give the model context.** Expressive models produce inconsistent results
  from very short inputs. Generate a **scene chunk with surrounding dialogue**,
  then cut out the line you need. The surrounding text conditions the prosody.
- **Set stability deliberately.** The most expressive setting hallucinates; the
  most stable ignores direction. Work in the middle; reserve the expressive end
  for short high-emotion lines you will listen to individually.
- **Direct with inline performance tags** and punctuation — ellipses for
  pauses, capitalisation for emphasis.
- **Use a dialogue endpoint for two-handers** where the platform has one, so
  the model sees the whole exchange and produces reactive performances.
- **Take five to ten takes on every hero line.** Vary the seed with identical
  text to get different readings of the same direction. It costs cents;
  attention is the expensive part.
- **Vary one axis at a time** when a line is not working: seed, then stability,
  then tags, then punctuation, then rewrite.

## 6. Log every take

Write `audio.md` with, for each line: shot, speaker, exact text including tags,
model ID, voice ID, seed, stability, and the output URL.

You will need to regenerate a line after a picture change, and without the seed
and the exact tag string you cannot match it.

## 7. Then set the shot durations

Measure each line and **update the shot list so each speaking shot is as long
as its line**, plus handles. The dialogue dictates the cut, not the plan.

## Gate

Present the full voice track for approval before any clip is generated. Play
the lines in story order so the user hears the performance as a whole.
