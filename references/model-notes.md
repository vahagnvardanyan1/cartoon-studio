# Picsart GenAI — practical notes

Discover, don't assume. Model names, prices and parameters change. Use
`picsart_model_catalog` to see what exists, `picsart_model_params` for a
model's exact schema, and `picsart_preflight` to validate and price a call
before spending credits. Check `picsart_credits` before a large batch.

What follows is the shape of the pipeline and the constraints that bit us.

## Choosing models by job

| Job | What to look for in the catalog |
|---|---|
| Reference art, character sheets, keyframes | An image model that accepts **many source images** — that is what holds identity |
| Motion | A video model supporting **start/end frame control** and reference images |
| Cheap drafts | A "fast" or "mini" variant of the same video family |
| Speaking shots | An **avatar / audio-driven portrait** model — these preserve the real audio |
| Voice | A TTS model that genuinely supports your language (verify, don't trust docs) |
| Music | A long-form music model — check its maximum duration before planning cues |
| Sound effects | A dedicated SFX model, typically short clips |
| Final render | The media compositor (`picsart_media_*`) |

**Text / language work.** The catalogue has LLMs under `mode: "text"` —
`gpt-5.5`, `claude-opus-4-8`, `claude-sonnet-4-6`, `gemini-3-pro` and the
Gemini Flash tiers. Reach for one to **normalise non-English narration and
dialogue before recording it** (see `voice-and-audio.md`), and to sanity-check
any culturally specific term before it reaches a prompt. Keep batches to eight
or ten lines — longer prompts have timed out at the MCP call's 60-second limit.

## Hard constraints learned the hard way

**Reference image payload cap.** Passing several high-resolution reference
images in one request can exceed the inline media limit and fail. Keep to about
two 2K images per call; describe the rest in words.

**Frames and reference media are mutually exclusive.** On the main video model
you may pass *either* start/end frames *or* reference media (images/audio) —
never both. Two errors reveal this:
- `reference image, video, or audio content cannot be mixed with both first and last frame images`
- `first/last frame content cannot be mixed with reference media content`

This forces the split:
- **Silent shots** → start frame + end frame (best camera control)
- **Speaking shots** → dedicated lip-sync model with portrait + audio

**Supplied audio is re-synthesised, not played.** A general video model treats
an audio input as a *style reference*. Foreign-language dialogue comes back as
convincing-sounding nonsense. Only avatar/audio-driven models play the actual
file.

**Video calls should run async.** Submit with `async: true`, then poll the job
handle. A synchronous video call can be severed by the host while the render
continues and still charges.

**Generated MP3s often carry no duration in the header.** A probe returns no
`durationSeconds`. Derive it from file size and bitrate (a 128 kbps file is
about 16,000 bytes per second), or declare a generous duration — over-declaring
adds silence, under-declaring truncates the line.

## The compositor

`picsart_media_quickstart` returns ready-to-run recipes — call it before
hand-building a scene.

**Concatenating clips:** probe one clip for exact dimensions and frame rate,
then use the montage template in `bootstrap` mode with one entry per clip.
Composition duration derives from the clips; do not set it by hand.

**Audio does not go in `layers`.** This is the trap: the schema validator
happily accepts an audio asset as a layer, and then the renderer refuses it —
`media asset type 'audio' on layer ... is not supported`.

Audio belongs in a **top-level `audio` array**, with each track referencing an
entry in a top-level `assets` array by `assetId`:

```json
{
  "composition": { "width": 1920, "height": 1080, "fps": 24, "duration": 185 },
  "assets": [ { "id": "vo1", "type": "audio", "uri": "https://...", "duration": 6 } ],
  "layers": [ { "id": "film", "start": 0, "duration": 185, "content": { "kind": "media", "asset": { "type": "video", "uri": "https://..." } } } ],
  "audio":  [ { "id": "t1", "assetId": "vo1", "start": 1.2, "duration": 6, "volume": 100 } ]
}
```

`volume` is a percent (0–100). Music sits around 25–30 under dialogue. Fades go
in `animations.volume.keyframes`, with times relative to the composition.

**Inspecting your own work:** `picsart_media_contact_sheet` renders frames from
a scene and returns them as images you can actually look at. Wrap any finished
clip in a one-layer scene and sample it. This is the only reliable quality
check — never present a clip you have not inspected.

## Rough economics

Drafting at low resolution costs roughly a quarter of a full-resolution render.
For a three-minute film of ~22 shots, budget approximately:

- reference art: a few dozen images
- one low-res draft per shot, plus retakes
- one full-res render per approved shot
- voice, music and sound effects: minor by comparison

Preflight the actual numbers for the models you pick, and tell the user the
total before you start spending.

---

## Video audio — two different tools, do not confuse them

### Non-dialogue shots: let Seedance generate the sound

`generateAudio: true` on Seedance produces sound **synchronised to the motion
it actually rendered** — the bark lands on the lunge, the dust lands on the
feet, the crackle follows the real flame. This beats a separately generated
effects bed, which always needs manual sync and never fits as well.

Describe the sound explicitly in the prompt, in its own block, or the model
invents music and modern noise:

```
SOUND: one hard deep bark, a low guttural growl, heavy claws scrabbling in
dry grit, the thud of body weight hitting the ground, then abrupt silence
with only a dry wind and distant sheep bells. No music. No human voices.
```

Always say what must **not** be there. "No music" is worth including every time.

> **`generateAudio` defaults to `true`.** If a clip must be silent, turn it off
> by hand. This is the opposite of what the earlier version of this file said.

### Dialogue shots: OmniHuman, never Seedance reference audio

Seedance's `audioUrls` slot treats a supplied track as a **style reference and
re-synthesises it.** Feed it Armenian and you get something with Armenian
prosody and no Armenian words. This destroyed a whole film's dialogue once.

**`bytedance-omnihuman-v1.5`** takes a portrait image plus a real audio track
and animates the face to it. The audio passes through untouched, so the
language survives exactly as recorded.

```
model: bytedance-omnihuman-v1.5
extra: { imageUrls: [<one portrait>], audioUrl: <the real speech track> }
```

Constraints found in practice:
- **One portrait only.** A two-shot with both characters speaking cannot go
  through it — that shot stays Seedance mouth-movement with the dialogue laid
  under it in the edit.
- Output came back **1920×1088 at 25fps** while Seedance clips were 864×496 at
  24fps. The compositor handles the mismatch with `fit: "cover"`; just declare
  the real dimensions on the asset.
- It is **slow** — several minutes, and it sits at 99% for a long time. Fire it
  early and do other work while it runs.
- `kling-avatar` is the alternative but has burned garbled subtitles into the
  picture in past runs. Prefer OmniHuman.

---

## Seedance 2.0 parameters, verified

| Param | Values |
|---|---|
| `duration` | any whole number **4–15** |
| `resolution` | 480p, 720p, 1080p, 4k |
| `aspectRatio` | 16:9, 9:16, 1:1, 4:3, 3:4, 21:9, adaptive |
| `generateAudio` | **defaults true** |
| `startFrame` / `endFrame` | one image each |
| `imageUrls` | up to 9 reference images |
| `returnLastFrame` | gives you the true last frame for chaining |

**Frames and reference media are mutually exclusive.** Give it start/end frames
*or* reference images, never both — it errors.

---

## Operational failures to expect

- **The MCP call times out at 60s on image generation** even though the job
  succeeded or failed server-side. Retry the prompt; roughly one call in six
  timed out across ~60 image generations.
- **Occasional `image_url ... timeout while fetching resource`** on a video job
  whose start frame lives on the CDN. Re-fire the same job; it usually works
  the second time.
- **Video generation is async by default.** You get a job handle. A 5–8 second
  480p clip takes roughly 2–4 minutes. Fire a whole beat at once, then poll.
- **`picsart_media_probe_media` cannot read MP3 duration.** Estimate from bytes
  at 128 kbps (`bytes × 8 ÷ 128000`), which has matched the displayed length
  every time, and give audio tracks a little headroom in the scene.
