# Nano Banana Pro (Gemini 3 Pro Image)

**Maker:** Google DeepMind, Nov 2025. **Magnific slug:** `imagen-nano-banana-2` (confusingly). Nano Banana 2 is `imagen-nano-banana-2-flash`. [catalog]

## Best at
- Local repair: hands, a single prop, one region, without regenerating the frame. [tested]
- Holding a supplied plate while changing one thing (dressing, recasts). [tested]
- Face fidelity, hands, proportions, and more pose variety than Seedream on the same brief. [tested, manual review]
- Bold flat illustration with even outlines (Scoot Next). [tested]
- Text rendering, infographics, translation inside images, search-grounded facts. [official]

## Weak at
- Art direction beyond content: could not hit the target lighting and camera angles, and renders clean with no film or flash treatment regardless of wording. [tested]
- Wardrobe and identity drift across references versus Seedream. [tested]
- Earlier notes called its poses stiff. The final side-by-side review found more pose variety than Seedream. Latest review wins. [tested]

## Hard constraints
- Magnific: 1k, 2k, 4k; ref types style, character, product, image. [catalog]
- Native: up to 14 reference images, 65,536 input tokens (Nano Banana 2: 131,072). Knowledge cutoff Jan 2025. [official]
- **Metadata always reports 1344×768.** Never judge resolution from it. [tested]

## How to prompt

### Core rules [official]
- **Open with a strong verb** naming the operation: Generate, Replace, Add, Remove, Change only.
- **Write narrative.** A tag list ("dog, park, 4k, realistic") underperforms a directed description. [official][community]
- **Positive framing:** "empty street", not "no cars".
- **Camera terms** for control: low angle, aerial view, macro, f/1.8.

### Four official formulas [official]
| Job | Formula |
|---|---|
| Text to image | Subject + Action + Location/context + Composition + Style |
| With references | [Reference images] + [Relationship instruction] + [New scenario] |
| Edit, no new refs | What changes + explicit list of what stays exactly the same (semantic mask) |
| Search-grounded | [Search request] + [Analytical task] + [Visual translation] |

Reference example: `Using the attached sketch as the structure and the attached fabric as the texture, transform this into a 3D armchair render. Place it in a sun-drenched minimalist living room.`

### Directing like a creative director [official]
- **Lighting setup by name:** "three-point softbox", "chiaroscuro, harsh high contrast", "golden hour backlight, long shadows".
- **Camera hardware sets the visual DNA:** GoPro (distorted action), Fujifilm (colour science), disposable camera (raw flash).
- **Film stock and grade:** "1980s colour film, slightly grainy", "muted teal grade".
- **Materiality:** "navy blue tweed", not "suit jacket".

### Text [official]
- Quote the words. Name the font or describe it ("bold white sans-serif").
- Per-line styling works: `top line 'GLOW' in brush script; middle '10% OFF' in heavy Impact; bottom line in thin Century Gothic`.
- Write the prompt in one language and name the target language for the text.
- **Text-first:** settle the copy before asking for the image.

### Edits and identity [tested][community]
- **Say what goes, not only what arrives.** "Dress her in X" adds; it does not remove. Write "Remove every garment she is wearing. Legs bare below the hem." [tested]
- Give each ref a role: "Use image A for the face, image B for the jacket." Start with 2 to 3 refs before going wide. [community]
- Common identity-lock phrasing in public libraries: "Keep the facial features of the person in the uploaded image exactly consistent", followed by an explicit list (bone structure, skin tone, expression). [community]
- Duplicates: public prompts repeat a hard single-object rule ("Render only ONE object. No second object as reflection, shadow or ghost"). [community]
- Magnific runs single-shot calls. Google's "iterate conversationally" advice becomes: restate the keep list on every edit call.

### What public prompt libraries show [community]
Analysed: ZeroLu/awesome-nanobanana-pro, YouMind awesome-nano-banana-pro-prompts.
- Heavy use of **JSON-structured prompts** (subject / photography / background / negative blocks, `preserve_original: true`). No official guidance says JSON beats prose; treat it as an organising format with no proven effect on output.
- Camera spec blocks (body, lens, aperture, ISO, shutter) are common and match Google's hardware advice.
- Many viral prompts lean on celebrity likeness or named IP. Unusable for client work (universal rule 7).

## Conflict to resolve
Google's own examples ask for "pronounced grain" and "1980s colour film, slightly grainy" and show grain in the output. On Magnific our three grain attempts came back clean. Either Magnific's pipeline or our phrasing differs. One cheap test: Google's exact wording, 1k, one frame. Until then, the tested rule stands: treatment goes to Seedream.

## Observed on our projects
- Frame edit costs 0 to 150 credits. [tested]
- An upscale priced XL on a "1344×768" frame returned 11008×6144. [tested]

## Open questions
- Is Nano Banana 2 (Flash) good enough for repair at lower cost?
- Does Google's exact grain phrasing render on Magnific?
