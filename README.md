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
- 360m
- small-model
- edge-ai
- quantization
- q4_k_m
- q8_0
- wikitext-2
---

# SmolLM-360M GGUF

<div align="center">

<a href="https://huggingface.co/ShayonSarker/SmolLM-360M-GGUF"><img alt="Hugging Face" src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge"></a>
<a href="https://github.com/Dadhichi-Sarker-Shayon/SmolLM-360M-GGUF"><img alt="GitHub" src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge"></a>

<img alt="SmolLM" src="https://img.shields.io/badge/model-SmolLM--360M-8A2BE2?style=for-the-badge">
<img alt="GGUF formats" src="https://img.shields.io/badge/GGUF-F16%20%7C%20Q8_0%20%7C%20Q4_K_M-FFD21E?style=for-the-badge">
<img alt="Parameters" src="https://img.shields.io/badge/params-362M-00A6A6?style=for-the-badge">
<img alt="Context" src="https://img.shields.io/badge/context-2048-16A34A?style=for-the-badge">
<img alt="License" src="https://img.shields.io/badge/license-Apache--2.0-7C3AED?style=for-the-badge">

</div>

[Source model](https://huggingface.co/HuggingFaceTB/SmolLM-360M) · [HF release](https://huggingface.co/ShayonSarker/SmolLM-360M-GGUF) · [Build hub](https://github.com/Dadhichi-Sarker-Shayon/SmolLM-360M-GGUF)

Pinned, reproducible llama.cpp GGUF conversion of the 362M-parameter SmolLM base model. The source is Apache-2.0 licensed and uses a 2,048-token context window.

## Formats

| File | Status | Purpose |
|---|---|---|
| `smollm-360m-F16.gguf` | Published | Reference quality |
| `smollm-360m-Q8_0.gguf` | Published | Higher-quality compact format |
| `smollm-360m-Q4_K_M.gguf` | Published | Smallest release format |

## Verified outputs

Verbatim `smollm-360m-Q4_K_M.gguf` completions, `--temp 0`, 24 new tokens, prompt form `Question: ...\nAnswer:`. Text after the first sentence is trimmed with `…`. The model is a base LM, so it keeps inventing new questions after answering; that behaviour is left unedited.

| Question | Model answer |
|---|---|
| What is the capital of Japan? | `Tokyo is the capital of Japan.` |
| What is the capital of Italy? | `The capital of Italy is Rome.` |
| What is the capital of Egypt? | `The capital of Egypt is Cairo.` |
| What is the largest ocean on Earth? | `The largest ocean on Earth is the Pacific Ocean. It covers about 30% of the Earth…` |
| Which planet is closest to the Sun? | `Mercury. It is the closest planet to the Sun.` |
| How many days are in a leap year? | `366 days.` |
| How many continents are there? | `There are seven continents in the world.` |
| What is the chemical symbol for gold? | `The chemical symbol for gold is Au.` |

Eight of eight short factual lookups are correct. Treat longer output as unreliable: the model is small, has no instruction tuning, and drifts into a new fabricated `Q:`/`A:` pair once it finishes a sentence.

## Validation

WikiText-2 raw test evaluation, 8 chunks of 512 tokens. Lower perplexity is better.

| Format | PPL | Ratio to F16 |
|---|---:|---:|
| F16 | 14.5685 | Baseline |
| Q8_0 | 14.6009 | 1.0022 |
| Q4_K_M | 14.8333 | 1.0182 |

## Build

```bash
python -m pip install -r requirements-build.txt
python build_gguf.py --model-id HuggingFaceTB/SmolLM-360M
```

The builder pins llama.cpp commit `6b790a9c291b5d7af3312bbf9f0c558aa023b13e` and the upstream model revision. It does not upload or overwrite this repository.

## License

Apache-2.0. See the upstream model card and `LICENSE` for source attribution.
