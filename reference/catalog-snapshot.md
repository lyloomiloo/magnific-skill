# Magnific catalogue snapshot

Pulled 25 Sep 2026 via `video_models_list` and `images_models_list`. Re-pull at the start of every project. `private` means feature-flagged, not generally available.

## Video (generation)

| Model | Slug | Secs | Max res | Refs | Refs + start frame | Audio |
|---|---|---|---|---|---|---|
| Seedance 2.5 | bytedance-seedance-pro-2.5 | 4-30 | 1080p | img 30, char 30, prod 1, style 1, vid 10, aud 10 | No | Yes |
| Seedance 2.0 | bytedance-seedance-pro-2.0 | 4-15 | 4K | img 9, char 9, prod 1, style 1, vid 3, aud 3 | No | Yes |
| Seedance 2.0 Fast / Mini | fast-2.0 / mini-2.0 | 4-15 | 720p | as 2.0 | No | Yes |
| Kling 3.0 | kling-30 | 3-15 | 4K | char 3, prod 3, img 3 | Required | Yes |
| Kling 3.0 Omni | kling-omni3 | 3-15 | 4K | char 3, prod 3, img, vid 1 | Yes | Yes |
| Kling 3.0 Turbo | kling-30-turbo | 3-15 | 1080p | none | n/a | No |
| Kling 2.6 / 2.5 | kling-26 / kling-25 | 5, 10 | 1080p | none | n/a | 2.6 yes |
| Veo 3.1 | google-veo3_1 | 4, 6, 8 | 4K | img 3 | Yes | Yes |
| Veo 3.1 Fast / Lite | veo3_1-fast / -lite | 4, 6, 8 | 4K / 1080p | none | n/a | Yes |
| Gemini Omni 1.1 | gemini-omni-1_1 | 3-10 | 4K | img 8, vid 3 | Yes | No |
| MiniMax H3 Max | minimax-video-3_0-max | 5-15 | 768p | img 9, char 9, vid 3, aud 3 | No | No |
| MiniMax H3 Max Turbo | minimax-video-3_0-max-turbo | 5-15 | 768p | none | n/a | No |
| Wan 3.0 / Prime (private) | wan-3-0 / -prime | 2-30 | 1080p | img 10, vid 5, aud 5, char 1, prod 1 | No | Yes |
| Wan 2.7 | wan-2-7 | 2-15 | 1080p | img 5, vid 5, char/prod/style 1 | Yes | Yes |
| Grok Imagine 1.5 | grok-imagine-video-1-5 | 1-15 | 1080p | img 7 (not at 1080p) | No | No |
| Happy Horse 1.1 | happy-horse-1-1 | 3-15 | 1080p | img 9 | No | Yes |
| PixVerse 6 | pixverse-6 | 1-15 | 1080p | none | n/a | Yes |
| Runway Gen 4.5 | runway-gen45 | 5, 8, 10 | 720p | none | n/a | No |
| FLUX 3 (private) | bfl-flux-3 | 5-20 | 1080p | none | n/a | Yes |

Talking head / lip sync: OmniHuman 1.5 (to 30s audio), Veed Fabric 1.0 (to 300s), Veed Sync 2.0 (video to video). Motion transfer: Kling 3.0 Motion Control, Kling 2.6 Motion Control, Wan 2.2 Animate.

## Image

| Model | Slug | Res | Refs | Magnific note |
|---|---|---|---|---|
| Seedream 5 Pro | seedream-5-pro | 1.5k, 2k | style, char, prod, img | SOTA 1, default |
| Seedream 5 Flash / Lite | seedream-5-flash / -lite | to 2k / to 4k | all four | |
| Nano Banana Pro | imagen-nano-banana-2 | to 4k | all four | Recommended 3, max fidelity |
| Nano Banana 2 | imagen-nano-banana-2-flash | to 4k | all four | extreme aspects to 8:1 |
| Nano Banana 2 Lite | imagen-nano-banana-2-lite | | all four | Recommended 2, cheap drafts |
| Recraft V4.1 | recraft-v4-1 | | style only | SOTA 1, pure text to image |
| GPT 2 / GPT 2.5 | gpt-2 / gpt-2-mini | to 4k | all four | SOTA 1, text and layout; transparent bg |
| Flux.2 Pro / Max / Flex / Klein | flux-2* | to 2k | all four | |
| Ideogram 4 | ideogram-4 | | style | |
| Luma Uni-1.1 | luma-uni-1 | | all four | |
| Cinematic (Imagen) | cinematic | to 4k | char, prod, img | cinematicControls extra setting |
| Mystic 2.5 | mystic-2-5 | | style, char, prod | Magnific native |
