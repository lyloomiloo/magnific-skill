# Selection matrix

Snapshot: Magnific catalogue, 25 Sep 2026. Re-pull before relying on limits.

## Video: the first question

**Does the shot start from a fixed, approved frame, and does it also need references?**

This one question eliminated the platform's top-ranked model on Desigual UC02. Most models take references OR keyframes, never both.

| Model | Start frame + references together? | Notes |
|---|---|---|
| Kling 3.0 `kling-30` | **Yes, and required.** Refs only work with a start frame | char 3, product 3, image 3 [catalog][tested] |
| Kling 3.0 Omni `kling-omni3` | **Yes, refs optional.** Image refs cannot combine with an end frame | char 3, product 3, image, video 1 [catalog] untested |
| Veo 3.1 `google-veo3_1` | Yes | image refs 3, 4/6/8s only, 16:9 or 9:16 only [catalog]. See `veo-3-1.md` |
| Wan 2.7 `wan-2-7` | Yes | image 5, video 5, char/product/style 1 each [catalog]. See `wan-2-7.md` |
| Gemini Omni 1.1 `gemini-omni-1_1` | Yes | image 8, video 3, 3 to 10s, beta [catalog] |
| Seedance 2.0 / 2.5 | **No on Magnific.** Every visual ref type is prohibited with keyframes | [catalog][tested]. Natively, 2.5 accepts first/last frame declared in the prompt alongside refs [official]. Untested whether that works through Magnific |
| MiniMax H3 / H3 Max | No | [catalog] |
| Grok Imagine 1.5 | No, and no refs at 1080p | [catalog] |
| Happy Horse 1 / 1.1 | No | [catalog] |
| Wan 3.0 / Prime | No (style, colour, effect still allowed). Private flag | [catalog] |

## Video: by job

| Job | First choice | Why | Alternative |
|---|---|---|---|
| Shot from approved frame, identity must hold | Kling 3.0 | Only tested model taking refs with a start frame | Kling Omni (untested, more flexible) |
| One continuous take over 15s | Seedance 2.5 | Only GA model to 30s in one pass | Wan 3.0 (30s, private) |
| No start frame, many refs (cast, product, style) | Seedance 2.5 | Up to 30 image, 30 character, 10 video, 10 audio refs | MiniMax H3 Max for cheap drafts |
| Cheap motion or staging drafts | Seedance 2.5 at 480p or Draft | Same model as final, so drafts predict finals | MiniMax H3 Max Turbo, Kling 2.5 |
| Presenter or UGC performance to camera | Seedance 2.5 | Best performance; native multilingual delivery [tested] | Kling 3.0 if a start frame is mandatory |
| Talking head from a still + audio | OmniHuman 1.5 or Veed Fabric | Purpose built; Fabric runs to 300s | `video_speak` catalogue |
| Same speaker, several languages | See `reference/talking-video.md` | Native per language wins on performance; dubbing wins on one voice [tested] | |
| Motion copied from a reference clip | Kling 3.0 Motion Control | Up to 15s, multishot. 2.6 version copied motion and script too rigidly and took no product refs [tested] | Wan 2.2 Animate |
| Dialogue with native lip sync | Seedance 2.5 or Kling 3.0 | Both native audio | Veo 3.1 |

## Video: cost [tested, Magnific credits]

| Setup | Credits |
|---|---|
| Kling 3.0, 5s, 1080p | 450 |
| Seedance 2.5, 5s, 1080p | 3,950 |
| Seedance 2.5, 30s, 1080p / 720p / 480p | 23,700 / 13,200 / 6,000 |

Test at 480p before committing 1080p. Run `simulate_cost` first, every time.

## Image: by job

| Job | First choice | Why | Avoid |
|---|---|---|---|
| Campaign stills with film, grain or flash treatment | Seedream 5 Pro | Only tested model that renders the treatment [tested] | Nano Banana Pro renders clean whatever you write |
| Holding wardrobe and identity across refs | Seedream 5 Pro | Held fidelity where Nano Banana drifted [tested] | |
| Fix one local defect (hands, a prop) | Nano Banana Pro | Local edits without regenerating; better anatomy [tested] | Regenerating the whole frame |
| Dress a plate, swap one thing, keep the rest | Nano Banana Pro | Holds a supplied plate [tested] | |
| Bold flat illustration with outlines | Nano Banana Pro | Scoot Next style [tested] | |
| Readable text, infographics, UI, diagrams | GPT 2 / GPT 2.5 | Magnific SOTA for layout [catalog] | Seedream on long text (garbles) [community] |
| First drafts with no references | Recraft V4.1 | Magnific SOTA for pure text to image [catalog] | Recraft when you need character refs (style only) |
| Cheap high-volume iteration | Nano Banana 2 Lite | Fast, cheap [catalog] | |
| Upscale without reinventing detail | Magnific Precision, creativity 0 | [tested] | Any creativity above 0 |

## Image: tradeoffs side by side [tested, Desigual UC01]

Same prompts, refs, aspect and resolution. Only the model changed.

| | Seedream 5 Pro | Nano Banana Pro |
|---|---|---|
| Grain, halation, lifted blacks, flash | Full signature | Absent |
| Face and wardrobe across refs | Holds | Drifts |
| Lighting and angles to brief | Holds | Misses |
| Hands, proportions, limbs | Poor, extra limbs | Better |
| Pose variety | Narrower | Wider |
| Character | 1990s newsprint | Clean digital |

**Split rule:** generate on the model that holds the *diffuse* property (treatment, identity). Repair the *local* defect (a hand) on the other.

## Slug traps on Magnific

- `imagen-nano-banana-2` is **Nano Banana Pro**. `imagen-nano-banana-2-flash` is **Nano Banana 2**.
- `bytedance-seedance-pro-2.5` is Seedance 2.5. `pro-2.0` is the older model.
- `kling-omni3` is 3.0 Omni. `kling-omni1` is the older O1.
