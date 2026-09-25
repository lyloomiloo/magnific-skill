# Veo 3.1

**Maker:** Google DeepMind, GA Oct 2025. **Magnific slug:** `google-veo3_1`. Siblings `veo3_1-fast`, `veo3_1-lite` (no refs). [catalog]
**Status on our projects:** never run. Everything below is [catalog], [official] or [community].

## Hard constraints [catalog]
- 4, 6 or 8s only. Up to 4K. 16:9 or 9:16 only.
- Image refs: 3. **Start frame plus refs together: yes.**
- Native audio: yes.
- Native features (check Magnific exposes them): image to video, "ingredients to video" (refs), first and last frame, scene extension. Add/remove object runs on Veo 2 with no audio. [official]

## Best at [official]
- Synchronised audio: multi-person dialogue, timed effects, ambience from the prompt.
- Narrative and character interaction; strong adherence to cinematic terms.
- First-and-last-frame transitions with audio.

## Weak at [community]
- 8s ceiling. Keep one scene and one main action per clip.
- Multi-subject scenes: best with one character; two is the practical limit.
- Burns garbled subtitles into dialogue clips unless told not to.

## How to prompt

### Formula [official]
`[Cinematography] + [Subject] + [Action] + [Context] + [Style & ambiance]`
Cinematography comes first and is the strongest lever for tone.
`Medium shot, a tired corporate worker, rubbing his temples, in front of a bulky 1980s computer in a cluttered office late at night. Lit by harsh fluorescent overheads and the green glow of the monitor. Retro aesthetic, 1980s colour film, slightly grainy.`

### Camera vocabulary [official]
- Movement: dolly, tracking, crane, aerial, slow pan, POV.
- Composition: wide, close-up, extreme close-up, low angle, two-shot.
- Lens and focus: shallow depth of field, wide-angle, soft focus, macro, deep focus.
- Name the path with start and end: `Crane shot starting low on a lone hiker and ascending high above, revealing the canyon.`

### Audio [official][community]
- **Dialogue:** Google's guide quotes lines (`A woman says, "We have to leave now."`). Community testing finds quotes are the strongest trigger for burned-in captions and uses the colon form plus a flag: `She says: we have to leave now (no subtitles).` Test both once; default to colon form. [community]
- Keep each line speakable in one breath; the clip is 8s. [community]
- **SFX:** `SFX: thunder cracks in the distance.`
- **Ambience:** `Ambient noise: the quiet hum of a starship bridge.`
- Undefined sound gives rushed delivery and mismatched ambience. Always write the soundscape. [community]

### Negatives [official]
Describe the absence positively: "a desolate landscape with no buildings or roads", not "no man-made structures".

### Ingredients (references) [official]
Name each ref by content in the opening clause:
`Using the provided images for the detective, the woman, and the office setting, create a medium shot of the detective behind his desk. He looks up and says in a weary voice: ...`
On Magnific, bind with `@LibraryName`. Max 3 refs. [catalog][tested elsewhere]

### First and last frame [official]
Describe the transition and the camera path between the two images, plus audio:
`The camera performs a smooth 180-degree arc, starting on the front view of the singer and circling to end on the POV shot from behind her.`
Google's workflow: build both keyframes in Nano Banana, then let Veo fill the motion.

### Timestamps inside 8s [official]
```
[00:00-00:02] Medium shot from behind the explorer as she pushes aside a vine.
[00:02-00:04] Reverse shot of her face, awe. SFX: leaves rustle, distant birds.
[00:04-00:06] Tracking shot as she steps into the clearing.
[00:06-00:08] Wide high-angle crane reveal. SFX: gentle orchestral swell.
```

### Consistency without refs [community]
Repeat an identical, specific character description word-for-word across prompts.

## Why it matters for us
One of five models that take a start frame and refs together, with audio. A cheaper-per-shot candidate against Kling 3.0 for UC02-style shots if 8s is enough.

## Open questions
- Which Veo modes (ingredients, first/last, extend) does Magnific expose, and do refs combine with an end frame?
- Quote form vs colon form for subtitle suppression.
- Cost per 8s at 1080p versus Kling 3.0 (run `simulate_cost`).
