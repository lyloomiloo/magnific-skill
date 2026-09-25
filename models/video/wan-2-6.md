# Wan 2.6

**Maker:** Alibaba. **Magnific slug:** `wan-2-6`. No Magnific recommendation. [catalog]
Newer on Magnific: `wan-2-7` (refs + keyframes together), `wan-3-0` (private, to 30s).

## Hard constraints [catalog]
- 5, 10, 15s. 720p, 1080p. Prompt 1,500 chars. Multishot up to 5.
- On Magnific: start frame plus **one audio reference only**. No image, character or video refs.

## Verdict
**Not for identity-critical work on Magnific.**

## Weak at
- Changed the character's appearance despite a start frame. [tested]
- Flat performance despite explicit performance direction and script notes. [tested]
- Audio can come out harsh in the treble; EQ in post. [community]

## Why the gap
Wan 2.6's marketed identity lock comes from its reference-to-video mode (1 to 3 reference videos, `@Video1` syntax). [platform] Magnific exposes only start frame plus audio, so that lock is unavailable here. Image-to-video from a single frame is where Wan loses identity as the face turns or changes expression. [community]

## If you must use it
- Clean, well-lit start frame with a clear subject; avoid small text and busy hands. [community]
- Keep the prompt on motion and camera. [community]
- Consider Wan 2.7 instead, which accepts character refs with a start frame. [catalog] Untested. Prompting guidance for the whole Wan family lives in `wan-2-7.md`.
