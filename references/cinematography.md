# Cinematography

The camera decisions that separate a film from a slideshow of generated
pictures. Every shot in the shot list must name a value from each of the four
axes in §1. A shot that does not is not yet a shot — it is a description.

---

## 1. The four axes. Specify all four, every time.

They are independent, and collapsing them is the single most common reason a
generated film looks amateur. "Close-up" is not a camera decision. "Close-up,
eye level, 85mm, locked" is.

| Axis | What it controls | Values |
|---|---|---|
| **Size** | intimacy | EWS · WS · FS · MLS · cowboy · MS · MCU · CU · ECU |
| **Height** | power | ground · knee · hip · shoulder · eye · high · overhead |
| **Lens** | credibility | 14 · 18 · 24 · 35 · 50 · 85 · 135 · 200 mm |
| **Movement** | attention | locked · pan · tilt · push · pull · truck · pedestal · crane · orbit · handheld |

A fifth, **depth of field**, is set by lens + distance + stop and should be
named when it carries meaning.

### 1.1 The size ladder

| Size | Frame line | What it is for |
|---|---|---|
| **EWS** | figure is a token in the landscape | scale, insignificance. Establishes world, not character |
| **WS** | whole body plus air | teaches the audience the geography. Isolation or grandeur |
| **FS** | head to toe, tight | whole-body performance — gait, posture, physical comedy |
| **MLS** | knees up | body and face both legible; environment still present |
| **Cowboy** | mid-thigh up | action and emotion at once. The standoff |
| **MS** | waist up | the workhorse. Also the *buffer* rung you land on before a CU so the CU still lands |
| **MCU** | chest up | dialogue default. Emotion with the door still ajar |
| **CU** | face fills frame | interior state. Every CU spends currency — the more you use the less each is worth |
| **ECU** | eyes, mouth, hands, the object | pressure, not intimacy. Detail invisible at any other size |

Three operating rules:

- **Escalate toward the turn.** The biggest close-up in a scene lands on the
  beat where the value flips. If your largest CU is not on the turn, the
  coverage is pointed at the wrong moment.
- **Pay off the wide.** If you never give the audience a wide, they never
  learn where they are, and every subsequent close-up floats.
- **Never cut adjacent rungs from the same position** (MS → MCU). See §3.2.

### 1.2 Lens as psychology

**The mechanism, which matters because a generated pipeline can decouple the
two and a real camera cannot:** focal length does not distort faces —
*camera distance* does. Holding a given framing forces you to a given distance,
and it is that distance which sets the nose-to-ear ratio. A portrait lens
flatters because it makes you stand back.

A **normal** lens equals the recording format's diagonal (~53° horizontal).
Full frame 43mm, Super-35 ~28mm. That is why **27–40mm reads as
neutral/documentary** — it renders perspective the way someone standing in the
room would see it. Everything wider is an editorial claim. Everything longer is
an editorial claim.

| Lens | Distance for a CU | Face | Background | Reads as |
|---|---|---|---|---|
| **14–18** | 1–2 ft | grotesque; nose balloons | enormous, swallows them | nightmare, mania, cruelty-comedy |
| **24** | 3 ft | large, immediate, slightly warped | expanded, context-rich | pressure, confinement, duress |
| **27–35** | 4–5 ft | mild shaping | present, legible | documentary, realist. The reportage default |
| **50** | 6–7 ft | as the eye sees it | balanced | the unmarked baseline; objective observer |
| **85** | 10–12 ft | flattened, idealised | peels into soft focus, comes forward | romantic, intimate-but-separate. The reaction lens |
| **135** | 16 ft+ | strongly compressed | claustrophobic | observation, not participation. Longing, surveillance |
| **200+** | far | maximally flat | foreground and background collapse into one plane | fate, voyeurism; a crowd becomes an impassable mass |

**The liar and the hero.** A character who is lying or unstable, in close-up:
go **wide and close** (24–32mm at 2–3 ft). The face enlarges, the room bends,
the audience is inside their space with no exit, and the background stays sharp
so we keep seeing the world they are lying about. The distrust is pre-verbal.
A character we should believe: go **long and back** (85–135mm). The face
flattens into its most idealised proportions and the background dissolves; the
frame says *this person is separate from and better than their circumstances*.

