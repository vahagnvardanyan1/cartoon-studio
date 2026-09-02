# Text and language

**Every word that will be heard or seen in the finished film passes through a
language model before it is recorded, generated or typeset. Every word. In
every language. Including English.**

This is a gate, not a suggestion. It is cheap — one text call — and skipping it
is the most expensive mistake in the pipeline, because text errors are
discovered *after* the voice is recorded, after the lip-sync is generated, and
after the shot is cut.

---

## 1. What goes through the gate

| What | Why |
|---|---|
| Every narration cue | it will be spoken aloud and cannot be un-spoken |
| Every line of dialogue | same, and it also drives the lip-sync |
| The opening title and closing credits | typeset, permanent, and read closely |
| Any on-screen text the story depends on | a sign, a letter, a decree |
| The film's own title and logline | they end up in the artifact and in the delivery |

**English is not exempt.** The failure mode in English is different from the
failure mode in a language with archaic orthography, but it is just as real:
an unspeakable clause, a repeated word two lines apart, a stilted register, a
sentence that scans on the page and collapses in the mouth, a number written as
digits that the voice model will read wrong. A narration line is a *performance
script*, not prose, and it needs an editor.

---

## 2. When to run it

**After the lines are written. Before a single take is generated.**

Re-recording fifteen cues because the text was wrong is the most avoidable
rework in this whole pipeline, and it cascades: a changed line changes the
duration, which changes the shot length, which changes the cut.

Run it again if the story text changes, if the user corrects a line, or if a
new line is added mid-production. Never record from an un-gated line "just to
hear it" — that take will end up in the film.

---

## 3. How to run it so it actually works

Send the lines to a text model through `picsart_generate` — `gpt-5.5`,
`claude-opus-4-8` and `gemini-3-pro` are all in the catalogue under
`mode: "text"`.

Five things separate a useful pass from a useless one.

### 3.1 Prompt in the target language

**This is the difference between a timid pass and a real one.** A correction
prompt written in English, asking a model to fix a line in another language,
comes back with a comma added. The same request written *in that language*
comes back with real corrections — case endings, verb forms, archaic vocabulary
replaced, metrical notation stripped.

The model matches the register and rigour of the language it is addressed in.
For a non-English film, write the instruction in the film's language. This was
observed directly: the same set of lines, sent twice to the same model, came
back cosmetically changed under an English prompt and substantively corrected
under a native-language one.

### 3.2 Give a worked before/after pair

One example teaches more than a paragraph of instruction. **If the user has
corrected a line themselves, that correction is the example** — quote it
verbatim in the prompt as the standard to match.

### 3.3 Say explicitly that it need not be verbatim

Fidelity to a printed spelling is a virtue on the page and a defect on a
soundtrack. Say so. Then name the register to preserve: "the narrator is a
village storyteller; the shouted lines stay raw and colloquial."

### 3.4 Name the specific defects you expect

Generic instructions get generic results. List the actual failure classes:

- archaic or dialect spellings a speech model will mispronounce
- metrical notation — inserted vowels marking sounded syllables in verse
- wrong case endings, wrong verb forms, wrong agreement
- words that are simply the wrong word
- numbers as digits, abbreviations, symbols
- anything unspeakable in one breath

### 3.5 Ask for the corrected text only

A numbered or labelled list. No commentary, no transliteration, no translation
back. Otherwise the next step is spent unpicking the reply.

---

## 4. The model is a first pass, not the authority

**Show the corrected lines to the user before recording anything.** Print the
before and after side by side so every change is visible at a glance, and ask
directly whether any of them is still wrong.

The user is the check on the language model, not the other way round. For a
culturally significant text this is not optional — a model will happily
modernise away the exact archaism that was the point.

Record the approved text in `script.md` and treat that file as canon.
**Recordings are made from `script.md`, never from the research notes, never
from the bible, never from the shot list.** Two sources of truth for the same
line is how half a film gets recorded from the corrected text and half from the
original.

---

## 5. It catches errors, not only style

On one production this pass turned century-old dialect into clean modern
standard usage throughout — and separately caught a plain factual error: the
wrong word for a common tool. That wrong word was already in the shot list, in
the narration, and in an image prompt. Nobody had noticed. The image had
already been generated with the wrong object in it.

The gate is a proofreading pass on the whole production's vocabulary, not only
on its grammar.

---

## 6. Content filters will block some lines

Speech models refuse text that reads as violent even when it is a hundred-year-
old folk tale. When a line is refused, **do not quietly drop it and do not
soften the story**. Rephrase the line so it carries the same meaning through a
different construction, then note the change and show it to the user with the
reason.

A line about killing is often accepted as an image ("blood spilled on his own
threshold") where the plain verb is refused. That is a phrasing problem, not a
story problem.

---

## 7. `script.md`

One file. The canon for every word in the film.

```
# Script — all text normalised through <model>, approved <date>

## Narration
N1  <corrected text>
N2  <corrected text>

## Dialogue
D1  <speaker> — <corrected text>
D2  <speaker> — <corrected text>

## On-screen text
TITLE    <corrected text>
CREDIT   <corrected text>

## Casting
<role>  <voice name>  <voiceId>  <which cues>
```

The casting block belongs here rather than in `audio.md` because it is the
thing most often lost between sessions, and a character whose voice changes
halfway through the film is a failure the user will hear immediately.
