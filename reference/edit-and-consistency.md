# Editing and reference consistency

When to stop generating and start editing, which edit tool to use, and how to keep product and model locked across passes.
Tool behaviour is from Magnific's tool specs [catalog]. Most edit tools are **untested on our projects**; tested lessons are tagged.

## 1. Generate again or edit?

| The problem is... | Do this | Why |
|---|---|---|
| **Diffuse:** treatment or light direction wrong across the whole frame, or the cast is the wrong person or outfit everywhere | Regenerate (change model or refs, not wording) | Edits cannot fix what is wrong everywhere [tested] |
| **Local:** one hand, one prop, a stray object, text, **a face or a garment that drifted from its card** | Edit that region | Cheap, keeps the approved rest [tested] |
| **Global but content approved:** mood, light, background, grade | Relight / replace background / post grade | Keeps composition and people |
| **Framing only:** needs another angle or aspect | Crop or expand first; change camera only if new pixels are needed | Crop adds no AI drift |

**Face and wardrobe are a per-frame precision check, so they are local edits.** After every generation, compare the face and each garment against the character card. If one region drifted, segment it and retouch (or Nano Banana "change only the face" / "change only the jacket") with the card wired back in. Do not re-roll the whole frame for a local miss. Regenerate only when the whole cast or outfit is wrong.

**Rule of thumb:** move to edits the moment composition, cast and product read right. Every further generation re-rolls things you already approved.

## 2. The edit ladder (least to most destructive)

Climb only as far as the fix needs. Each rung re-renders more of the frame.

1. **`images_crop` / `images_resize`** (no AI) and **`video_crop`** (no new pixels). Framing fixes. Zero drift.
2. **`images_retouch`** (masked). Only the white area of the mask changes; the rest stays pixel-identical.
3. **Nano Banana prompt edit** (semantic mask, "change only X"). No mask needed; slight global re-render possible. Our tested local-repair route, 0 to 150 credits. [tested]
4. **`images_relight`** / **`images_skin_enhancer`**. Whole-frame light or skin pass on approved content.
5. **`images_replace_background`**. Keeps the subject, swaps the setting, relights the subject to match.
6. **`images_expand`**. Outpaints to a new aspect; the original area is kept.
7. **`images_change_camera`**. New viewpoint around the subject; regenerates the frame.
8. **`images_reimagine`** (`strength`, `keepStructure`) / **`images_restyle`**. New take or new look on the same composition.
9. **Regenerate** from references.

## 3. Tool notes

### Retouch (masked replace or erase)
- Needs a black and white mask the same size as the image (white = change). Make it with **`images_segment`**: describe the thing ("the left hand holding the strap") and it returns the mask. [catalog]
- `replace` needs a prompt describing **only what the masked area becomes**, never the whole frame: "a relaxed closed hand, five fingers, holding the leather strap". `erase` removes the area.
- Mask a little wider than the defect so the fill blends into its edges.
- Model choice: `retouch_models_list` shows which models support replace or erase.
- Spaces have no retouch node; retouch is a direct tool call outside the Space. [tested]
- **Mask or Nano Banana?** Mask when the rest must stay pixel-identical (product, faces nearby). Nano Banana when the region is fuzzy or you cannot segment it cleanly.

### Relight
- Use when content is approved and only the light is wrong (direction, warmth, contrast). One variable per pass.
- Relight **before** grain and grade. Treatment goes on last, in post, identically on every frame. [tested rule 22]
- Video equivalent: `video_relight` (Beeble SwitchLight).

### Change camera (reposition)
- Three sliders: `rotate` 0 to 360 (default 45), `vertical` -30 to 90, `closeup` 0 to 10. [catalog]
- It regenerates the frame, so product and face can drift. **Start small** (rotate 15 to 30) and check details against the packshots after every move.
- Best for coverage variants of an approved hero (a three-quarter, a high angle), not for fixing a bad frame.
- Turning to the back invents what the refs never showed. Describe the back on the card first; back-view drift came from front-only cards. [tested]
- Video equivalent: `video_camera_angle` (can re-shoot only a time window). For framing only, use `video_crop`.

