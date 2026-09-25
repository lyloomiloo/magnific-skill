# Sources (prompting research, 25 Sep 2026)

Re-check these when a model updates.

## Official
- Google Cloud, Ultimate prompting guide for Nano Banana (Mar 2026): cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-nano-banana
- Google, 7 tips for Nano Banana Pro: blog.google/products-and-platforms/products/gemini/prompting-tips-nano-banana-pro/
- Google Cloud, Ultimate prompting guide for Veo 3.1 (Oct 2025): cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-veo-3-1
- Kling VIDEO 3.0 user guide: kling.ai/quickstart/klingai-video-3-model-user-guide
- Kling VIDEO 3.0 Omni user guide: kling.ai/quickstart/klingai-video-3-omni-model-user-guide
- Kling Omni API docs (element naming): kling.ai/document-api/api/video/3-0-omni/video-omni
- ByteDance Seedance 2.5 prompt guide (BytePlus ModelArk, JS-rendered): docs.byteplus.com/en/docs/ModelArk/2607689. Read via the English walkthrough: dev.to/super_lewis/the-seedance-25-prompting-guide-in-english-4hen
- Alibaba Model Studio, Wan text/image-to-video prompt guide (Sep 2026): alibabacloud.com/help/en/model-studio/text-to-video-prompt
- Recraft, Prompting with V4: recraft.ai/docs/prompt-engineering-guide/prompting-with-recraft-v4

## Platform
- Runware, Recraft V4.1 prompting: runware.ai/docs/models/recraft-v4-1/guides/prompting
- Runware, Seedream 5.0 Pro prompting: runware.ai/docs/models/bytedance-seedream-5-0-pro/guides/prompting
- OpenArt, JXP, GPT Proto, XMK Seedream 5 Pro guides (length, visual markers, edit fix table, ref roles)

## Community libraries analysed
- ZeroLu/awesome-nanobanana-pro (GitHub). Patterns: JSON prompts, identity-lock phrasing, camera spec blocks, single-object rules.
- YouMind-OpenLab/awesome-nano-banana-pro-prompts (GitHub, 10k+ prompts).
- Veo community guides on subtitle suppression (colon syntax, "(no subtitles)").
- maciejdzierzek/kling-ai-prompt-generator (audited clean earlier): motion endpoints, camera vocabulary.

## Checked 25 Sep 2026 against Lyla's two intuitions
- Anthropic, Building effective agents: anthropic.com/engineering/building-effective-agents. "Simplest solution possible, only increasing complexity when it demonstrably improves outcomes." Layers of abstraction obscure prompts and tempt extra complexity. [official, general LLM guidance, not image-specific]
- UD, Nano Banana consistent characters: ud.hk/en/blogs/insight/article/2026-06-29-nano-banana-consistent-characters. Use incremental targeted edits over full regeneration; name signature clothing items or they get dropped; long face descriptions fight the reference and blend into a stranger. [community]
- Jenova, regeneration vs reference sheets: jenova.ai/en/resources/which-method-keeps-ai-characters-consistent. Each regeneration is an independent draw, so drift compounds; a fixed reference anchors it. Says nothing on inpainting. [community]
- Atlas Cloud, Seedream 5 Pro guide: atlascloud.ai/blog/tips/seedream-5-pro-prompt-guide. Long prompts are fine if organised; one change per rerun. Does not support "shorter is better". [platform]
