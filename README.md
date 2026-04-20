# Local AI Troubleshooting

A community-maintained collection of fixes for common issues when running AI models locally. Ollama, LM Studio, llama.cpp, and the coding agents that connect to them.

If you've hit a wall setting up local AI, the answer is probably here.

## Quick Links

| Problem | Go to |
|---------|-------|
| Ollama issues | [ollama/](ollama/) |
| Qwen model issues | [models/qwen.md](models/qwen.md) |
| Coding agent issues (Qwen Code, OpenCode, Claude Code + Ollama) | [agents/](agents/) |
| GPU not detected | [ollama/gpu.md](ollama/gpu.md) |
| Context window problems | [ollama/context.md](ollama/context.md) |
| Tool calling broken | [agents/tool-calling.md](agents/tool-calling.md) |

## How This Repo Works

Each issue has:
- **Symptom** — what you see (the error message or behavior)
- **Cause** — why it happens
- **Fix** — step-by-step solution
- **Source** — where this was reported (GitHub issue, YouTube comment, Reddit)

## Contributing

Hit a local AI issue and found the fix? Open a PR. Format:

```markdown
### [Short description of the issue]
**Symptom:** [What you see]
**Cause:** [Why it happens]
**Fix:**
[Step-by-step solution]
**Source:** [Link to where this was reported]
```

## Topics Covered

- **Ollama:** Installation, GPU detection, context window, memory, speed, MLX
- **Models:** Qwen 3.5/3.6, Gemma 4, Llama, DeepSeek, Mistral — model-specific quirks
- **Coding Agents:** Qwen Code, OpenCode, Claude Code + Ollama, Cline, Continue.dev
- **Hardware:** Apple Silicon, NVIDIA, AMD, CPU-only, remote Ollama setups

---

Built by [CloudYeti](https://youtube.com/@CloudYeti) — [$0 AI setups every week](https://youtube.com/@CloudYeti)

Found this useful? [Star the repo](https://github.com/ravsau/local-ai-troubleshooting) so others can find it.
