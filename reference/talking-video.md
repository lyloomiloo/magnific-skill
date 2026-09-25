# Talking video: presenter, UGC, multilingual

## What we found [tested]
1. **Audio generated with the video beats audio added after.** Forcing new audio onto an existing clip made lip sync read unnatural.
2. **Post lip-sync is bound by the clip's length.** The script drifted and actions stopped matching the words.
3. **Seedance 2.5 native generation gave the best performance,** with distinct delivery per language (EN, ES, ZH) and the script adapted to each speaker.
4. **Wan 2.6 performance was flat** even with explicit direction.
5. **All 775 Magnific TTS voices are single-language,** so one voice across languages needs dubbing.

## The tradeoff

| Route | Wins | Loses |
|---|---|---|
| Native generation per language (Seedance 2.5, Kling 3.0) | Performance, sync, gestures that fit the words | A different voice in each language |
| Generate once, then `video_dubbing` | One cloned voice across languages | Sync and timing risk, same family as post lip-sync (untested at scale) |
| `video_speak` onto an existing clip | Reuse of an approved visual | Script drift, unnatural sync [tested] |

## Rule of thumb
- Performance or authenticity matters (UGC, presenter): generate natively in each language.
- Voice identity across markets is the brief: dub, and write the source script so each language fits the same duration.
- Either way, write dialogue as performance: quote each line, time-block it, say who stays silent. [platform]
