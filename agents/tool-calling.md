# Tool Calling Issues (Coding Agents + Ollama)

## Model prints tool calls but doesn't execute them

**Symptom:** Agent shows XML/JSON like `</tool_call: write_file>` in the output but no file is created. Nothing happens.

**Cause:** Ollama versions before 0.17.5 routed Qwen's XML-based tool calling through the wrong pipeline (JSON-based). The system prompt, format instructions, and output parser were all incorrect.

**Fix:** Update Ollama:
```bash
# Linux
curl -fsSL https://ollama.com/install.sh | sh

# macOS
brew upgrade ollama
```
Need version 0.17.7+ for full tool calling support. 0.19+ recommended.

**Affected models:** Qwen 3.5, Qwen 3.6, Qwen3-Coder

**Source:** [GitHub Issue #14493](https://github.com/ollama/ollama/issues/14493), [GitHub Issue #14745](https://github.com/ollama/ollama/issues/14745)

---

## Tool calls show as executed but files aren't created

**Symptom:** Agent says "file created successfully" but nothing appears on disk.

**Cause:** Multiple possible causes:
1. Agent is running in read-only or sandbox mode
2. Working directory mismatch
3. Ollama version bug (pre-0.17.5)

**Fix:**
1. Check your agent's permission settings (Qwen Code: say "always allow" when prompted)
2. Check which directory you launched the agent from
3. Update Ollama to latest

**Source:** [GitHub Issue #7030](https://github.com/anomalyco/opencode/issues/7030)

---

## Tool calling works but is inconsistent

**Symptom:** Works 70-80% of the time, randomly fails on some calls.

**Cause:** Local models are less consistent at tool calling than frontier cloud models. Known limitation. Smaller models are worse.

**Fix:**
- Use the largest model your hardware supports
- Budget for re-prompts ("try again" or rephrase)
- Use Qwen 3.6 over older versions (better tool calling)
- Set temperature to 0.7 (not too creative, not too rigid)

**Source:** Community consensus across multiple YouTube comment sections

---

## "API Error: 403 Access to model denied"

**Symptom:** Qwen Code shows 403 error when trying to use the model.

**Cause:** You're hitting Qwen's cloud API, not local Ollama. Qwen's free OAuth tier was discontinued April 15, 2026.

**Fix:** Launch with the local flag:
```bash
qwen --auth-type openai --model qwen3.6
```
Ensure `~/.qwen/settings.json` has `baseUrl: "http://localhost:11434/v1"`.

**Source:** CloudYeti video comments, Qwen Code docs
