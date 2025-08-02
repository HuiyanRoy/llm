
# Granite 4.0 Tiny + llama.cpp on MacBook: Quickstart Guide

IBM's Granite 4.0 Tiny(Preview) version features a **hybrid MoE (Mixture of Experts)** architecture, offering exceptional memory efficiency — **up to 72% less memory** usage compared to Granite 3.3!
Read more in IBM's official [page](https://www.ibm.com/new/announcements/ibm-granite-4-0-tiny-preview-sneak-peek).

## Getting Started with `llama.cpp`

You can easily run the model locally using [`llama.cpp`](https://github.com/ggerganov/llama.cpp). Support for Ollama and other runtimes is expected soon.

### 1. Install `llama.cpp` (if not already installed)

```bash
brew install llama.cpp
```
### 2. Pick your desired model variant and start the server

⚙️ Full Precision (FP16) Version:
```bash
llama-server -hf mrutkows/granite-4.0-tiny-preview-GGUF:F16
```
⚙️ 4-bit Quantized Version (Q4_K_M):
```bash
llama-server -hf mrutkows/granite-4.0-tiny-preview-GGUF:Q4_K_M
```

⚙️ 2-bit Quantized Version (Q2_K): This is the smallest one, may fit a mobile device?
```bash
llama-server -hf mrutkows/granite-4.0-tiny-preview-GGUF:Q2_K
```

### 3. Start Chatting

Open your browser and go to:
```bash
http://127.0.0.1:8080
```

### Optional: Monitor Resource Usage (Mac)

To monitor system performance, go to Applications → Utilities → Activity Monitor

Explore other variants of Granite 4.0 Tiny at Hugging Face
https://huggingface.co/mrutkows/granite-4.0-tiny-preview-GGUF/tree/main

