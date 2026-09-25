# Wan 2.7

**Maker:** Alibaba Tongyi, Apr 2026. **Magnific slug:** `wan-2-7`. [catalog]
**Status on our projects:** never run. Wan 2.6 was run and failed on identity and performance (see `wan-2-6.md`). 2.7 is the version that fixes the ref gap on Magnific.

## Hard constraints [catalog]
- 2 to 15s. Up to 1080p. Audio yes.
- Refs: image 5, video 5, character 1, product 1, style 1. **Start frame plus refs together: yes.**
- Native modes: text, first frame, first and last frame, continuation, reference to video, instruction editing. "Thinking mode" plans complex prompts. [official][platform]

## How to prompt

### Formulas [official]
| Job | Formula |
|---|---|
| Exploration | Entity + Scene + Motion |
| Controlled | Entity (described) + Scene (described) + Motion (amplitude, speed, effect) + Aesthetic control + Stylisation |
| From a start frame | Motion + Camera movement only. The image already defines entity, scene, style |
| With sound | add Voice / SFX / Music (below) |
| Multi-shot | Overall description + Shot number + Timestamp + Shot content |
| References | Reference identifier + Action + Scene + Lines (optional) + Music (optional) |

- **Most weak prompts skip aesthetic control and stylisation, and get a static camera in an undefined void.** Cover all five. [official]
- Aesthetic control = light source, lighting environment, shot size, camera angle, lens, camera move.
- Motion needs amplitude and speed: "swaying violently", "moving slowly".
- To hold the camera: `fixed camera`.
- Naming two light sources with colour temperatures and a shot size plus move did more than any quality adjective. [community, Wan 3 test]

### Camera intent [official]
Push-in = intimacy or tension. Pull-out = scale or isolation. Tracking = viewer alongside. Orbit = importance; keep the arc under 45 degrees or space distorts. Fixed = stillness.

### Sound [official]
- Voice = line + emotion + tone + speed + timbre + accent: `He says, "Study hard," in a relaxed tone, at a moderate speed, with a clear voice, in American English.`
- SFX = source + action + ambient: `A glass ball falls onto a wooden floor, making a thud in a quiet room.`
- Music = score + style.
- **Wan fills gaps.** If lines are not written, it invents dialogue; if music is not mentioned, it picks some. Suppress with `No dialogue.` and `No background music.` (English wording exact).

### Multi-character dialogue, four rules [official]
1. Unique, consistent labels, no pronouns: `[Character A: Black-suited Agent]`.
2. Anchor the line to an action first: `The agent slams his hand on the table. [Black-suited Agent, angrily]: "Where is the truth?"`
3. Distinct voice labels per character: `[Agent, raspy deep voice]`.
4. Link turns in time: `Immediately, [Assistant]: "Because it's time."` Without a linker, speech can merge.

### Multi-shot [official]
```
A short play about losing and regaining hope, third person.
Shot 1 [0-3 s] A boy sits alone in a corner of the playground, looking down at a letter.
Shot 2 [4-6 s] Hard cut, fixed camera, close on his eyes glistening with tears.
Shot 3 [7-10 s] Hard cut to a classroom. A girl walks over with a warm, determined smile.
```
Wan 2.7 dropped the `shot_type` parameter. For one shot, write `Generate single shot.`

### References [official]
- Refer to uploads as `Image 1`, `Video 1` (capital, space, number). Images and videos are numbered separately by upload order. One ref of a type can be "reference image".
- Either direct (`Image 1 in Image 2`) or with content (`the cat in Image 1 plays in the room in Image 2`).
- Reference video carries appearance, motion, voice timbre and background.
- On Magnific, test whether `Image 1` numbering survives, or bind with `@LibraryName`.

### What not to prompt [official]
- Exact legible text.
- Lip sync to exact words ("does not work reliably" per Alibaba).
- Rapid scene changes inside one clip without multi-shot structure.
- Long choreographed sequences. Keep actions simple and short.

## Open questions
- Does 2.7 hold identity from a start frame plus one character ref where 2.6 failed?
- Does performance improve over 2.6's flat delivery?
- Does Magnific expose thinking mode or `prompt_extend`?