### Reimagine, restyle, replace background, expand
- **Reimagine:** `strength` 0.2 to 0.4 for a light variant, `keepStructure: true` to lock layout; mode `imagen-nano-banana` keeps every element.
- **Restyle:** changes look only; keeps subject and layout. Do not use it to add treatment to a campaign set: post is more consistent.
- **Replace background:** give the new setting its light direction so the subject relight matches.
- **Expand:** for format adaptation (9:16 from 16:9). Check the new area for invented props or text.

### Video edits
- `video_modify` for prompt edits to footage; `video_extend` to continue past the last frame; `video_relight`, `video_camera_angle`, `video_crop` as above.
- Seedance 2.5 native editing grammar (sole master, scope, inherit) is in `seedance-2-5.md`.

## 4. Order of operations

1. Generate and **approve composition, cast, product**.
2. **Local repairs** (retouch or Nano Banana), smallest first.
3. **Global passes** (relight, background, skin) one at a time.
4. **Coverage** (change camera, expand) from the repaired frame.
5. **Re-check product and identity against ground truth** (section 5).
6. **Upscale last:** Magnific Precision, creativity 0. Never upscale a frame you still plan to edit. [tested]
7. **Grade and grain in post,** identical on every frame. [tested]

## 5. Re-uploading references for product and model consistency

### What counts as ground truth [tested]
- **Product:** only the client's own catalogue photography (packshots plus tight detail crops). Never a generated image, even a good one. A generated product ref locks its errors into every frame after it.
- **People (fictional cast):** the approved character card is the identity truth. Generated is fine here because it is the definition.
- **Locations:** generated plates are fine once approved.

### Re-assert on every pass
- Each edit and each video cut is a copy of a copy. **Wire the original packshots and detail crops back in** on every generation that shows the product, alongside the edited frame. [tested]
- State the authority split in the prompt: "The plate is the authority on her face, hair, proportions and the size of the bag. The packshots and detail crops are the authority on the product. Where they disagree, the packshots win." [tested]
- In video, garment drift starts around the third or fourth cut when only a start frame carries the look. Re-anchor there with a new approved frame or refs. [tested]

### Small details that vanish [tested]
- Give the element its own tight detail crop from catalogue pixels.
- Give it a job in the scene (bag held open, turned to camera). Refs alone did not keep charms visible; the action did.
- Anchor scale to the body ("about the length of her forearm"), same wording every frame.

### When to update the library card vs re-upload per call
- **Update the card** when the truth changes or grows: a new view (back, side), a corrected colour, a new detail crop. Descriptions cap at 1,000 characters, so compress the front to add the back. Keep the rules that have failed before verbatim. [tested]
- **Re-upload per call** for one-off authority: a single detail crop for one tight shot.
- `library_edit` can reject silently. Read the card back; if it did not change, create a new card and check `library_list` for duplicates first. [tested]
- Taking a new identity view (e.g. the back) **from an approved frame** is fine for cast and wardrobe styling. Never for product detail. [tested]

### Before every re-wire [tested]
- Text must match the pixels: sides from the wearer's view, colour from a full-res crop.
- Three refs or fewer on a tight shot; count what actually wired.
- Bind by `@LibraryName` at the point the subject appears.

## 6. Symptom to tool

| Symptom | First move |
|---|---|
| Extra finger, bad hand | Segment the hand, retouch replace; or Nano Banana "change only the left hand" |
| Stray object, sign, text | Segment, retouch erase |
| Charm or hardware wrong | Retouch with the detail crop re-wired; if it fails, regenerate with the crop and a job for the prop |
| Face drifted | Local edit: segment the face, retouch replace with the card wired in (or Nano Banana "change only the face"). Regenerate only if the whole cast is wrong. **Untested on faces, log the result.** |
| Garment drifted from the card | Local edit on that garment with the card wired in. Same rule. |
| Light flat or wrong side | Relight |
| Right frame, wrong setting | Replace background |
| Need another angle of an approved hero | Change camera, small rotate, then re-check product |
| Need 9:16 from 16:9 | Crop if content allows, else expand |
| Soft or low-res final | Upscale last, Precision, creativity 0 |

## Open questions (all need credit approval)
- Does `images_change_camera` hold product detail at rotate 15 to 30?
- Does relight preserve Seedream's treatment, or should treatment always wait for post?
- Retouch model comparison for hands on Seedream frames.
