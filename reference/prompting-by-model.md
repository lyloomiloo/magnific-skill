# Prompting by model: quick comparison

One screen to see how the makers differ. Detail and sources live in each model file.

## The Magnific layer first [tested]
- Magnific wraps these models. It wires refs by type (style, character, product, image, video, audio) and **rewrites `@LibraryName` tokens into the reference description**. That binding is tested on Kling and Seedream.
- Native syntaxes below (`@image1`, `Image 1`, `@Element`) are what the maker trained on. Whether they survive Magnific's rewrite is untested per model. Default to `@LibraryName` at the point of use, then write the role sentence in the maker's style.
- Native features can be blocked on Magnific (Seedance keyframes plus refs). Always check the catalogue first.

## Images

| | Seedream 5 Pro | Nano Banana Pro | Recraft V4.1 |
|---|---|---|---|
| Opening move | Name the format ("Editorial cover, 3:4") | A strong verb (Generate, Replace, Change only) | Name the medium ("A watercolour illustration of") |
| Order | Format, subject, composition, light, text, style | Subject, action, context, composition, style | Subject, environment, framing, details, light, camera, mood |
| Length | 30 to 80 words ideal, 600 max | Narrative, as long as it stays specific | Under ~15 words to explore, structured to control |
| Refs | One role each, say what not to average | [Refs] + relationship + new scenario | Style ref only |
| Edits | Target + change + protected list; never re-describe | Semantic mask: what changes + what stays exactly | n/a |
| Text | Quote, name language, position, priority | Quote, name font, per-line styling | Quote, or it reads as scene |
| Negatives | Concrete exclusions work ("no watermark") | Positive framing ("empty street") | Hard constraints for flat graphics ("no gradients") |
| Treatment (grain, flash) | Renders it [tested] | Clean on Magnific [tested]; Google says it works [official] | n/a |

## Video

| | Kling 3.0 / Omni | Seedance 2.5 | Veo 3.1 | Wan 2.7 |
|---|---|---|---|---|
| Formula | Camera, subject, sequential action, endpoint | Subject + action required; scene, style, camera, sound optional | Cinematography + subject + action + context + style | Entity + scene + motion + aesthetic control + stylisation |
| First words | Camera language | The event | Shot and camera | Entity, then camera and light |
| Length | 100 to 200; longer only with second markers | Stages with end states; budget per block | 8s: one scene, one action | Cover all five dimensions; short actions |
| Timing syntax | `Shot 1 (3s):` / "At the 4th second" | Stages, or `0-5s` blocks, continuous | `[00:00-00:02]` | `Shot 1 [0-3 s]` + "Hard cut" |
| Ref syntax (native) | `@ElementName`, `@Image` | `<NAME> corresponds to @image1; take X only` | "Using the provided images for X, Y, Z" | `Image 1`, `Video 1` (separate numbering) |
| Dialogue | `Name (delivery, language): line` | `{line}` after "Dialogue language: ..." | `says: line (no subtitles)` [community] | `[Label, voice]: "line"` after an action anchor |
| Music / SFX | Describe in prose | `( )` music, `< >` SFX | `SFX:` / `Ambient noise:` prefixes | Voice / SFX / BGM formulas |
| Suppress | "one continuous take without any cuts" | "No background music", "No subtitles" | "(no subtitles)" | "No dialogue.", "No background music.", "Generate single shot." |
| Fills gaps with | Improvised camera | Waiting or slow motion on thin blocks | Subtitles, rushed audio | Invented dialogue and music |

## Where the makers agree
1. Direct, do not describe. Camera and action beats beat adjectives.
2. One main action per shot or stage, with a visible end state.
3. Each reference gets one job and a "do not take".
4. Name what must stay fixed.
5. Translate emotions and niche camera terms into visible change.

## Where they disagree
- **Length:** Recraft rewards 2 words; Kling's own demos run 300. Match the model's appetite.
- **Negatives:** Google says frame positively. ByteDance says explicit prohibition is right for asset roles, edit scope and bleed-ins. Both hold: positive for picture content, explicit for asset roles and sound categories.
- **Dialogue quotes:** Google uses them; Veo's community says they trigger captions; Seedance uses `{ }`; Kling uses speaker labels.
