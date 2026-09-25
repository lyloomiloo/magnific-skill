# Universal principles

Rules that held across every model we used. Model files override these only where they say so.

## Selecting

1. **Constraints before quality.** Check what the model accepts together (start frame, refs, end frame, audio) before comparing output.
2. **Treatment is a model capability.** If a model renders clean, no adjective makes it render grain. Swap the model, not the wording. [tested]
3. **Split diffuse from local.** Generate where identity and treatment hold. Repair single-region defects elsewhere. [tested]

## Prompting

4. **Direct, do not describe.** For video, write camera, action beats and end state like a shot note. For stills, layer format, subject, composition, lighting, text, style. [official, all makers]
5. **Keep it short and layered.** Upstream text nodes concatenate into one prompt. Our frame hit 14,000 characters and the model dropped specifics. Direction layer once, product layer by reference, one line per shot. [tested] Seedream's own ceiling is under 600 words. [platform]
6. **Pair every prohibition with the positive target.** "No makeup" produced tired faces. Write "light natural makeup, visible pores, no airbrushing." Google's guidance agrees: describe what you want. [tested][official]
7. **Describe the look, never cite the work.** Naming a film, director, artist or track got Seedance and music generations refused. It is also the copyright position for client work. [tested]
8. **Plain physical language, not craft vocabulary.** Posing rules pasted into a prompt produce diagram poses. Rules are tests you check against, not text. [tested]
9. **Underwrite scene briefs.** Location, one ordinary action, framing, colour bias. Over-choreography reads as staged. [tested]
10. **Name what is actually there.** "Lantern" fetched a Western hurricane lamp in a Japanese arcade. Use the regional noun. [tested]
11. **English prompts.** Keep dialogue in the target language inside quotes. [platform]

24. **Over-directed hands and interactions break anatomy on every model.** Seedream grew extra limbs on choreographed poses, Kling failed a step-by-step charm clip, Seedance 2.0 added a third hand. Name one contact and the end state ("the charm now hangs from the strap ring, her palm empty"), not each finger move. Pair with an end frame where the model allows it. [tested]
25. **Generate audio with the picture.** Audio forced on afterwards drifts and reads false. [tested]

## References

12. **One job per reference, and say what not to copy.** "@Image1 controls only the product. Do not copy its background." [platform][tested]
13. **Pin what must not change, by name.** Unmentioned elements drift. [platform]
14. **Address refs by content or bound token, not position.** "The tan leather journal" or `@DSG_Sheet_Emma_LookA`, not "the first image". [platform][tested]
15. **Wire only what is in frame, three or fewer on a tight shot.** Five refs broke a face. Two fixed it. [tested]
16. **Ground truth is the client's own pixels.** Never feed a generated image back as product truth. [tested]
17. **Text must match the reference pixels.** Check side from the wearer's view and colour from a full-res crop. [tested]
18. **Check per-type limits and count after wiring.** A Space generator silently drops refs past ten while reporting success. [tested]

## Iterating

19. **Change one variable.** Three prompt rewrites moved nothing. One model swap moved everything. [tested]
20. **A fix that does not move the outcome is evidence about the lever.** Stop pulling it. [tested]
21. **Cheap tier first.** 480p or Draft video, 1.5K stills, singular node runs. Ask before spending credits.
22. **Post beats prompt for cross-shot consistency.** Grade, grain, glow in ffmpeg, identical on every shot. [tested]
23. **Verify silent failures by reading back.** Metadata, ref counts, placeholder identifiers. [tested]

## Added 25 Sep 2026 from maker guides

26. **Each maker publishes a formula. Use theirs.** They converge (event first, camera explicit, style last) but order and length differ. See `prompting-by-model.md`. [official]
27. **Negatives, refined.** Picture content: describe the positive target (rule 6). Asset roles, edit scope, bleed-ins and sound categories: explicit prohibition is correct ("Do not take the background", "No background music"). [official]
28. **Suppress what the model fills in.** Wan invents dialogue and music when unwritten; Veo burns in subtitles; Kling improvises the camera; Seedance pads thin time blocks with waiting. Write the absence. [official][community]
29. **Dialogue syntax is model-specific.** Speaker labels (Kling), `{ }` braces (Seedance), colon plus "(no subtitles)" (Veo), action-anchored labels (Wan). Wrong syntax risks merged speakers or burned captions. [official][community]
30. **End states over durations.** Every maker's long-take advice is the same: one change per block, and the state visible when it ends. Time blocks are budgets and never frame-exact cuts. [official]
31. **Separate view images beat packed grids** when the model reads raw images (Seedance native). Library cards on Magnific built from one turnaround sheet still worked. [official][tested]
32. **Magnific sits between you and the model.** Native syntax and features may be rewritten or blocked. Bind with `@LibraryName`, check the catalogue for prohibited combinations, and treat native-only tricks as untested here. [tested]

## Added 25 Sep 2026 from Lyla's review

33. **Face and wardrobe checks are local edits.** They are a precision check on every frame, so the repair is a targeted edit of that region, not a regeneration. Regenerate only when the identity or wardrobe is wrong across the whole frame. Community guides agree (targeted edits keep identity; each regeneration is a fresh draw and drift compounds). Not yet [tested] on faces here. [Lyla][community]
34. **Do not over-engineer Spaces or prompts.** Extra nodes and extra prompt layers can confuse the model and burn tokens and credits for nothing. Start with the fewest nodes and the shortest prompt that could work, and add one only when a test shows it moves the result. Build nothing speculatively. Length is not the issue, disorganised stacking is: a long organised prompt is fine (Seedream guides), but concatenated layers and long face descriptions that compete with the reference are not. [Lyla][official][community]
