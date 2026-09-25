---
license: apache-2.0
library_name: transformers
pipeline_tag: text-generation
base_model: HuggingFaceTB/SmolLM-360M
tags:
- gguf
- llama.cpp
- text-generation
- smollm
---

# SmolLM-360M GGUF

[Source model](https://huggingface.co/HuggingFaceTB/SmolLM-360M) · [HF release](https://huggingface.co/ShayonSarker/SmolLM-360M-GGUF) · [Build hub](https://github.com/Dadhichi-Sarker-Shayon/SmolLM-360M-GGUF)

Pinned, reproducible llama.cpp GGUF conversion of the 362M-parameter SmolLM base model. The source is Apache-2.0 licensed and uses a 2,048-token context window.

## Formats

| File | Purpose |
|---|---|
| `smollm-360m-F16.gguf` | Reference quality |
| `smollm-360m-Q8_0.gguf` | Higher-quality compact format |
| `smollm-360m-Q4_K_M.gguf` | Smallest release format |

## Validation

WikiText-2 raw test evaluation, 8 chunks of 512 tokens. Lower perplexity is better.

| Format | PPL | Ratio to F16 |
|---|---:|---:|
| F16 | 14.5685 | Baseline |
| Q8_0 | 14.6009 | 1.0022 |
| Q4_K_M | 14.8333 | 1.0182 |

A deterministic Q4_K_M generation smoke test completed successfully. This is a base language model, not an instruction-tuned assistant.

## Build

```bash
python -m pip install -r requirements-build.txt
python build_gguf.py --model-id HuggingFaceTB/SmolLM-360M
```

The builder pins llama.cpp commit `6b790a9c291b5d7af3312bbf9f0c558aa023b13e` and the upstream model revision. It does not upload or overwrite this repository.

## License

Apache-2.0. See the upstream model card and `LICENSE` for source attribution.
