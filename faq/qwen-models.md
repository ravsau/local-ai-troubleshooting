# Qwen Model Issues

## Which Qwen model should I use?

| Model | Size | Best for | Min RAM |
|-------|------|----------|---------|
| qwen3.6 | 24GB | Best overall for agentic coding (April 2026) | 32GB |
| qwen3.5:35b | 24GB | Strong all-rounder with vision + tools | 32GB |
| qwen3.5:9b | 6.6GB | Good balance for 16GB machines | 16GB |
| qwen3.5:4b | 3.4GB | Lightweight, prototyping | 8GB |
| qwen3-coder:30b | 18GB | Coding-specific, older but proven | 32GB |

## Qwen 3.5 vs 3.6 — which one?

Qwen 3.6 (April 2026) is newer and scores 73.4% on SWE-Bench. Use 3.6 if your hardware supports it. Qwen 3.5 has more size variants (0.8B to 122B) so it's better if you're on limited hardware.

## "Model is very slow"

**Cause:** Usually context window too large for available RAM, causing swap.

**Fix:**
1. Reduce context: `export OLLAMA_CONTEXT_LENGTH=32768`
2. Use a smaller quantization (Q4 vs Q8)
3. Verify GPU is active: `ollama ps`
4. On Mac: upgrade to Ollama 0.19+ for MLX acceleration (2x faster)

## Qwen 3.6 specific: thinking takes too long

**Symptom:** Model "thinks" for a very long time before responding, even on simple questions.

**Cause:** Thinking mode is on by default. For simple tasks, the thinking overhead isn't worth it.

**Fix:** You can ask the model to respond without thinking: prefix your prompt with `/no_think` or add to your system prompt: "Respond directly without extended thinking for simple tasks."

**Source:** Community reports, Qwen docs
