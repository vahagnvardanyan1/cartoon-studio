---
name: voice-production
description: Script, correct, cast, direct and record the narration and dialogue for an animated production — before any clips are generated. Use after the shot list is approved, or when the user says "/voice-production", "record the voices", "do the narration", "cast the voices", "generate the dialogue", "fix the script".
---

# Produce the voice

Record the voice **before** generating picture. This is not borrowed tradition
— lip-sync tools take audio as their driving input and the recorded line sets
the shot's length. Generating picture first means fighting the tool, and it is
what makes lip sync unfixable later.

Read `${CLAUDE_PLUGIN_ROOT}/references/text-and-language.md` and
`${CLAUDE_PLUGIN_ROOT}/references/voice-and-audio.md` first.
`${CLAUDE_PLUGIN_ROOT}/references/finishing.md` §6 has the mix numbers.

## 1. Write the lines

Extract every narration and dialogue line from the shot list. Keep them short
and speakable — a line that reads well and says badly is a common failure.
Mark each with its speaker and its shot.

## 2. THE TEXT GATE — run it, in every language, including English

**Nothing is recorded until every line has been through a language model and
the user has approved the result.** This is a gate. It has a whole reference
file: `${CLAUDE_PLUGIN_ROOT}/references/text-and-language.md`. Follow it.

The short version:

1. **Send every line** — narration, dialogue, the title, the credits, any
   on-screen text — to a text model via `picsart_generate` (`gpt-5.5`,
   `claude-opus-4-8` or `gemini-3-pro`, `mode: "text"`).
2. **Write the instruction in the film's own language** if the film is not in
   English. An English prompt asking a model to fix another language returns a
   timid pass; the same request written in that language returns real
   corrections. This one change is the difference between the gate working and
   not.
3. **Give it a worked before/after pair.** If the user has corrected a line
   themselves, quote that correction verbatim as the standard.
4. **Say the result need not be verbatim**, and name the register to keep.
5. **Name the specific defect classes** you expect — archaic spelling, metrical
   notation, wrong case endings, wrong words, digits, anything unspeakable in
   one breath.
6. **Ask for the corrected text only** — a labelled list, no commentary.
7. **Show the user the before and after side by side** and ask whether anything
   is still wrong. The user is the check on the model, not the reverse.
8. **Write the approved text to `script.md`.** Every later recording comes from
   that file and from nowhere else.

**English is not exempt.** Its failure mode is different — an unspeakable
clause, a repeated word, a stilted register, a number written as digits the
voice model will read wrong — but it is just as real. A narration cue is a
performance script, not prose.

**Re-run the gate whenever a line changes.** Re-recording a dozen cues because
the text was wrong is the most avoidable rework in this pipeline, and it
cascades into shot lengths and the cut.

## 3. Confirm the language is genuinely supported

Check support **per model version**, not per vendor. Rosters differ enormously
between versions of the same family, and the flagship expressive model often
supports many more languages than the stable long-form one — which can force
you onto a model with a tighter character limit and more hallucination.

Check the **cloning** language list separately; it often follows a different
model's roster than synthesis does.

## 4. Cast, and let a native speaker choose

Never cast from a benchmark leaderboard — those measure short neutral
agent-style speech, not character acting.

Generate **the same real line from the film** on every candidate. Present them
unlabelled and ask the user to pick by ear. For a non-English film, insist on a
native speaker's judgement, and ask them to listen for **lexical stress** and
**accent**, not just intelligibility — an English-biased model gets every
phoneme right and still sounds foreign.

**Write the casting into `script.md`** — role, voice name, voice ID, and which
cues it covers. A character whose voice changes halfway through the film is a
failure the user hears immediately, and the usual cause is a casting decision
that was never written down.

If nothing is good enough, say so and propose a human recording. For a
culturally significant text this is often the right answer, and twenty short
lines take twenty minutes.

## 5. If the user records their own voice

Use the recording **directly**. Do not clone it into the target language unless
the reference speaker is already a native speaker of that language — a clone
carries timbre, not accent.

Recording spec: proper microphone, pop filter, a room without baked-in reverb
(it cannot be removed), consistent level, one speaker, uncompressed.

## 6. Generate properly

- **Stability 35–45%.** The single most important control. Most amateur output
  is over-stabilised into flatness. Higher ignores direction; lower
  hallucinates. Similarity 70–85%, style exaggeration 0–10%, speaker boost on.
- **Give the model context.** Expressive models produce inconsistent results
  from very short inputs. Generate a scene chunk with surrounding dialogue,
  then cut out the line you need — the surrounding text conditions the prosody.
- **Break long passages into sections** and generate them separately. This is
  the direct fix for the flat metronomic cadence that marks synthetic
  narration: each chunk gets its own arc.
- **Punctuation is performance notation** — ellipses for hesitation, em-dashes
  for rhythm breaks, capitals for emphasis, full stops for hard landings.
  Inline performance tags on top of that.
- **Use a dialogue endpoint for two-handers** where the platform has one, so
  the model sees the whole exchange and produces reactive performances.
- **Five to ten takes on every hero line.** Vary the seed with identical text
  to get different readings of the same direction. It costs cents; attention is
  the expensive part.
- **Vary one axis at a time** when a line is not working: seed, then stability,
  then tags, then punctuation, then rewrite.

## 7. When a line is refused by a content filter

Speech models refuse text that reads as violent even when it is a century-old
folk tale. **Do not quietly drop the line and do not soften the story.**
Rephrase so it carries the same meaning through a different construction — an
image often passes where a plain verb is refused — then tell the user what you
changed and why.

## 8. Log every take

Write `audio.md` with, for each line: shot, speaker, exact text including tags,
model ID, voice ID, seed, stability, duration, and the output URL.

You will need to regenerate a line after a picture change, and without the seed
and the exact tag string you cannot match it.

## 9. Then set the shot durations

Measure each line and **update the shot list so each speaking shot is as long
as its line**, plus handles. The dialogue dictates the cut, not the plan.

## Gate

Present the full voice track for approval before any clip is generated. Play
the lines in story order so the user hears the performance as a whole.
