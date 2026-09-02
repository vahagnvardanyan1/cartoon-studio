# Directing

Scene construction, coverage, and the order a real animated production runs in.

---

## 1. A scene is a unit of change

Structure every scene as four things, written down before it is shot:

- **Objective** — what the point-of-view character wants *in this scene*.
  Concrete, actionable, pursuable in the next ninety seconds. Not their life
  goal.
- **Obstacle** — the person, fact or condition that resists it.
- **Turn** — the moment direction changes. New information, a forced choice, a
  refusal landing.
- **Value shift** — the charged pair that flips, with its polarity at the top
  and the bottom: safe→endangered, hopeful→disappointed, together→alone,
  trust→suspicion, ignorant→informed.

**The test: did something change that matters to the larger story?** Activity
is not change. A scene with no value shift should be strengthened, refocused,
merged, or cut.

In a short film — six to twelve scenes — enforce this absolutely. Every scene
flips a named value, and **consecutive scenes do not flip the same value in the
same direction.** Two scenes in a row going hopeful→disappointed is one scene
written twice.

Write the value shift into `shots.md` at the head of each beat. If you cannot
name it, that is the finding, and it belongs in the plan you show the user —
not something to paper over with better pictures.

---

## 2. Coverage

Standard coverage for a scene between two people:

| Setup | What it is for |
|---|---|
| **Master / establisher** | the whole scene wide. Teaches geography, provides the safety net |
| **Two-shot** | the relationship as one image |
| **OTS A / OTS B** | matched pair. The conversation as engagement |
| **Clean single A / B** | matched pair. The conversation as isolation. Save the drop to singles for the turn |
| **Inserts** | the object that carries the stake |
| **Reactions** | the listener; the third party; the thing being ignored |

Shooting order convention is **widest first, working closer** — the wide
teaches the space and every later setup matches to it, and performance
intensity naturally builds as the camera closes in.

**Coverage means something stricter in animation.** You do not shoot extra and
choose later; every shot costs. So the coverage decision is made in the
animatic: board the alternatives, cut the reel with them, keep what works, then
commit. **The animatic is animation's coverage.**

In a generated pipeline there is one exception worth knowing: a *reaction
close-up is the cheapest and most reliable shot the models produce*. When in
doubt about the budget, spend it on reactions.

---

## 3. Visual subtext

Meaning the dialogue does not state. Each of these is a rule you can apply
tonight.

- **Open on the object, not the face.** Begin a scene on the prop that carries
  its stake; the audience reads the whole conversation through it.
- **Put the argument in the frame.** Characters on opposite sides when their
  positions oppose; let one drift toward the other's side as they concede.
- **Let a character hold the power object.** Authority in the hand is authority
  in the scene. Pass the object to pass the power.
- **Geometry as allegiance.** Triangular groupings state hierarchy before
  anyone speaks; the apex holds power. Moving a figure from one leg to another
  shows a change of allegiance without a line.
- **Frame within a frame.** Doorways, mirrors, windows, railings — a secondary
  border says confined, observed, or divided.
- **Reframe without cutting.** Let actors and camera move so the composition
  changes inside the shot, and information appears and disappears at chosen
  moments. Cheaper than coverage, more sustained, and a natural fit for a
  pipeline where every cut is a continuity risk.
- **Lens as attitude.** Give a character a lens the way you give them a
  costume, and change it when they change. A character shot at 85mm all film,
  suddenly shot at 24mm from two feet, has been exposed — and the audience will
  feel it without being able to say why.
- **Light side as moral side.** Which side of the face the key falls on across
  a reverse pair is an editorial claim. Flipping a character from key side to
  shadow side over a scene is a moral turn.

---

## 4. Murch's Rule of Six

For every proposed cut, in priority order:

| | Criterion | Weight |
|---|---|---|
| 1 | **Emotion** — does the cut preserve what the audience should feel here? | **51%** |
| 2 | **Story** — does it advance the story? | **23%** |
| 3 | **Rhythm** — is it at a moment that is rhythmically right? | **10%** |
| 4 | **Eye-trace** — does it respect where the eye is currently looking? | **7%** |
| 5 | **Two-dimensional plane** — does it respect the 180° rule and screen direction? | **5%** |
| 6 | **Three-dimensional space** — is it true to the physical geography? | **4%** |

Two operating principles, both Murch's:

- **"If you find you have to sacrifice certain of those six things to make a
  cut, sacrifice your way up, item by item, from the bottom."**
