# Seedream 5 Pro

**Maker:** ByteDance. Pro released 8 Jul 2026. **Magnific slug:** `seedream-5-pro`. Magnific SOTA rank 1, default image model. [catalog]
Siblings: `seedream-5-flash` (1.5k/2k, faster), `seedream-5-lite` (up to 4k), `seedream-4-5` (2k/4k).

## Best at
- Rendering a photographic **treatment**: grain, halation, milky blacks, slow-sync flash. The only model that did on Desigual. [tested]
- Holding face and wardrobe across several references. [tested]
- Staying on the art direction (lighting, angles, flash look) consistently across a six-frame set. [tested, manual review]
- Reference-guided variants and multi-image fusion, up to 10 inputs natively. [platform]
- Dense layouts, posters, infographics and multilingual in-image text (14 languages claimed). [platform]
- Region-precise editing: change one element, leave light, depth and texture elsewhere alone. [platform]

## Weak at
- Proportions, hands and extra limbs. Worst where poses and hand-prop interactions were heavily directed, so over-direction is the likely cause, not only the model. [tested, manual review]
- Long or fine text can garble; ByteDance admits room to improve on fine text and pixel-level edit consistency. [platform]
- Skin can come out over-smoothed versus 4.5. Action can overshoot in dynamic scenes. [community]

## Hard constraints [catalog]
- Resolutions 1.5k, 2k. Aspect 1:1, 4:3, 3:4, 16:9, 9:16, 3:2, 2:3, 21:9.
- Ref types: style, character, product, image.
- Native model: prompt up to 3,000 chars. [platform]

## How to prompt

### Generating and editing are two different prompts [platform]
- **Generate:** describe the whole frame.
- **Edit:** name the target, the change, and a protected list. Nothing else.
- Mixing the two is why a background edit moves the face. Do not re-describe the whole image in an edit unless you want a redesign.

### Generation order [platform]
Format, subject, composition, lighting, in-image text, style. Each clause is read as a directive; a skipped layer falls back to model defaults.
- **Name the format first.** "Editorial magazine cover, 3:4" makes it reserve space and compose like an art director.
- **Place the light, spell out the layout.** One adjective ("beautiful", "premium") is not a brief.

### Length
- Sweet spot: a focused brief of roughly 30 to 80 words. [platform]
- Ceiling: under 600 English words; past that, attention scatters. [platform]
- Our 4,000-character node went past the ceiling and dropped specifics. [tested]

### Realism
- Comes from physical cause, not "8K": name the light source, material response, skin texture (pores, fine lines, restrained shine), sensor noise, depth of field, handheld softness. [platform][community]

### References [platform]
- **One role per reference** (identity, clothing, product, pose, environment, lighting). State priority and say what must not be averaged.
  `Use Image 1 as the exact product reference. Preserve the bottle shape, glass, cap, label and logo position. Use Image 2 only for the soft sunrise lighting.`
- **Style refs get a "not":** `Use the muted palette, soft grain and diffused highlights of Image 2, but do not copy its subject or composition.`
- **Campaigns:** keep one identity block word-for-word across the set; change only the scene-specific part.
- **Packshots beat lifestyle shots** as product refs (white background).
- **Visual markers:** mark up a copy of the image (arrow, circle, rough sketch), upload it beside the original, and point to it: `Follow the red arrow in Image 2: move the product there. Use Image 1 for everything else.` Untested on Magnific.
- On Magnific, bind refs by `@LibraryName`; see `reference/prompting-by-model.md`. [tested]

### Editing [platform]
- Pattern: `Using the [object] from the reference, change only X. Keep the exact silhouette, camera angle, backdrop and lighting.` Without the pin clause, unmentioned elements move.
- Fix table:

| Symptom | Add to the prompt |
|---|---|
| Face changes during an edit | Lock facial structure, expression, apparent age, skin detail |
| Skin looks plastic | Ask for pores, fine lines, restrained shine, natural texture |
| Background also changed | Name the target; list background and composition as protected |
| Product shape drifts | Preserve silhouette, dimensions, label edges, camera angle |
| Still reads CG | Define physical light, material response, depth of field, camera behaviour |
| Text wrong | Shorten copy; state exact wording, language, position, priority |
| References blend | Give each ref one job; say what must not be averaged |

### In-image text [platform]
- Quote it, name the language, give position and size: `English headline reading "NIGHT MARKET" top centre in bold cream letters. Japanese subheading reading "夏の夜市" directly below in smaller red type.`
- Close with `no additional copy, no logos`.

### Exclusions
- Seedream treats the whole prompt as instructions, so concrete exclusions work: "no logo, no watermark, no additional copy". [platform]
- For people and looks, still pair the prohibition with the positive target (universal rule 6). [tested]

### Template
```
[FORMAT + aspect]. [SUBJECT: who/what, bound refs]. [COMPOSITION: framing, placement, negative space].
[LIGHT: source, direction, quality]. [TEXT: "exact words", language, position]. [STYLE / treatment].
Keep [protected list]. No [concrete exclusions].
```

## Observed on our projects
- Three attempts to push grain through Nano Banana prompts came back clean. Seedream rendered it on the first run. [tested]
- ~100 credits per 2k still. [tested]

## Open questions
- Does 5 Flash keep the treatment at lower cost?
- Does the hand problem improve with a crop that makes hands the subject?
- Do marked-up visual-marker refs work through Magnific's ref types?