These are **conventions, not optics.** Teach them, then know that inverting one
— a long-lens liar, a wide-lens hero — is a legitimate authored move. Deakins:
"focal length, composition, position and movement of camera in space are only
tools and it's up to the filmmaker to assign meaning to them."

**Why 85mm+ isolates, mechanically:** three effects stack. Shallow depth severs
the subject from context; compression pulls the background forward and flattens
it into a field of colour so the character floats; and the required distance
means the observer is physically outside the conversation. The image encodes
someone who is not in the circle.

### 1.3 Height is a separate axis from angle

A camera can be at knee height and level (heroic, ground-anchored) or at knee
height tilted up (aggrandising). Different meanings. Name both.

- **Eye level** — neutral, peer. Note that many directors park slightly lower,
  at **shoulder level**, because true eye level looks flat and over-heady.
- **Above eye level, level lens** — diminished without the melodrama of a tilt.
- **High angle, tilted down** — vulnerability, being judged.
- **Hip / waist** — the standing-vs-seated transitional height; foregrounds
  hands and what they hold.
- **Knee** — dominance when tilted up; grandeur without going full ground.
- **Ground / worm** — monumentalises, obscures the face, makes the floor a
  character. A child's or an animal's world.
- **Overhead (~90°)** — removes agency; the frame becomes a diagram. Fate,
  surveillance, clinical detachment.
- **Dutch roll** is a fourth axis (rotation), not a height: destabilised mind.

**The mnemonic: height is power, size is intimacy, lens is credibility.**

### 1.4 Distance vs focal length — never say "zoom"

A zoom changes magnification only. A dolly changes the observer's position,
which changes the *relative* size of things at different depths.

- Dolly in: near objects grow faster than far ones, parallax occurs, the
  audience experiences travel.
- Zoom in: everything grows at the same rate. No parallax. There is **no
  equivalent of a zoom in human experience**, which is why zooms read as
  mediated and televisual — useful precisely when you want the audience to feel
  watched or reported on.
- Therefore **moving closer with a wide lens ≠ zooming in.** Wide-and-close
  gives a big face in an expanded present room; long-and-far gives the same
  size face against a flat absent room. Same framing, opposite meaning.
- **Dolly zoom** (push in while zooming out): isolates perspective change as
  the only variable. One per film, on a realisation.

**Generation note:** video models interpret the word "zoom" as pixel
enlargement. Always write **"dolly in"** or **"push in"**, and add
"perspective shifts naturally with parallax."

### 1.5 Depth of field

Four controls: stop, focal length, subject distance, format size.

- **Shallow (T/1.3–2.8, long, close)** — subjective, empathic. The world is out
  of focus because the character is not attending to it. Withholds information:
  good for suspense, bad for comedy.
- **Deep (T/8–16, wide, far)** — objective, layered, democratic. Foreground,
  midground and background can carry three simultaneous actions without a cut.
  Hands the audience the choice of where to look, which is itself a statement
  about the characters' agency.
- **Rack focus** is a cut you don't cut — it re-assigns attention inside a
  continuous shot and implies a link between the two planes.
- **Split focus** (focus between two subjects) refuses to choose. Useful for
  unresolved opposition.

**Pick a house stop for the film and deviate for meaning.** A film living at
T/1.4 has said the interior is the only real place; a film at T/8 has said the
world is real and the characters are in it.

---

## 2. Movement

### 2.1 What each move means

| Move | Mechanics | Meaning |
|---|---|---|
| **Pan** | rotate horizontally on a fixed point | reveals; connects two things by refusing to cut — "these are in the same space" |
| **Tilt** | rotate vertically | verticality and scale. Tilt up to a face = reverence; tilt down from one = judgement |
| **Push in** | camera approaches | increasing engagement, interiority. "We are entering this person" |
| **Pull back** | camera retreats | reveal of context; abandonment. The standard "and then they were alone" |
| **Truck** | slides laterally | parallax turns the world into a scrolling relief; walks beside a character as a peer |
| **Pedestal** | rises or lowers *without tilting* | pure height change — alters the power reading at a constant look-angle. Underused and very precise |
| **Crane / jib** | boom plus arc | ceremony, scale. The pull-up-and-away ending = release, the world continuing |
| **Handheld** | unstabilised | immediacy and instability. Intensity scales with amplitude — micro-jitter reads "real", violent shake reads chaos |
| **Gimbal / Steadicam** | stabilised walking | a gliding disembodied observer. Uncanny slow, immersive fast |
| **Orbit** | circles the subject | circling one character says the world turns around them; circling two says they are locked together |
| **Whip pan** | very fast pan into blur | energy, comedy, or a hidden cut |
| **Locked off** | nothing | the frame as a stage. Underrated; a locked frame returned to twice is a rhyme |

