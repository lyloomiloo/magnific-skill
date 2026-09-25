# Kling 3.0 family

**Maker:** Kuaishou, Feb 2026. Merges Kling 2.6 (motion) and O1 (consistency) into one model. [community]

| Variant | Slug | Refs | Start/end | Audio | Max | Res |
|---|---|---|---|---|---|---|
| Kling 3.0 | `kling-30` | char 3, product 3, image 3, **all require start frame** | both; end needs start | yes | 15s | 720p, 1080p, 4K |
| Kling 3.0 Omni | `kling-omni3` | char 3, product 3, image, video 1; **no start-frame requirement** | both; image refs not with end frame; end frame barred if >1 upload | yes | 15s | 720p, 1080p, 4K (no video ref at 4K) |
| Kling 3.0 Turbo | `kling-30-turbo` | none | start only | no | 15s | 720p, 1080p |
| Kling 3.0 Motion Control | `kling-motion-control-30` | video 1, start is a video | | no | 15s | 720p, 1080p |

All: prompt 2,500 chars, multishot up to 6 shots, 16:9 / 9:16 / 1:1, 3 to 15s. [catalog]

## Best at
- **Shots from an approved start frame with references still holding identity.** The inverse of Seedance, and why it won UC02. [tested]
- **Motion reads filmed:** bodies carry weight, hair moves correctly, camera moves feel choreographed. Wardrobe, palette and treatment carry through from the start frame. [tested, manual review]
- Cost: 450 credits for 5s 1080p, roughly a ninth of Seedance 2.5. [tested]
- Native multi-shot storyboard in one generation. [platform]
- Tolerated named film references that Seedance refused. Still do not rely on it; describe the look. [tested]

## Weak at
- 15s ceiling. Longer takes need Seedance 2.5.
- Base 3.0 cannot use refs without a start frame. Use Omni for that.
- **Hand-object mechanics.** Failed to show charms being clipped onto a bag; hands and props did not follow the directed steps. Likely worsened by over-direction. [tested] Hands, jewellery and fine props are a known weak zone, worst in close-ups. [community]
- **Kling 2.6 Motion Control** copied the source clip's motion, audio and script too faithfully, leaving no room to redirect performance, and takes no product references. [tested][catalog]

## How to prompt

### Core [platform][official]
- **Direct a scene.** Scene, characters, sequential action, camera, audio, style. Write like a director of photography, not a caption.
- **Lead with camera language.** "Handheld tracking shot following..." sets the whole generation. Reads well: tracking, orbit, macro close-up, POV, whip-pan, slow push-in, static wide, handheld with slight drift.
- **Explicit camera, always.** Without it the camera improvises. Official demos tie camera to action: "tracks her as she walks and freezes instantly when she pauses". [official]
- **Anchor subjects early** and describe them identically in every shot.
- **Sequential actions:** "First she looks up, then turns to the window, finally smiles."
- **One main action per shot.** Split complexity across shots.
- **Motion endpoints:** end on "then settles" or "returns to rest". Open-ended motion hangs or drifts.
- **Hold things still in words:** "The [element] stays completely fixed throughout."
- **Existing text in the start frame is preserved** if you point at it: "The camera remains fixed on the word KLING on the bat as he swings." [official] Still add brand text in post.

### Length
- Platform guides: 100 to 200 words. [platform]
- Official long-take demos run 200 to 300 words, but every clause is a timed beat: "At the 4th second...", "At the 8th second...", "In the final 3 seconds...". [official]
- Rule: 100 to 200 words for a short take or per shot. Go longer only for a single 15s take, and only with second markers.

### Single take vs multi-shot [official]
- **Multi-Shot on, no custom shots:** the model plans cuts itself and may collapse to one shot if the scene suits it.
- **Custom Multi-Shot:** strict. Official demos keep each shot short: size + angle + one action + camera.
  `Shot 1 (3s): Low-angle rear wide, tracking behind the rider. Shot 2 (2s): Low-angle side close-up of the wheel. Shot 3 (2s): First-person POV, handlebars ahead.`
- Keep 4 to 6 shots across 10 to 15s. [platform]
- **One take:** say so explicitly, twice if needed: "one continuous long take without any cuts". [official]

### Dialogue and voice [official]
- Speaker label, delivery in brackets, then the line:
  `Mom (softly, in a surprised tone): Wow, I didn't expect this. Dad (low voice, calm): Yeah, never thought that would happen.`
- Language per line: `Boy (casual tone, Korean): "..."`. Five languages native (ZH, EN, JA, KO, ES); others are translated to English.
- Accents and dialects by tag: "in English with an Indian accent", "in Cantonese". Code-switching inside one scene works.
- If a bound element already carries a voice, do not restate the tone in the prompt.
- Dialogue in target language, rest in English. [platform]

### References on Kling 3.0 (start frame + elements) [official][tested]
- Elements lock character, item or scene across camera moves. Build from 2 to 4 images (front, three-quarter left, three-quarter right, back), or a 3 to 8s video that also captures voice.
- **Bind references by name** at the point the person appears, e.g. `@DSG_Sheet_Emma_LookA`. On Magnific the server rewrites the token into the reference description. Unbound refs drift in crowds. [tested]
- **Arrivals need an end frame.** Charms landing on a bag were fixed by an end frame showing them hung correctly. Skip the end frame for one-way motion. [tested]

### Kling 3.0 Omni specifics [official]
- Treats images, videos, elements and text all as prompt. Refs are called inline with `@`.
- Official demo grammar: elements as actors, images as stage or look.
  `Shot 1 (3s): Mid-shot, background @Image. @Grace sits on the sofa as @Alan walks in holding @Samoyed.`
  `...Cinematic look @image1.` (an image ref used as the style reference, called at the end)
- Limits native: up to 7 images/elements without a video, 4 with a video; video ref 3 to 10s. Magnific: char 3, product 3, image, video 1. [official][catalog]
- API note: avoid element names that collide with words in the prompt. [official]
- No start frame required, so refs can drive the whole shot. Image refs cannot combine with an end frame on Magnific. [catalog]

### Template
```
[CAMERA: shot size, angle, move]. [SUBJECT @Bound] [one action], then [second action], then settles.
[SETTING @Image as background]. [LIGHT]. [Speaker (delivery, language): line].
The [element] stays fixed throughout. [One continuous take / Shot list].
```

## Community fixes for body motion [community, untested]
- Describe foot contact (heel to toe) to stop gliding walks.
- Match camera speed to the subject and keep the subject centred; proportions hold better.
- Slight handheld motion hides over-clean backgrounds.

## Open questions
- **Omni has never been run.** On paper it is strictly more flexible than 3.0 for UC02-style work. Highest-value test.
- Turbo quality versus 3.0 for silent drafts.