- **"Satisfying the criteria of items higher on the list tends to obscure
  problems with items lower on the list, but not vice-versa."**

A cut that is emotionally right survives a spatial violation. A spatially
perfect cut does not survive being emotionally wrong.

**Encode it as a procedure:** if a cut fails only on 4, 5 or 6, make the cut.
If it fails on 1 or 2, find a different cut however clean the geography is.

This matters more in a generated pipeline than a filmed one, because the
temptation is to cut where the footage is cleanest. The footage is not the
criterion.

---

## 5. The order a real production runs in

**Development**

1. Premise → treatment → script. In animation the script is provisional; the
   boards are the real draft.
2. **Beat board** — a small set of drawings showing only the key story beats,
   drawn *before characters are designed*. One or two drawings should convey
   the mood. Its purpose is to prove you found the right moments before anyone
   invests in a shot list.
3. Character, environment and prop design.
4. **Colour script** — see `lighting.md` §7.
5. Storyboards — shot by shot.
6. **Voice record.** In animation, voice is recorded before animation, never
   after.
7. **Animatic / story reel.**

**Production**

8. **Layout** — camera placement, lens, staging and shot geometry committed.
   This is where the cinematography actually gets decided.
9. Blocking — key poses in *stepped* interpolation, approved before splining.
   The reason is precise: in spline mode, by frame 12 the curves are already
   halfway to the next key, so the pose is 50% gone and you cannot judge
   timing or clarity.
10. Splining, then polish — overlap, follow-through, arcs.

**Post**

11. Compositing → conform → sound design and mix → grade.

**The mapping to this pipeline:** beat board → the shot list's beat structure ·
storyboard → the keyframes · layout → the per-shot camera block · blocking →
the animatic · splining and polish → clip generation · post → `film-assembly`.
The stages have not gone away. They have changed medium.

---

## 6. Why the animatic gates everything

**"In animation, you edit first and shoot later."** The edit is not a
post-production stage; it exists from the beginning and is progressively
*replaced* with more finished material.

The three states of the reel:

1. **Radio play.** After the voice record, assemble an audio-only version —
   dialogue, temp effects, temp music. Story, performance and timing get
   established before a single image exists.
2. **Animatic.** Stills cut to that audio. Three editorial rules at this stage:
   keep all dialogue on screen; **cut slower than feels natural** — about four
   frames of air around dialogue shots, a two-second minimum on establishers;
   and lean hard on sound design, because the picture is not yet carrying the
   story.
3. **Progressive replacement.** Stills → clips, each dropped into the same
   timeline.

**Why it gates: the animatic is the only cheap place to discover that a scene
does not work.** Once a shot is generated its length is a budget line. Cutting
one extra second in the reel saves every downstream step. So the animatic is
watched, timed and re-cut until it plays — and only then does generation begin.

**The rule:** no shot is generated until its in-frame and out-frame exist as
compositions, its duration is locked in the reel, and the reel has played end
to end and worked *without dialogue explaining what the pictures failed to*.

---

## 7. Disney's twelve principles

Applicable whatever the render style, and several of them are direct prompt
instructions.

1. **Squash and stretch** — deform to convey weight while preserving volume.
2. **Anticipation** — a preparatory move in the opposite direction before the
   main action. *In a generated pipeline this is what makes the start keyframe
   right: the keyframe shows the loaded pose, not the rest pose.*
3. **Staging** — one clear idea per shot, directed by placement, silhouette,
   light and camera.
4. **Straight ahead vs pose to pose** — sequential (fluid, good for fire and
   chaos) vs planned keys with breakdowns (controlled, good for acting).
   *First-frame/last-frame conditioning is pose to pose.*
5. **Follow through and overlapping action** — loose parts drag behind and
   settle after the main mass stops. *This is the single most useful thing to
   write into a motion prompt; its absence is what "floaty" means.*
6. **Slow in and slow out** — mass takes time to accelerate and decelerate.
7. **Arcs** — natural motion travels on curves, not straight lines.
8. **Secondary action** — a supporting movement that enriches without competing.
9. **Timing** — frame count sets weight and scale, not only speed.
10. **Exaggeration** — caricature the truth rather than distorting it.
11. **Solid drawing** — respect volume and perspective; avoid twinning and
    symmetry. *Too-perfect symmetry is a named AI tell.*
12. **Appeal** — clear silhouette, distinctive shape language, readable
    proportions. Applies to villains as much as heroes.
