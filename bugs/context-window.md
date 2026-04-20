# Ollama Context Window Issues

## Model "forgets" everything / loses context mid-conversation

**Symptom:** Model asks "what are you talking about?" or repeats itself. Seems to forget what you just said.

**Cause:** Ollama defaults to 4,096 tokens context. System prompts from coding agents eat most of that, leaving almost nothing for your conversation.

**Fix:**
```bash
# Set before starting Ollama
export OLLAMA_CONTEXT_LENGTH=65536

# Linux systemd
sudo systemctl set-environment OLLAMA_CONTEXT_LENGTH=65536
sudo systemctl restart ollama

# macOS desktop app
launchctl setenv OLLAMA_CONTEXT_LENGTH 65536
# Quit and reopen Ollama app
```

**Recommended values by RAM:**
| RAM | Context Length |
|-----|--------------|
| 16GB | 16384-32768 |
| 32GB | 65536 |
| 64GB | 131072 |
| 128GB | 196608-262144 |

**Source:** [Ollama FAQ](https://docs.ollama.com/faq), multiple YouTube comment threads

---

## "Response truncated due to token limits"

**Symptom:** Model stops generating mid-file. Followed by `API Error: 400 invalid message content type: nil`.

**Cause:** `max_tokens` in your settings caps output per response. Default 8192 is too low for large outputs (HTML files, long code).

**Fix:** In your agent's settings, bump `max_tokens` to 32768 or higher:
```json
"samplingParams": {
  "max_tokens": 32768
}
```

**Source:** [GitHub Issue #1924](https://github.com/QwenLM/qwen-code/issues/1924), CloudYeti video comments

---

## Context window setting not taking effect

**Symptom:** You set `OLLAMA_CONTEXT_LENGTH` but model still truncates.

**Cause:** The env var must be set before Ollama starts. If using the desktop app, `export` in terminal doesn't affect it.

**Fix:**
1. Kill Ollama completely
2. Set the env var
3. Start Ollama fresh

Verify with: `ollama run qwen3.6 --verbose` — check the reported context length in the startup logs.

**Source:** [GitHub Issue #6286](https://github.com/ollama/ollama/issues/6286)
