# Local AI Troubleshooting

Fixes and optimizations for running AI models locally. Ollama, LM Studio, llama.cpp, and the coding agents that connect to them.

Something broken? The fix is probably here. Something slow? That's here too.

## Structure

```
local-ai-troubleshooting/
  bugs/            # Broken behavior + fixes
  optimizations/   # Working setups made faster
  configs/         # Reference Modelfiles, env var presets, settings.json templates
  faq/             # Clustered Q&A mined from YouTube comments + community
```

## Bugs (It's broken)

| Problem | Fix |
|---------|-----|
| [Context window: model forgets everything](bugs/context-window.md) | Set `OLLAMA_CONTEXT_LENGTH` before starting Ollama |
| [Context window: response truncated](bugs/context-window.md#response-truncated-due-to-token-limits) | Bump `max_tokens` in settings to 32768+ |
| [GPU not detected / running on CPU](bugs/gpu-not-detected.md) | Check drivers, verify with `ollama ps` |
| [GPU: model crashes on GPU/CPU split](bugs/gpu-not-detected.md#model-crashes-when-splitting-between-gpu-and-cpu) | Update Ollama to 0.19+ |
| [GPU: MLX not activating on Mac](bugs/gpu-not-detected.md#mlx-not-activating-on-apple-silicon) | Need 32GB+ RAM + Ollama 0.19+ + supported model |
| [Tool calling: prints but doesn't execute](bugs/tool-calling.md) | Update Ollama to 0.19+ (XML pipeline fix) |
| [Tool calling: says executed but no files created](bugs/tool-calling.md#tool-calls-show-as-executed-but-files-arent-created) | Check agent permissions + working directory |
| [Auth: 403 "Access to model denied"](bugs/tool-calling.md#api-error-403-access-to-model-denied) | Use `--auth-type openai`, point to Ollama not cloud |

## Optimizations (It works, make it faster)

| Topic | Guide |
|-------|-------|
| Context window tuning by RAM | Coming soon |
| Ollama MLX on Apple Silicon (2x speed) | Coming soon |
| Keep-alive and batch size tuning | Coming soon |
| Model quantization: Q4 vs Q8 vs NVFP4 | Coming soon |
| Remote Ollama setup (separate machine) | Coming soon |

## Configs (Copy-paste setups)

| Config | For |
|--------|-----|
| Qwen Code + Ollama settings.json | Coming soon |
| OpenCode + Ollama config | Coming soon |
| Ollama Modelfile with custom context | Coming soon |
| systemd service with env vars (Linux) | Coming soon |

## FAQ (Common questions)

| Question | Answer |
|----------|--------|
| [Which Qwen model should I use?](faq/qwen-models.md) | Depends on RAM: 3.6 for 32GB+, 3.5:9b for 16GB |
| [Qwen Code vs OpenCode?](faq/qwen-models.md) | OpenCode has better context compaction |
| [Is local as good as Claude Code?](faq/qwen-models.md#is-this-as-good-as-claude-code) | For routine tasks yes, complex reasoning no |

## How each entry is formatted

```markdown
### [Short description]
**Symptom:** What you see (error message or behavior)
**Cause:** Why it happens
**Fix:**
Step-by-step solution
**Source:** Where this was reported (GitHub issue, YouTube comment, Reddit)
```

## Contributing

Hit a local AI issue and found the fix? Open a PR. Follow the format above.

The "Coming soon" entries are the ones we need most. If you've solved any of them, your PR goes straight in.

## Where these come from

Issues are sourced from:
- YouTube comments on [CloudYeti](https://youtube.com/@CloudYeti) local AI tutorials
- GitHub issues on [ollama/ollama](https://github.com/ollama/ollama), [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)
- Reddit (r/LocalLLaMA, r/ollama, r/ClaudeAI)
- Direct viewer troubleshooting threads

---

Built by [CloudYeti](https://youtube.com/@CloudYeti) — [$0 AI setups every week](https://youtube.com/@CloudYeti)

[1:1 help with your setup](https://cloudyeti.io/meet) | [AI tutorials repo](https://github.com/ravsau/ai-tutorials)