### 2.2 Motivated, not decorative

- **Move for one of five reasons only:** to travel through space and reveal it;
  to follow a subject; to build tension; to change emotional proximity; to mark
  a decision or a realisation. If the proposed move is none of these, lock it
  off.
- **A move must start on a composition and end on a composition.** Both the
  first and last frames have to work as still images; the middle is transit.
  If either end is a bad frame the move is decorative. *In a generated
  pipeline this is literal: generate the in-frame and the out-frame as two
  stills and let the model interpolate.*
- **Do not invent character movement to justify a camera move.** Block the
  scene for truth, then find the camera. Unless the camera is a character's
  POV it should have no say over the blocking.

### 2.3 Speed

- **The slow push-in works because it is subliminal** — the conscious mind does
  not register the movement, so the effect passes without defence. The audience
  feels itself leaning in without deciding to. Coppola's pull-back across
  Bonasera's monologue runs over two and a half minutes.
- **A move must land.** Arrive at the final composition on or just before the
  line that carries the beat, then hold. A move still travelling when the beat
  lands steals the beat.
- **Speed is meaning:** slow = involuntary and psychological; medium =
  purposeful and observational; fast = an external force acting on the
  character. Ease-in-ease-out reads as thought; a linear snap reads as shock.

### 2.4 In a generated pipeline

- **One primary camera move per generation.** Stacked moves produce jitter and
  drift. If a sequence needs two, that is two shots.
- **Attach a speed word to every move.** "Slow, deliberate, steady, rapid" — or
  an explicit duration: "slow 5-second dolly in."
- For a multi-phase move, **describe what is in frame at each phase** rather
  than stacking movement verbs.
- **Add the handheld tremor in post, not in the prompt.** Models produce
  weirdly smooth motion with no micro-vibration; a real operator has weave and
  breath. The usable spec is "shoulder-mounted, a real operator's breath and a
  constant fine 1–2cm tremor."

---

## 3. Blocking, staging and screen grammar

### 3.1 The 180° rule

Draw an **axis of action** through the two subjects. Keep every setup within
the 180° arc on one side. Characters then hold a consistent left/right
relationship and A always looks screen-right while B looks screen-left. Cross
it unprepared and the audience momentarily believes the characters have swapped
places.

**Write the line into the canon at the top of each location** — "shop on the
RIGHT of frame, lane running off LEFT, the visitor enters from LEFT" — and
paste it into every prompt set in that location. The model has no memory of
your geometry.

The five legitimate crossings:

1. **Move the camera across the line on screen** in an unbroken shot, so the
   audience witnesses the transition and re-maps the space.
2. **Cut to a neutral shot on the line** — straight down the axis, or from
   directly behind a head. That shot belongs to neither side; exit it on the
   far side.
3. **Let a character re-establish the line** — someone stands and crosses. New
   blocking creates a new axis and the old one no longer binds.
4. **Cut away** to something unoriented (an insert, a detail), then return on
   the new side.
5. **Overhead** — a top shot re-diagrams the space and is directionally
   neutral.

### 3.2 The 30° rule

Between two successive shots of the same subject the camera must move **at
least 30° around it**. Below that the two frames are too similar for the brain
to register a new viewpoint, so it registers a discontinuity in *time* instead
— a jump cut.

Corollary: changing focal length instead of angle needs **~20mm of change** at
the same angle. In practice: **change angle by ≥30°, or change image size by a
full rung of the ladder, or both.** The 30° rule lives inside the 180° rule,
leaving a 150° working band on one side.

### 3.3 Shot / reverse — the backbone

Shot-reverse variants make up about **50% of all shots in popular narrative
cinema**. Get this right before anything else.

- **Matched pair conventions:** same shot size, same focal length, matched
  eyeline heights, equal looking room, and the two characters on opposite sides
  of frame — A on the left third looking right, B on the right third looking
  left. Break these deliberately to imbalance a scene.
- **Eyeline match** must agree in *direction and vertical angle*. If A is short
  and B is tall, A's single tilts up and B's tilts down. Failing the vertical
  is the most common eyeline error in an animated pipeline, because the default
  is level.
