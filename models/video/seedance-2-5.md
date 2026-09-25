# Seedance 2.5

**Maker:** ByteDance. **Magnific slug:** `bytedance-seedance-pro-2.5`. Magnific SOTA rank 1 for video. [catalog]
Older siblings: `pro-2.0` (to 4K, 15s), `fast-2.0`, `mini-2.0` (720p max, cheaper).

## Hard constraints [catalog]
- 4 to 30s. 1080p, 720p, 480p, Draft. Output mp4 or mov. Prompt up to 10,000 chars.
- Refs: image 30, character 30, **product 1, style 1**, colour, effect, video 10, audio 10. Native cap 50 combined. [official]
- **Every visual ref type is prohibited with start and end keyframes.** References or keyframes, never both. [catalog][tested]
- Audio refs work without a visual ref. `noMusic` flag available. 52 camera-motion presets.
- Multishot up to 6, each 1 to 12s.

## Best at
- One continuous take up to 30s. [catalog]
- Heavy reference control when there is no fixed start frame. [official]
- Native audio, lip sync, directed camera. [catalog]
- **Character performance.** Strongest of the three on a to-camera presenter. Native English, Spanish and Chinese takes each got distinct delivery, with the script adapted to suit the speaker's mannerisms. [tested] ByteDance lists native generation in 10+ languages. [official]
- Region-level editing and extension. [official]

## Weak at
- Cannot combine an approved start frame with identity refs. Garment drift risk from the third or fourth cut with a start frame alone. [tested]
- **Seedance 2.0, no start frame:** convincing UGC selfie look, but hand logic broke (a third hand touching a charm) and a charm duplicated on the bag. [tested] Add explicit hand-count and no-duplicate-prop lines; see the constraints block. [platform]
- Cost: 3,950 credits for 5s 1080p. [tested]
- Moderation refused a style note naming a film, director and cinematographer. No charge. [tested]

## How to prompt

Source for this section: ByteDance's own Seedance 2.5 prompting manual (released with the model, 31 Jul 2026), read via an English walkthrough, plus fal and platform guides. [official] unless tagged.

### Base formula
`subject + action or event` (required) + scene + visual style + camera or cutting + sound (all optional).
- Summarise the main process first; add detail only for the key action; never describe the same action twice.
- Resolution, duration, aspect ratio are parameters. Keep them out of the prompt.
- **Treat it as a producer reading a brief.** Say what happens, when, what each ref controls, what stays fixed, where the shot ends.

### References: prepare, then assign roles
- Native cap 50 assets. **Recommended** for stability: 1 to 8 image subjects, 1 to 5 video/audio subjects at 5 to 10s each. More assets, less stability.
- **Every asset gets a role, and a "do not take" when something could bleed in:**
  `@image1 supplies <BAKER>'s features, hair and grey apron. Do not take the background.`
  `@video1 supplies the rhythm of shaping the dough. Do not take the person, clothing or room.`
- **Bind each subject separately.** Never "@image1 to @image4 define four characters".
  `<PERSON A> corresponds to @image1; take appearance, hair and clothing only.`
- **Many assets:** group by type ([PEOPLE] [PROPS] [SCENES] [ACTION AND SOUND]), then a spec block for the key subject (appearance, fixed prop, where they appear, what they must never wear or hold).
- **Several views of one object:** separate images beat a packed grid. Say how many exist: "the four images define one single folding lamp; there is only ever one in the video".
- **Do not rely on text labels burned into ref images** to tell the model who is who. Write the mapping in the prompt.
- **A reference video that already carries the choreography:** say what it inherits; do not restate the moves (that conflicts with the asset).
- **Image for look, video for motion.** Do not give both the same job. [platform]
- On Magnific, refs are wired by type and bound by `@LibraryName`; the native `@image1` numbering is untested there. [tested]

### Long takes (15 to 30s): stages with end states
- Break into consecutive stages. **One main state change per stage**, and write the state **visible on screen** when it ends.
  ```
  [STAGE ONE] Opens with: ... Main event: ... Ends with: bouquet in her left hand; shears back on the right of the bench.
  [STAGE TWO] Carried over: ... Main event: ... Ends with: ...
  [KEEP CONSISTENT] identity, headcount, clothing, prop ownership, orientation.
  ```
- Prefer stages over timestamps. Use seconds only for a handover, entrance, transition or specific beat. Ranges must be continuous with no overlap.
- **A time block is a budget.** The model will not cut on the exact second. Too little content invites invention; too much drops beats. A 30s setting with one small action becomes waiting or slow motion. [platform]
- **Occlusion:** state how long the subject is hidden and repeat the details that must return unchanged. [platform]
- **Continuation:** use the final frame of clip one as the start of clip two; do not retell clip one. [platform]

