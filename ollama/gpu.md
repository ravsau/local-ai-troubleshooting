# Ollama GPU Issues

## Model not using GPU (running on CPU)

**Symptom:** Inference is extremely slow. `ollama ps` shows CPU instead of GPU.

**Check:**
```bash
ollama ps
```

**Fix (NVIDIA Linux):**
```bash
# Check if NVIDIA driver is detected
nvidia-smi

# If not found, install
sudo apt install nvidia-driver-535

# Restart Ollama
sudo systemctl restart ollama
```

Ollama needs CUDA 11.8+ and NVIDIA compute capability 5.0+ (GTX 900 series or newer).

**Fix (macOS):** Apple Silicon GPUs work automatically. Check Activity Monitor → GPU tab during inference. If no GPU activity, restart Ollama.

**Fix (AMD):** Need ROCm v7. Linux only. Check Ollama's [GPU docs](https://docs.ollama.com/gpu).

**Source:** [Ollama Troubleshooting](https://docs.ollama.com/troubleshooting)

---

## Model crashes when splitting between GPU and CPU

**Symptom:** Ollama crashes when model is too large for VRAM and splits across GPU + CPU.

**Cause:** Bug in Ollama versions before 0.17.5, specifically with Qwen 3.5 models.

**Fix:** Update Ollama to 0.19+:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Source:** [GitHub Issue #14500](https://github.com/ollama/ollama/issues/14500)

---

## MLX not activating on Apple Silicon

**Symptom:** Running on Mac but not seeing the MLX speed boost.

**Cause:** MLX requires:
1. Ollama 0.19+
2. Apple Silicon (M1 or later)
3. 32GB+ unified memory
4. A supported model (Qwen 3.5/3.6 NVFP4 variants)

**Fix:** Verify version, check RAM, use a supported model tag:
```bash
ollama --version    # Need 0.19+
ollama pull qwen3.5:35b-a3b-coding-nvfp4   # MLX-accelerated tag
```

**Source:** [Ollama MLX Blog](https://ollama.com/blog/mlx)

---

## Debug: Check GPU discovery logs

```bash
OLLAMA_DEBUG=1 ollama serve
```
Look for "discovering available GPUs" in the output. Shows what Ollama sees.

**Source:** [Ollama Troubleshooting](https://docs.ollama.com/troubleshooting)