- **Over-the-shoulder:** the foreground shoulder is a pressure gauge — the more
  of A intrudes, the more A crowds B. A **dirty single** keeps a sliver of A; a
  **clean single** removes A entirely, which is how you say *they are now
  alone*. **Dropping from OTS pairs to clean singles at the scene's turn is the
  most reliable coverage gesture in the language.**

### 3.4 Screen direction

- **Strong direction** = movement parallel to the lens. **Neutral** = movement
  toward or away from camera; a subject coming straight at camera can exit into
  any new direction, which is the cheapest legitimate way to re-map a chase.
- **Exit frame right → enter the next shot frame left**, so the trajectory
  continues across the cut.
- **In a chase, pursuer and pursued travel in the SAME screen direction.**
  Opposite directions read as convergence — that is a collision or a
  rendezvous, not a pursuit.
- **Western reading bias:** left-to-right reads as progress, right-to-left as
  regression or return. A tiebreaker, not a law.

### 3.5 Staging in depth vs laterally

- **Lateral staging** (spread across the frame's width) puts characters in
  *opposition* — left versus right is a debate. Easy to read, flat.
- **Depth staging** (foreground / midground / background) puts them in
  *hierarchy* — near is powerful, far is subordinate, and the audience
  discovers the background figure second. Tools: doorways and corridors centre
  frame for entrances; movement toward and away from the lens; one body
  obscuring another face.
- **Depth staging lets a whole scene play without a cut.** In a generated
  pipeline that is a direct saving: one shot with internal reframing replaces
  six, and avoids six continuity joins.
- **Distance is emotional currency.** Inches apart is intimacy or
  confrontation; ten feet apart is emotional walls.
- **Levels encode power.** Standing over seated is dominance; side by side is
  equality. **Who approaches and who retreats is the scene's power graph.**
- **Furniture is punctuation.** A table or a counter is a barrier; crossing to
  the same side of it is a plot event.
- **The mid-scene re-block is the strongest directorial tool.** Stage the scene
  so the character who begins in the power position — nearer, higher, centred,
  facing camera — has physically swapped to the weak position by the end.
  Reframe by moving the actor, not by cutting, and the shift feels discovered
  rather than announced.

### 3.6 Headroom, lookroom, thirds

- **Headroom:** put the **eyes on the upper third line** and correct headroom
  falls out automatically at every size. Too much headroom reads amateur and
  sinks the subject; cropping the crown in a CU is normal and reads as pressure.
- **Lookroom:** space in front of the gaze or the travel. Looking screen-left
  means placed right of centre.
- The spectrum and its meanings:
  - **Maximum lead room** — isolation, backed into a corner. Put another
    character in that void and they now dominate the frame.
  - **Thirds lead room** — balance. Two thirds-framed characters cut together
    with *no compositional tension*, which is exactly why a scene shot entirely
    this way feels inert.
  - **Centre framing** — control, formality, a claim of authorship.
  - **Short-siding** (pushed toward the edge they are looking at) — trapped,
    wrong-footed, unbalanced.
- **Break the rule of thirds when the character is broken.** The rule exists so
  that departures are legible. A film that never uses thirds has no way to
  signal wrongness.

### 3.7 The silhouette test

If the staging does not read in pure black-and-white silhouette, restage it.
Run this on every keyframe before generating motion from it. It is the single
cheapest staging check available and it catches limbs merged into torsos, props
lost against backgrounds, and two characters occupying the same visual mass.

---

## 4. The per-shot camera block

Every shot in `shots.md` carries this, filled in. No blanks.

```
SIZE      MCU
HEIGHT    shoulder, level
LENS      85mm
DOF       shallow, background falls off at 2m
MOVE      locked            (or: slow push in, 12cm over 4s, landing on X)
LIGHT     key 3/4 back camera-left, 4:1, hard, motivated by the window
AXIS      A screen-left, B screen-right; line runs along the counter
DIRECTION he entered from frame left and stays left of her
IN-FRAME  <what the first frame is>
OUT-FRAME <what the last frame is>
JOB       one sentence: what this shot is FOR
```

The **JOB** line is not decoration. "Camera clutter — the shot list names
angles but not what each shot is *for*" is a named root cause of incoherent
output. A shot that cannot state its job in one sentence should be
merged with its neighbour or cut.