### Sound and on-screen text syntax
| Bracket | Use |
|---|---|
| `( )` | music: `(calm piano underneath)` |
| `< >` | sound effect: `<a bell rings in the distance>` |
| `{ }` | dialogue: `{Hello, welcome back}` |
| `【 】` | subtitle text |
- Plain language also works; brackets disambiguate when several sound types coexist.
- **Language before non-Chinese lines.** Formula: language + regional variant + delivery + speaker + {line}.
  `Dialogue language: American English. The girl says it naturally and colloquially: {I thought you weren't coming.}`
- Suppress by category: "No background music; keep only dialogue, ambience and action effects." "No subtitles."
- **Dialogue as performance:** give each line a time block and say who keeps their mouth closed. [platform]

### Performance
- Emotion words set direction but leave acting open. Name 2 to 4 **observable** signals (gaze, brow, mouth corner, breathing, hands) for a single emotional turn.
- "She regrets leaving" becomes "she hesitates at the old sign, touches it, walks on". [community]

### Camera
- Basic terms go straight in (push, pull, pan, track, orbit, overhead, first person).
- For niche or ambiguous terms, keep the term and translate it into visible change: `Rack focus: focus moves from the foreground leaves to the figure behind; the leaves soften, her face resolves.`
- For popular moves say who it is built around and where it starts and ends (oner, dolly zoom, FPV, speed ramp, handheld with a named subject).
- **Screen space:** where the subject sits in frame, what event starts the move, whether the axis can be crossed. "Dynamic" carries no information. [platform]
- Numbers (aperture, focal length) are allowed, but the visible result is clearer.

### Physical action
- **Cause before reaction:** contact, resulting movement, sound, reaction, as separate actions. [platform]
- **Motion as contacts:** approach, contact, force transfer, landing, recovery. [platform]
- **Fluids and cloth:** direction of force plus settled end state. [platform]
- **Hands:** add explicit hand count and "no duplicated props" lines; our 2.0 run grew a third hand and duplicated a charm. [tested]

### Editing, extension, keyframes (native)
- **Edit:** declare `@video1 is the sole editing master`, then scope (object, region, time range, sound category), target asset role, what stays, and for replacements "the new object inherits every appearance, movement, occlusion and exit of the original". Aspect and duration lock to the source.
- **Extend forward:** describe the source's last-frame state first, then what happens next. **Backward:** describe what comes before, then write the source's first frame as an explicit end state, and say which later elements must not appear early.
- **First + last frame inside reference mode:** natively, 2.5 accepts `@image1 is the first frame... @image2 is the last frame...` in the opening lines alongside other refs, each anchor in its own sentence, same aspect ratio. **Magnific's catalogue prohibits visual refs with keyframes.** Whether declaring an image ref as the first frame in the prompt works through Magnific is the most valuable untested question in this file.
- **Storyboard grid:** gives order and rough composition only; under ~15 cells, clean line art, few labels, state reading order and "do not take the line-art style or labels".

### What it will not do [official]
Timestamps are not frame-exact cuts. Edits raise the odds of alignment with the source and guarantee nothing. Multi-asset jobs select assets per scene; they do not show all at once. Exact subtitles, signage, specs and frame-precise timing belong in pre-composited assets and post.

### Pre-submit checklist (condensed from the official 14)
1. Subject and main action clear?
2. Every asset has a take and a do-not-take?
3. Each person, product, prop named and bound?
4. Each long-take stage has one change and a visible end state?
5. Headcount, clothing, prop ownership, orientation stated as stable?
6. Emotions and niche camera terms cashed out as visible change?
7. First/last frames each in their own sentence, same aspect?

## Template [platform][official]
```
FORMAT: [single take or cuts], [real-time]
REFERENCE ROLES: <NAME> corresponds to @Image1; take [X] only. Do not take [Y].
STARTING STATE: [positions, held objects, camera]
STAGES: Stage 1 ... Ends with ... / Stage 2 ... Ends with ...
CAMERA: [path, screen position, when it starts and stops]
CONTINUITY: [identity, headcount, objects, direction, clothing]
AUDIO: {dialogue} <effects> (music or none); no subtitles
ENDING STATE: [final frame]
CONSTRAINTS: [no cuts, no slow motion, no duplicated props]
```
Delete sections that solve no problem in the shot.
