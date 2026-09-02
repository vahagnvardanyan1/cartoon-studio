---
name: film-cutdown
description: Cut a trailer, teaser or vertical social edit from a finished film by ranking its moments and selecting the best non-overlapping windows. Use when the film is done, or when the user says "/film-cutdown", "make a trailer", "cut a teaser", "make a vertical version", "clip this for social", "make shorts from this".
---

# Cut down the film

Take a finished film and produce a shorter edit from it: a trailer, a teaser,
or a vertical cut for a phone. This is a **selection** problem, not a
generation problem — nothing new is generated, and the discipline is in what
you leave out.

## Inputs

| Name | Required | Default | What it is |
|---|---|---|---|
| `source` | yes | — | the finished film, or the running cut |
| `format` | no | `16:9` | `16:9` · `9:16` · `1:1` · `4:5` |
| `target` | no | 30s | how long the cutdown should run |
| `count` | no | 1 | how many separate cutdowns to produce |
| `purpose` | no | trailer | trailer · teaser · social · festival submission |

Platform targets, when the user names one rather than a length:

| Platform | Ratio | Sweet spot |
|---|---|---|
| Vertical short (TikTok, Reels, Shorts) | `9:16` | 30–75s |
| Feed | `1:1` | 15–45s |
| Portrait feed | `4:5` | 30–60s |

## 1. Score the film's moments

Go through the finished cut and mark every candidate window with a score and a
reason. Score against these eight categories — a moment that hits more than one
scores higher:

- **Hook** — an opening image or line strong enough to stop a scroll
- **Emotional peak** — laughter, grief, rage, awe
- **Revelation** — the "wait, what?" reframe
- **Conflict** — the moment two things collide
- **Story peak** — the climax of an arc
- **Quotable line** — tight enough to screenshot
- **Striking image** — a frame that works with the sound off
- **Turn** — where a named value flips

For each candidate record, as first-class fields rather than a bare number:

```
start · end · score · hook — the first line or image · why — one sentence
```

The **why** field is what makes the selection reviewable. A list of timecodes
and scores cannot be argued with; a list of reasons can.

## 2. Dedupe overlapping candidates before selecting

**This is the step people skip and it is what ruins a cutdown.** Peaks cluster:
a strong thirty seconds will generate five overlapping candidate windows that
are all essentially the same moment. Take them all and your "top five" is one
scene shown five ways.

Sort by score, walk the list, and **discard any candidate that overlaps one
already kept.** Only then take the top N.

## 3. Separate selection from rendering

Present the selection **as timecodes with their reasons, before rendering
anything.** The user approves the choice of moments; then you cut.

This means a rejected selection costs one conversation instead of one render,
and a re-cut with different moments does not re-do the scoring.

## 4. Cut it

- **The hook lands in the first second.** Not the first five. For a vertical
  cut this is the whole game.
- **Cut faster than the film does.** A cutdown is not the film at a smaller
  size; hold times drop by roughly a third from the feature cut.
- **Carry the sound across the joins.** Audio bridges are what stop a
  compilation of moments reading as a compilation of moments.
- **Do not narrate what the film already shows.** If the trailer needs a voice
  explaining it, the moments are wrong.
- **Never spoil the turn** in a teaser. In a trailer, spoil it only if the film
  is a comedy and the turn is the joke.

### Reframing for vertical

A `16:9` film recut to `9:16` loses two thirds of every frame. Two rules:

- **Reframe per shot, not per film.** A static centre crop throws away the
  composition the film was built on — and every wide becomes unreadable.
- **Wides usually cannot be saved.** Replace them with the closest available
  shot rather than cropping into mush. If the film has no close coverage of a
  beat, that beat does not go in the vertical cut.

## 5. Do not pad

If the film honestly contains four moments worth cutting and the user asked for
six, **return four and say so.** Padding a cutdown with weak material is how a
good film gets represented badly, and the two filler clips are the ones people
judge it on.

## Done criteria

1. Candidates were scored, deduped for overlap, and the surviving list was
   shown to the user with reasons before anything rendered.
2. The hook lands inside the first second.
3. The cutdown holds the target length within a couple of seconds.
4. Every shot in a reframed cut was reframed individually.
5. Nothing was padded to hit a requested count.

## Failure modes

| Symptom | Cause |
|---|---|
| Five clips that are all the same scene | overlapping candidates never deduped |
| Reads as a compilation, not a trailer | no audio bridges across the joins |
| Vertical cut is unreadable | static centre crop instead of per-shot reframing |
| Nobody watches past two seconds | the hook is at 0:05, not 0:00 |
| The last two clips are weak | padded to hit a requested count |
