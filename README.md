# gen-model-library

A working library for choosing an image or video model and prompting it well, built for Magnific. It comes from real project runs (Desigual, Scoot, Felix) plus each maker's own guides, and it grows as models ship.

It is written as a Claude skill. `SKILL.md` is the entry point and routes to everything else.

## Core rule

Model choice is decided by constraints, not quality. Check what a model accepts together (start frame, references, end frame, audio) before comparing output.

## What is inside

| Path | Purpose |
|---|---|
| `SKILL.md` | Skill entry point: workflow, file router, evidence tags |
| `reference/selection-matrix.md` | Pick a model. Read first. |
| `reference/universal-principles.md` | Rules that held across every model |
| `reference/prompting-by-model.md` | Side-by-side formula, length, ref and dialogue syntax |
| `reference/edit-and-consistency.md` | Regenerate vs edit, the edit ladder, re-wiring product and cast refs |
| `reference/talking-video.md` | Presenter, UGC, lip sync, multilingual |
| `reference/catalog-snapshot.md` | Raw model limits on Magnific, dated |
| `reference/sources.md` | Maker guides and sources to re-check |
| `models/image/` | Seedream 5 Pro, Nano Banana Pro, Recraft V4.1 |
| `models/video/` | Kling 3, Seedance 2.5, Veo 3.1, Wan 2.7, Wan 2.6 |
| `models/_template.md` | Template for adding a new model |

## Evidence tags

Every claim carries a source tag. Weigh them in this order.

- **[tested]** run on a real project. Strongest.
- **[catalog]** Magnific's live model catalogue.
- **[official]** the model maker's own docs.
- **[platform]** a hosting provider's guide.
- **[community]** creator posts. Treat as hypotheses until tested.

## Use it as a Claude skill

Zip the folder contents so `SKILL.md` sits at the top level, then add the zip as a skill in Claude. Claude reads `SKILL.md` first and opens other files only when the task needs them.

## Keeping it current

- Re-pull the Magnific catalogue at the start of each project and update `catalog-snapshot.md`.
- Add a model by copying `models/_template.md`. Fill hard constraints first, prompting second, then add a row to the selection matrix.
- Log test results under `Observed` in the model file. Promote a community claim to a rule only after it is tested.
- Keep Spaces and prompts lean. Add a node or a prompt layer only when a test shows it moves the result.

## Status

v2.2, 25 Sep 2026. Prompting sections rewritten from maker guides, edit and consistency reference added, face and wardrobe checks set as local edits. Several edit tools and models are still untested on our projects. Test queues are listed in the model files and in `edit-and-consistency.md`.
