---
name: gen-model-library
description: Model selection and prompting library for image and video generation, built for Magnific. Use whenever choosing a model, writing or reviewing a generation prompt, wiring references or keyframes, planning a shot, or debugging a bad output on Seedream, Nano Banana, Recraft, Kling, Seedance, Veo, Wan, MiniMax or any other image/video model. Also use when a new model is released and needs adding.
---

# Generative model library

A working library for picking the right image or video model and prompting it well. Built from real project runs (Desigual, Scoot, Felix) plus official and platform guidance. Grows as models ship.

## Core rule

**Model choice is decided by constraints, not by quality.** Read the constraint matrix before any benchmark. The deciding factor is usually a hard property one model has and others lack: what it accepts alongside a start frame, whether it renders a treatment, how long it runs, what it refuses.

**Keep it lean.** Do not over-engineer Spaces nodes or prompts. More nodes and longer prompts can confuse the model and cost tokens for nothing. Add a layer only after a test shows it moves the result (principle 34).

## Workflow

1. **Define the job.** Still or motion? Starts from an approved frame? Needs identity or product locked? Length? Treatment (grain, flash, flat illustration)? Audio?
2. **Filter by hard constraints.** `reference/selection-matrix.md`. Eliminate models that cannot do the job at all.
3. **Choose among survivors by tradeoff.** Same file, tradeoff tables.
4. **Read the model file.** `models/image/*` or `models/video/*`. Prompt in that model's shape: its formula, its length, its ref and dialogue syntax. On Magnific, bind refs with `@LibraryName`.
5. **Apply universal rules.** `reference/universal-principles.md`.
6. **Test cheap, then commit.** Lowest resolution tier, one frame or one shot, one variable changed at a time. Ask before spending credits.
7. **Switch to edits once composition, cast and product are approved.** `reference/edit-and-consistency.md`. Face and wardrobe checks are local edits on every frame. Re-wire ground-truth refs on every pass.
8. **Log what you learn** back into the model file under `Observed`.

## Files

| File | Read when |
|---|---|
| `reference/selection-matrix.md` | Choosing a model. Always first. |
| `reference/universal-principles.md` | Writing any prompt. |
| `reference/edit-and-consistency.md` | Deciding regenerate vs edit, choosing retouch / relight / change camera / expand, order of passes, re-wiring product and cast refs. |
| `reference/prompting-by-model.md` | Side-by-side: formula, length, ref and dialogue syntax per model. Read before switching models. |
| `reference/catalog-snapshot.md` | Checking a model's raw limits on Magnific. |
| `models/image/seedream-5-pro.md` | Campaign stills, treatment, multi-reference fusion. |
| `models/image/nano-banana-pro.md` | Local repair, plate dressing, text, infographics. |
| `models/image/recraft-v4-1.md` | Illustration, vector-ish, no-reference first drafts. |
| `models/video/kling-3.md` | Video from an approved start frame. Kling 3.0, Omni, Turbo. |
| `models/video/seedance-2-5.md` | Long takes, heavy references, native audio, performance. |
| `models/video/veo-3-1.md` | 8s shots with start frame + refs and strong native audio. Untested. |
| `models/video/wan-2-7.md` | Wan family prompting; start frame + refs. Untested. |
| `models/video/wan-2-6.md` | Only if forced to use Wan 2.6; explains why it drifts here. |
| `reference/talking-video.md` | Presenter, UGC, lip sync, multilingual. |
| `models/_template.md` | Adding a new model. |
| `reference/sources.md` | Re-checking maker guides after an update. |

## Evidence tags

Every claim in a model file carries a source tag. Weigh them in this order.

- **[tested]** we ran it on a real project. Strongest.
- **[catalog]** Magnific's live model catalogue. Authoritative for limits on this platform.
- **[official]** the model maker's own docs or blog.
- **[platform]** a hosting provider's guide (fal, Runware, BytePlus). Usually reliable.
- **[community]** creator posts. Treat as hypotheses to test.

## Keeping it current

- Re-pull the catalogue (`video_models_list`, `images_models_list`) at the start of any new project. Slugs, limits and recommendations change. Update `catalog-snapshot.md` and the date.
- New model: copy `models/_template.md`, fill hard constraints from the catalogue first, prompting from official docs second, then add a row to the selection matrix.
- Never promote a [community] claim to a rule until it is [tested].
