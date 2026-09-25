# Recraft V4.1

**Maker:** Recraft, May 2026. **Magnific slug:** `recraft-v4-1`, variants `standard` / `utility`, tiers `mid` / `pro`. Magnific SOTA rank 1 for pure text to image. [catalog]
Also: `recraft-v4`, `recraft-v4-pro`; vector output via `images_generate_svg` (V4 Pro Vector).

## Best at
- First drafts with no references, creative exploration, fast iteration. [catalog]
- Short prompts: fills in framing, light and grade well from a few words. [official][platform]
- Precise control from long structured prompts when needed. [official]
- Flat graphic logic: logos, icon systems, posters with typographic hierarchy, smooth gradients, 3D renders. [official]

## Weak at
- **Style reference only.** No character or product refs, so no locked faces or products. [catalog][tested]
- Thin hairline illustration look was dropped for Scoot in favour of Nano Banana Pro's bold outlines. [tested]

## Variants [platform]
- **Standard** brings its own point of view: experiments with angle, light, composition.
- **Utility** does the opposite: flat light, front-facing, simple scenes. Use for mockups, product shots, icon sets, design-system assets where predictability beats surprise.

## How to prompt

### Two modes [official][platform]
- **Interpretive (under ~15 words):** the model decides placement, light, grade. Use for exploration, mood discovery, pitch references. "golden hour portrait" is a complete prompt.
- **Structured:** when composition must be exact. Structure makes results repeatable. It does not raise quality on its own. If exploring, keep it minimal.

### Structured layer order, most to least important [platform]
1. Subject and scene
2. Environment
3. Framing and pose
4. Physical details (identity, clothing, materials)
5. Lighting (direction, quality, colour temperature)
6. Camera (angle, lens, depth of field)
7. Mood
Use only the layers the image needs. A product shot may need three.

### By format [official][platform]
- **Photoreal:** brief it like a photographer: lens ("85mm f/1.8"), light setup, environment.
- **Illustration:** state medium early ("A watercolour illustration of..."), line behaviour, colour logic.
- **3D:** material and light as in a render engine ("matte vinyl, three-direction soft studio light, light grey seamless").
- **Posters:** describe typographic hierarchy and layout mechanics; it builds the layout rather than scattering elements. For photo plus graphic hybrids, define each visual language separately, then how they interact.
- **Logos and icon sets:** shape logic, colour system, hard constraints ("flat colours only, no gradients, shadows or texture"). Repeat shared traits across a set explicitly ("identical tiny dot eyes, same size and placement").

### Text [platform]
- Quote every literal word. Unquoted words are read as scene description.

### Style consistency
- Lean on the style reference, not repeated style prose. [platform]
- Native API locks palette and background colour via parameters (`colors`, `backgroundColor`). Not seen in Magnific's catalogue. [platform]

## Open questions
- Does V4 Styles (style ID from 1 to 10 refs) exist on Magnific? Not in the catalogue as of 25 Sep 2026.
- Does Magnific expose the palette parameters?
