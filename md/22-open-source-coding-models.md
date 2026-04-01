# Open-Source & Open-Weight Coding Models: Comprehensive Guide (March 2026)

> State of the open-source coding model landscape as of March 25, 2026.
> Covers every notable model family, from frontier-class to laptop-friendly.

---

## Table of Contents

1. [Tier 1: Frontier Open Models](#tier-1-frontier-open-models)
2. [Tier 2: Strong Open Models](#tier-2-strong-open-models)
3. [Tier 3: Small/Efficient Models](#tier-3-smallefficient-models)
4. [Tier 4: Reasoning Models for Coding](#tier-4-reasoning-models-for-coding)
5. [Benchmark Comparison Tables](#benchmark-comparison-tables)
6. [Size vs Performance Analysis](#size-vs-performance-analysis)
7. [Recommendations by Use Case](#recommendations-by-use-case)
8. [How to Run These Models](#how-to-run-these-models)
9. [Tool Compatibility Matrix](#tool-compatibility-matrix)

---

## Tier 1: Frontier Open Models

These models compete with GPT-4o / Claude Sonnet 4 / Gemini 2.5 Pro on coding tasks.

---

### 1. DeepSeek-V3.1 / V3.2

| Field | Details |
|---|---|
| **Creator** | DeepSeek AI (China) |
| **Release** | V3: Dec 25, 2024; V3.1: Aug 2025; V3.2: Dec 2025 |
| **License** | MIT |
| **Parameters** | 671B total / 37B active (MoE) |
| **Context Window** | 128K tokens |
| **Training Data** | 14.8T tokens; pre-trained from scratch on diverse code + text |
| **Architecture** | Mixture-of-Experts with Multi-head Latent Attention (MLA) |

**Benchmark Scores:**
- HumanEval: 85.7%
- MBPP: 75.4%
- LiveCodeBench: 45.8-49.2% (V3.1)
- SWE-bench Verified: ~49.2% (V3), improved in V3.1/V3.2
- Codeforces: Competitive-level performance

**Key Strengths:**
- Exceptional cost-efficiency (trained for ~$5.5M)
- Strong agentic/tool-use capabilities in V3.1+
- Unified thinking/non-thinking mode in V3.1
- Best open model for general-purpose coding + reasoning hybrid tasks
- Supports 100+ programming languages

**How to Run:** Ollama (`deepseek-v3`), vLLM, llama.cpp (GGUF), HuggingFace TGI. Requires ~350GB VRAM for full precision; quantized versions fit on 4x A100 or 2x H100.

---

### 2. Qwen3-Coder (Alibaba)

| Field | Details |
|---|---|
| **Creator** | Qwen Team, Alibaba Cloud |
| **Release** | July 22, 2025 |
| **License** | Apache 2.0 |
| **Parameters** | 480B total / 35B active (MoE) |
| **Context Window** | 256K native, 1M with extrapolation |
| **Training Data** | 7.5T tokens with 70% code ratio |

**Benchmark Scores:**
- SWE-bench Verified: ~70% (state-of-the-art among open models at release)
- SWE-bench Pro: 44.3%
- LiveCodeBench: Strong (specific score varies by evaluation window)
- Aider Polyglot: Leading performance

**Key Strengths:**
- Purpose-built for agentic coding (not a general model adapted for code)
- 256K native context -- handles entire repositories
- Comes with Qwen Code CLI tool (open-source terminal coding agent)
- Best open model for SWE-bench style real-world software engineering tasks
- 92 programming languages supported

**How to Run:** Ollama (`qwen3-coder`), vLLM, HuggingFace, LM Studio. FP8 variant available. Requires significant GPU resources for full model; API access via Together AI, OpenRouter.

---

### 3. GLM-5 (Zhipu AI)

| Field | Details |
|---|---|
| **Creator** | Zhipu AI (China) |
| **Release** | February 2026 |
| **License** | MIT |
| **Parameters** | ~745B (MoE) / 44B active |
| **Context Window** | 128K+ tokens |
| **Training Data** | Trained entirely on Huawei Ascend chips (no NVIDIA GPUs) |

**Benchmark Scores:**
- SWE-bench Verified: 77.8% (highest among open-source at time of release)
- Humanity's Last Exam: 50.4% (beats Claude Opus 4.5)
- Industry's lowest hallucination rate claimed

**Key Strengths:**
- Top SWE-bench Verified score among open models
- Trained without NVIDIA hardware (Huawei Ascend ecosystem)
- Strong at agentic engineering tasks
- Excellent code generation + debugging

**How to Run:** HuggingFace, vLLM. Available on major Chinese cloud platforms.

---

### 4. GLM-4.7 (Zhipu AI)

| Field | Details |
|---|---|
| **Creator** | Zhipu AI (China) |
| **Release** | December 22, 2025 |
| **License** | Open-source (specific license TBD) |
| **Parameters** | ~355B (MoE) / 32B active |
| **Context Window** | 200K tokens |

**Benchmark Scores:**
- LiveCodeBench: 84.9% (ahead of Claude Sonnet 4.5)
- SWE-bench Verified: 73.8% (highest among open-source at time of release)

**Key Strengths:**
- Extremely cost-effective ($3/month via API, or free locally)
- Matches premium closed-source models on real coding benchmarks
- Strong across both competitive programming and real-world SWE tasks

**How to Run:** Ollama, vLLM, HuggingFace TGI.

---

### 5. Kimi K2 / K2.5 (Moonshot AI)

| Field | Details |
|---|---|
| **Creator** | Moonshot AI (China) |
| **Release** | K2: Mid-2025; K2.5: Late 2025 |
| **License** | Modified MIT License |
| **Parameters** | 1T total / 32B active (MoE) |
| **Context Window** | 128K tokens |
| **Training Data** | 15.5T tokens (K2 base); K2.5 adds ~15T mixed visual/text tokens |

**Benchmark Scores:**
- SWE-bench Verified: 65.8% (K2)
- SWE-bench Multilingual: 47.3%
- HumanEval: 99.0% (K2.5 -- highest of any model tracked)

**Key Strengths:**
- Top open-source non-reasoning model for coding
- Largest open MoE model (1T parameters)
- Specifically designed for tool use, reasoning, and autonomous problem-solving
- K2.5 excels at front-end development
- Zero training instability reported

**How to Run:** HuggingFace, vLLM. Model weights available for self-hosting.

---

### 6. Devstral 2 (Mistral AI)

| Field | Details |
|---|---|
| **Creator** | Mistral AI (France) |
| **Release** | Late 2025 |
| **License** | Modified MIT |
| **Parameters** | 123B dense transformer |
| **Context Window** | 256K tokens |

**Benchmark Scores:**
- SWE-bench Verified: 72.2%

**Key Strengths:**
- Dense architecture (not MoE) -- simpler deployment
- Up to 7x more cost-efficient than Claude Sonnet at real-world tasks
- Purpose-built for code agents
- Strong at multi-file codebase exploration and editing
- Comes with Mistral Vibe CLI (open-source coding assistant)

**How to Run:** HuggingFace, vLLM, compatible with OpenAI API format.

---

### 7. Llama 4 Maverick (Meta)

| Field | Details |
|---|---|
| **Creator** | Meta AI |
| **Release** | April 2025 |
| **License** | Llama 4 Community License (free up to 700M MAU) |
| **Parameters** | ~400B total / 17B active (128 experts MoE) |
| **Context Window** | 1M tokens (instruct), 256K pre-trained |
| **Training Data** | Massive multimodal corpus |

**Benchmark Scores:**
- LiveCodeBench: 43.4%
- Meta claims competitive with GPT-4o
- Independent testing (Rootly): 70% accuracy on SRE-focused coding (vs 90% for Qwen2.5-Coder-32B)

**Key Strengths:**
- Natively multimodal (text + image)
- 1M context window -- largest among open models at release
- Only 17B active parameters for inference efficiency
- Distilled from Llama 4 Behemoth (2T parameter teacher model)

**Caveats:** Independent benchmarks have shown underperformance vs Meta's claims on specialized coding tasks. Not a coding-specialized model.

**How to Run:** Ollama, vLLM, llama.cpp, HuggingFace. Fits on 2x A100-80GB with quantization.

---

## Tier 2: Strong Open Models

Compete with GPT-3.5 Turbo / Claude Sonnet 3.5 level on coding.

---

### 8. Qwen2.5-Coder-32B (Alibaba)

| Field | Details |
|---|---|
| **Creator** | Qwen Team, Alibaba Cloud |
| **Release** | November 2024 |
| **License** | Apache 2.0 |
| **Parameters** | 32B dense |
| **Context Window** | 128K tokens |
| **Training Data** | 5.5T tokens of code data, 92 programming languages |

**Benchmark Scores:**
- HumanEval: 92.7%
- MBPP: 90.2%
- MATH: 57.2%
- LiveCodeBench: 31.4%
- Aider Polyglot: 73.7% (comparable to GPT-4o)
- McEval (multilingual): 65.9
- MdEval: 75.2 (first among open-source)

**Key Strengths:**
- Best pure coding model at the 32B scale
- Exceptional multilingual coding (40+ languages)
- Strong at code completion, generation, debugging, and translation
- Practical to run on consumer hardware with quantization
- State-of-the-art open-source code model at release

**How to Run:** Ollama (`qwen2.5-coder:32b`), vLLM, llama.cpp, LM Studio, HuggingFace. Fits on single A100-80GB or 64GB Mac with Q4 quantization.

---

### 9. DeepSeek-Coder-V2 (DeepSeek AI)

| Field | Details |
|---|---|
| **Creator** | DeepSeek AI |
| **Release** | June 17, 2024 |
| **License** | Permissive (research + commercial) |
| **Parameters** | 236B total / 21B active (MoE) |
| **Context Window** | 128K tokens |
| **Training Data** | Code-focused + math enriched dataset |

**Benchmark Scores:**
- HumanEval: 90.2%
- MultiPL-E: 72.8% average across all languages
- Strong math/reasoning capabilities

**Key Strengths:**
- First open model to match closed-source models on code intelligence
- Extended context from 16K to 128K via Yarn technique
- Strong multilingual code support (338 languages)
- Efficient inference with only 21B active parameters

**How to Run:** Ollama, vLLM, HuggingFace. Smaller active parameter count makes it more efficient than total size suggests.

---

### 10. Codestral 25.01 / 25.08 (Mistral AI)

| Field | Details |
|---|---|
| **Creator** | Mistral AI (France) |
| **Release** | Codestral: May 2024; 25.01: Jan 2025; 25.08: Aug 2025 |
| **License** | Mistral AI Non-Production License (MNPL) for original; varies by version |
| **Parameters** | 22B |
| **Context Window** | 256K tokens |
| **Training Data** | 80+ programming languages |

**Benchmark Scores:**
- HumanEval: 86.6%
- MBPP: 91.2%
- #1 on LMsys Copilot Arena leaderboard (25.01)

**Key Strengths:**
- Optimized for low-latency, high-frequency code completion
- Fill-in-the-Middle (FIM) support
- Code correction and test generation
- 2x faster than original Codestral (25.01 improvement)
- Excellent for IDE integrations (tab completion)

**How to Run:** Ollama (`codestral`), vLLM, HuggingFace. 22B fits on a single GPU with quantization.

---

### 11. Llama 3.3 70B (Meta)

| Field | Details |
|---|---|
| **Creator** | Meta AI |
| **Release** | December 2024 |
| **License** | Llama 3.3 Community License |
| **Parameters** | 70B dense |
| **Context Window** | 128K tokens |
| **Training Data** | 15T tokens |

**Benchmark Scores:**
- HumanEval: 88.4%
- Near Llama 3.1 405B performance at fraction of compute

**Key Strengths:**
- General-purpose model with strong coding
- 128K context window for large codebases
- Well-supported across all major inference frameworks
- Matches Llama 3.1 405B quality on many tasks despite 5.8x fewer parameters

**How to Run:** Ollama (`llama3.3:70b`), vLLM, llama.cpp, HuggingFace. Requires ~40GB VRAM with Q4 quantization.

---

### 12. Llama 3.1 405B (Meta)

| Field | Details |
|---|---|
| **Creator** | Meta AI |
| **Release** | July 2024 |
| **License** | Llama 3.1 Community License |
| **Parameters** | 405B dense |
| **Context Window** | 128K tokens |
| **Training Data** | 15T+ tokens |

**Benchmark Scores:**
- HumanEval: 89.0%
- MBPP: ~88.6%

**Key Strengths:**
- Largest dense open model with frontier-class coding
- Near GPT-4o / Claude 3.5 Sonnet quality
- 128K context
- Excellent for distillation teacher

**Caveats:** Requires massive infrastructure (8x A100-80GB minimum). Largely superseded by MoE models for practical use.

**How to Run:** vLLM (multi-GPU), HuggingFace TGI. Not practical for local inference.

---

### 13. Devstral Small 2 (Mistral AI)

| Field | Details |
|---|---|
| **Creator** | Mistral AI (France) |
| **Release** | December 2025 |
| **License** | Apache 2.0 |
| **Parameters** | 24B |
| **Context Window** | 256K tokens |

**Benchmark Scores:**
- SWE-bench Verified: 68.0% (strongest open-weight at this size)

**Key Strengths:**
- Strongest open-weight SWE-bench model at the 24B scale
- Outscores many 70B-class competitors
- Runs on a single RTX 4090 or Mac with 32GB RAM
- Purpose-built for software engineering agent tasks
- Multi-file codebase exploration and editing
- Vision capabilities (can analyze images/screenshots)

**How to Run:** Ollama (`devstral`), llama.cpp (GGUF available from Unsloth), vLLM, LM Studio. Single consumer GPU viable.

---

## Tier 3: Small/Efficient Models

Run on laptops and consumer hardware. Under 15B parameters.

---

### 14. Qwen3-Coder-Next (Alibaba)

| Field | Details |
|---|---|
| **Creator** | Qwen Team, Alibaba Cloud |
| **Release** | February 2026 |
| **License** | Apache 2.0 |
| **Parameters** | 80B total / 3B active (ultra-sparse MoE) |
| **Context Window** | 256K tokens |

**Benchmark Scores:**
- SWE-bench Verified: 70.6% (with SWE-Agent), 71.3% (with OpenHands)
- SWE-bench Pro: 44.3%
- SWE-bench Multilingual: 62.8%
- Terminal-Bench 2.0: 36.2%
- SecCodeBench: 61.2%

**Key Strengths:**
- Beats DeepSeek-V3.2 on SWE-bench while using 0.4% of active parameters
- 10x higher throughput than full-size models for repository tasks
- Ultra-sparse design: only 3B parameters active per token
- Purpose-built for coding agents
- Runs locally on consumer hardware despite 80B total parameters

**How to Run:** Ollama (`qwen3-coder-next`), vLLM, LM Studio, llama.cpp. The 3B active parameter count means it runs efficiently on modest hardware.

---

### 15. Qwen2.5-Coder (Alibaba) -- Smaller Sizes

| Field | Details |
|---|---|
| **Creator** | Qwen Team, Alibaba Cloud |
| **Release** | November 2024 |
| **License** | Apache 2.0 (0.5B/1.5B/7B/14B/32B); Qwen Research License (3B) |
| **Sizes** | 0.5B, 1.5B, 3B, 7B, 14B |
| **Context Window** | 128K tokens |
| **Training Data** | 5.5T tokens, 92 languages |

**Benchmark Scores (7B):**
- HumanEval: 88.4%
- Strong across 40+ languages

**Benchmark Scores (14B):**
- Competitive with much larger general-purpose models on code tasks

**Key Strengths:**
- Best coding performance per parameter at every size class
- 7B model rivals many 33B models from 2023-2024
- Full range of sizes for every hardware tier
- Supports code generation, completion, debugging, explanation

**How to Run:** Ollama (`qwen2.5-coder:7b`, `qwen2.5-coder:14b`, `qwen2.5-coder:1.5b`), llama.cpp, LM Studio, vLLM.

---

### 16. Phi-4 (Microsoft)

| Field | Details |
|---|---|
| **Creator** | Microsoft Research |
| **Release** | December 2024 |
| **License** | MIT |
| **Parameters** | 14B |
| **Context Window** | 16K tokens |
| **Training Data** | Synthetic data heavy; curated web + code |

**Benchmark Scores:**
- HumanEval: 82.6%
- Surpasses Llama 3.3 70B on some benchmarks despite being 5x smaller

**Key Strengths:**
- Exceptional parameter efficiency
- Strong math + code reasoning
- MIT licensed -- fully permissive
- 14B fits on consumer GPUs easily

**How to Run:** Ollama (`phi4`), llama.cpp, HuggingFace, vLLM. Runs on 8GB+ VRAM GPUs.

---

### 17. Phi-3 (Microsoft)

| Field | Details |
|---|---|
| **Creator** | Microsoft Research |
| **Release** | April 2024 |
| **License** | MIT |
| **Sizes** | Mini (3.8B), Small (7B), Medium (14B) |
| **Context Window** | 4K or 128K variants |

**Benchmark Scores:**
- HumanEval (Mini): 59.1-62.8%
- HumanEval (MoE/3.5): 70.7%
- MBPP (MoE/3.5): 80.8%

**Key Strengths:**
- Phi-3 Mini runs on phones (3.8B)
- 128K context variant available
- Strong for size -- rivaling Mixtral 8x7B at a fraction of parameters
- MIT licensed

**How to Run:** Ollama, llama.cpp, ONNX Runtime, vLLM. Phone-deployable for Mini.

---

### 18. Yi-Coder (01.AI)

| Field | Details |
|---|---|
| **Creator** | 01.AI (China) |
| **Release** | September 2024 |
| **License** | Apache 2.0 |
| **Sizes** | 1.5B, 9B |
| **Context Window** | 128K tokens |

**Benchmark Scores:**
- HumanEval (9B-Chat): 85.4%
- MBPP (9B-Chat): 73.8%
- LiveCodeBench (9B-Chat): 23.4% (only sub-10B model to exceed 20%)
- CRUXEval-O: >50% (first open-source LLM to achieve this)

**Key Strengths:**
- State-of-the-art coding under 10B parameters
- 128K context window -- rare at this size
- Strong code editing and long-context comprehension
- Math reasoning via program-aided settings: 70.3% average accuracy

**How to Run:** Ollama, llama.cpp, vLLM, HuggingFace. 9B fits on consumer GPUs easily.

---

### 19. CodeGemma (Google)

| Field | Details |
|---|---|
| **Creator** | Google DeepMind |
| **Release** | April 2024 |
| **License** | Gemma license (permissive, commercial allowed) |
| **Sizes** | 2B (pretrained), 7B (pretrained), 7B (instruction-tuned) |
| **Context Window** | 8K tokens |
| **Training Data** | 500B additional tokens of code on top of Gemma base |

**Benchmark Scores:**
- HumanEval (2B): 44.5%
- HumanEval (7B-IT v1.1): 60.4%
- HumanEval Infilling (7B): 76.09% single-line, 58.44% multi-line

**Key Strengths:**
- Excellent code infilling (FIM) capabilities
- Lightweight -- 2B runs on edge devices
- Good for IDE code completion
- Multi-language support (Python, C++, Java, Go, JS, Kotlin, Rust)

**Caveats:** 8K context is limiting. Superseded by newer models on raw benchmarks.

**How to Run:** Ollama (`codegemma`), llama.cpp, HuggingFace, NVIDIA NIM.

---

### 20. OpenCoder (OpenCoder Team)

| Field | Details |
|---|---|
| **Creator** | OpenCoder Consortium (multi-institution) |
| **Release** | November 2024 |
| **License** | Apache 2.0 |
| **Sizes** | 1.5B, 8B |
| **Context Window** | 8K tokens |
| **Training Data** | 2.5T tokens (1.5B-32B range); full data pipeline open-sourced |

**Benchmark Scores:**
- HumanEval (8B-Instruct): ~83.5%
- HumanEval (8B-Base): 64.6%
- Competitive on BigCodeBench, LiveCodeBench, MultiPL-E

**Key Strengths:**
- Fully reproducible -- all training data, code, and recipes open-sourced
- 4.5M+ SFT entries released
- Best option for research on code LLM training
- Supports English and Chinese

**How to Run:** Ollama (`opencoder`), llama.cpp, vLLM, HuggingFace.

---

### 21. StarCoder2 (BigCode / HuggingFace / ServiceNow / NVIDIA)

| Field | Details |
|---|---|
| **Creator** | BigCode Project (HuggingFace, ServiceNow, NVIDIA consortium) |
| **Release** | February 2024 |
| **License** | BigCode OpenRAIL-M v1 |
| **Sizes** | 3B, 7B, 15B |
| **Context Window** | 16K tokens (sliding window attention: 4K) |
| **Training Data** | 3.3-4.3T tokens from The Stack v2 (600+ languages) |

**Benchmark Scores:**
- HumanEval (15B-Instruct): 72.6%
- HumanEval (15B-Base): 46.3%
- StarCoder2-3B outperforms StarCoderBase-15B
- StarCoder2-15B matches/outperforms CodeLlama-34B

**Key Strengths:**
- 600+ programming languages (broadest language coverage)
- Permissive OpenRAIL license with responsible use guidelines
- Strong on low-resource languages
- Part of the most transparent open-source code LLM project
- Good math and code reasoning despite moderate size

**How to Run:** Ollama (`starcoder2`), llama.cpp, vLLM, HuggingFace. 15B fits on single consumer GPU.

---

### 22. Granite Code Models (IBM)

| Field | Details |
|---|---|
| **Creator** | IBM Research |
| **Release** | May 2024 (original); Granite 3.0: Oct 2024; 3.3: Early 2025 |
| **License** | Apache 2.0 |
| **Sizes** | 3B, 8B, 20B, 34B |
| **Context Window** | 8K (base), 128K (long-context variants) |
| **Training Data** | 116 languages; 3B/8B: 4T tokens; 20B: 3T tokens; 34B: 1.4T tokens |

**Benchmark Scores:**
- HumanEval (Granite-3.0-8B): 52.44%
- Granite-3B is best performing small model (+3% over CodeGemma-2B)
- Strong on HumanEvalSynthesize (multilingual: JS, Java, Go, C++, Rust)

**Key Strengths:**
- Enterprise-focused with compliance and safety features
- Full Apache 2.0 license -- no restrictions
- Long-context variants (128K) for repository-level tasks
- Code synthesis, fixing, explanation, editing, and translation
- Well-integrated with IBM watsonx platform

**How to Run:** Ollama, vLLM, HuggingFace, IBM watsonx.ai. Also available on AWS SageMaker.

---

### 23. WizardCoder (WizardLM Team)

| Field | Details |
|---|---|
| **Creator** | WizardLM Team (Microsoft Research affiliated) |
| **Release** | V1.0: June 2023; V1.1: January 2024 |
| **License** | Llama 2 Community License (based on Code Llama/StarCoder) |
| **Sizes** | 15B, 33B, 34B |
| **Context Window** | 16K tokens |

**Benchmark Scores:**
- HumanEval (33B-V1.1): 79.9%
- HumanEval+ (33B-V1.1): 73.2%
- MBPP (33B-V1.1): 78.9%
- Outperforms ChatGPT 3.5, Gemini Pro, DeepSeek-Coder-33B-Instruct

**Key Strengths:**
- Evol-Instruct methodology for code (ICLR 2024 paper)
- Strong Python focus
- Good for straightforward code generation tasks

**Caveats:** No updates since January 2024. Superseded by newer models. Limited language breadth.

**How to Run:** Ollama, llama.cpp, HuggingFace. 33B fits on single A100 or 64GB Mac.

---

### 24. Phind-CodeLlama-34B-v2 (Phind)

| Field | Details |
|---|---|
| **Creator** | Phind |
| **Release** | Late 2023 |
| **License** | Llama 2 Community License |
| **Parameters** | 34B |
| **Context Window** | 16K tokens |
| **Training Data** | 1.5B tokens of high-quality programming instruction-answer pairs |

**Benchmark Scores:**
- HumanEval: 73.8%

**Key Strengths:**
- Strong multi-language proficiency (Python, C/C++, TypeScript, Java)
- Instruction-tuned for practical coding tasks
- Fine-tuned on high-quality problem-solution pairs (not just code completion)

**Caveats:** No updates since 2023. Superseded by newer models.

**How to Run:** Ollama, llama.cpp, HuggingFace.

---

### 25. Code Llama (Meta)

| Field | Details |
|---|---|
| **Creator** | Meta AI |
| **Release** | 7B/13B/34B: Aug 2023; 70B: Jan 2024 |
| **License** | Llama 2 Community License |
| **Sizes** | 7B, 13B, 34B, 70B |
| **Context Window** | 16K trained, up to 100K effective |
| **Training Data** | 500B tokens (7B-34B); 1T tokens (70B) |

**Benchmark Scores:**
- HumanEval (7B): 37.3%
- HumanEval (13B): 42.9%
- HumanEval (34B): 53.7%
- HumanEval (70B): 67.8%
- MBPP (70B): 62.2%

**Key Strengths:**
- Foundation model for many fine-tuned variants (WizardCoder, Phind, etc.)
- Fill-in-the-Middle support (7B, 13B, 70B)
- Python-specialized and instruction-tuned variants available
- Well-supported ecosystem

**Caveats:** Superseded by Llama 3.x and specialized coding models. Lower benchmarks than modern alternatives.

**How to Run:** Ollama, llama.cpp, vLLM, HuggingFace. Broadly supported.

---

### 26. Snowflake Arctic

| Field | Details |
|---|---|
| **Creator** | Snowflake |
| **Release** | April 2024 |
| **License** | Apache 2.0 |
| **Parameters** | 480B total / 17B active (Dense-MoE Hybrid) |
| **Context Window** | 4K tokens |
| **Training Data** | Enterprise-focused corpus |

**Benchmark Scores:**
- HumanEval+: 64.3%
- MBPP+: Competitive
- Spider (SQL): 79%

**Key Strengths:**
- Best-in-class for SQL generation
- Enterprise intelligence focus (SQL, code, instruction following)
- Efficient MoE architecture (17B active)
- Apache 2.0 with all data recipes open-sourced

**Caveats:** Small context window (4K). Not competitive with modern coding models on general programming. SQL is the sweet spot.

**How to Run:** HuggingFace, vLLM. Designed for Snowflake platform integration.

---

## Tier 4: Reasoning Models for Coding

Extended thinking / chain-of-thought models that excel at complex coding problems.

---

### 27. DeepSeek-R1 (DeepSeek AI)

| Field | Details |
|---|---|
| **Creator** | DeepSeek AI |
| **Release** | January 2025; R1-0528: May 2025 |
| **License** | MIT |
| **Parameters** | 685B total / ~37B active (MoE) |
| **Context Window** | 128K tokens |

**Benchmark Scores:**
- HumanEval: 90.2%
- SWE-bench Verified: 49.2% (original), 57.6% (R1-0528)
- LiveCodeBench: 63.5% (original), 73.3% (R1-0528)
- Codeforces: ~1930 rating (R1-0528)

**Distilled Variants (all MIT licensed):**
| Model | Base | LiveCodeBench | Codeforces |
|---|---|---|---|
| R1-Distill-Qwen-1.5B | Qwen-2.5-1.5B | 16.9% | -- |
| R1-Distill-Qwen-7B | Qwen-2.5-7B | Moderate | -- |
| R1-Distill-Qwen-14B | Qwen-2.5-14B | Good | -- |
| R1-Distill-Qwen-32B | Qwen-2.5-32B | 57.2% | 1691 |
| R1-Distill-Llama-8B | Llama-3.1-8B | Moderate | -- |
| R1-Distill-Llama-70B | Llama-3.3-70B | 57.5% | 1633 |

**Key Strengths:**
- Chain-of-thought reasoning produces step-by-step solutions
- Trained via reinforcement learning (not just SFT)
- Matches OpenAI o1 on coding and math
- Six distilled variants cover every hardware tier
- Thinking process is transparent and inspectable

**How to Run:** Ollama (`deepseek-r1`, or distilled: `deepseek-r1:7b`, etc.), vLLM, llama.cpp, HuggingFace. Distilled 7B/8B run on consumer hardware.

---

### 28. QwQ-32B (Alibaba)

| Field | Details |
|---|---|
| **Creator** | Qwen Team, Alibaba Cloud |
| **Release** | March 2025 |
| **License** | Apache 2.0 |
| **Parameters** | 32B dense |
| **Context Window** | 128K tokens |

**Benchmark Scores:**
- Matches DeepSeek-R1 and OpenAI o1-mini on reasoning
- Strong on LiveCodeBench and CodeForces
- 32B params vs DeepSeek-R1's 671B -- an order of magnitude smaller

**Key Strengths:**
- Best reasoning-per-parameter ratio
- Deep thinking capabilities for complex algorithmic problems
- Runs on much more accessible hardware than DeepSeek-R1
- Apache 2.0 license -- fully permissive

**How to Run:** Ollama (`qwq`), vLLM, llama.cpp, HuggingFace. Fits on single A100 or 64GB Mac.

---

### 29. Qwen3 (with Thinking Mode)

| Field | Details |
|---|---|
| **Creator** | Qwen Team, Alibaba Cloud |
| **Release** | April 29, 2025 |
| **License** | Apache 2.0 |
| **Sizes (Dense)** | 0.6B, 1.7B, 4B, 8B, 14B, 32B |
| **Sizes (MoE)** | 30B-A3B (30B total/3B active), 235B-A22B (235B total/22B active) |
| **Context Window** | 128K tokens |

**Benchmark Scores:**
- Qwen3-235B: Leads on CodeForces ELO, LiveCodeBench v5, BFCL
- Qwen3-30B-A3B: Strong performer, outranked only by QwQ-32B
- Thinking mode enables step-by-step reasoning for complex problems

**Key Strengths:**
- Dual mode: Thinking (deep reasoning) and Non-Thinking (quick answers)
- 8 sizes covering every hardware tier
- MoE variants are extremely efficient
- Strong coding, math, and general reasoning
- Apache 2.0 for all sizes

**How to Run:** Ollama (`qwen3`), vLLM, llama.cpp, HuggingFace, LM Studio. Qwen3-4B runs on phones; 30B-A3B runs on laptops.

---

### 30. Phi-4-Reasoning (Microsoft)

| Field | Details |
|---|---|
| **Creator** | Microsoft Research |
| **Release** | April 2025 |
| **License** | MIT |
| **Parameters** | 14B |
| **Context Window** | 32K tokens |

**Benchmark Scores:**
- 25+ percentage point improvement on LiveCodeBench over base Phi-4
- Strong on HumanEvalPlus
- Competitive with much larger reasoning models

**Key Strengths:**
- Smallest true reasoning model (14B)
- Trained via SFT on o3-mini reasoning demonstrations
- Reasoning-plus variant available for enhanced performance
- MIT licensed -- fully open
- Runs on consumer GPUs

**How to Run:** Ollama (`phi4-reasoning`), llama.cpp, vLLM, HuggingFace.

---

## Benchmark Comparison Tables

### Table 1: HumanEval Pass@1 (Python Code Generation)

| Model | Size (Active) | HumanEval | MBPP |
|---|---|---|---|
| Kimi K2.5 | 32B | **99.0%** | -- |
| Qwen2.5-Coder-32B | 32B | 92.7% | 90.2% |
| DeepSeek-Coder-V2 | 21B active | 90.2% | -- |
| DeepSeek-R1 | 37B active | 90.2% | -- |
| Llama 3.1 405B | 405B | 89.0% | ~88.6% |
| Qwen2.5-Coder-7B | 7B | 88.4% | -- |
| Llama 3.3 70B | 70B | 88.4% | -- |
| Codestral 25.01 | 22B | 86.6% | 91.2% |
| DeepSeek-V3 | 37B active | 85.7% | 75.4% |
| Yi-Coder-9B-Chat | 9B | 85.4% | 73.8% |
| OpenCoder-8B-Instruct | 8B | ~83.5% | -- |
| Phi-4 | 14B | 82.6% | -- |
| WizardCoder-33B-V1.1 | 33B | 79.9% | 78.9% |
| Phind-CodeLlama-34B-v2 | 34B | 73.8% | -- |
| StarCoder2-15B-Instruct | 15B | 72.6% | -- |
| Phi-3.5-MoE | 16B active | 70.7% | 80.8% |
| Code Llama 70B | 70B | 67.8% | 62.2% |
| Snowflake Arctic | 17B active | 64.3% | -- |
| CodeGemma-7B-IT | 7B | 60.4% | -- |
| Granite-3.0-8B | 8B | 52.44% | -- |
| CodeGemma-2B | 2B | 44.5% | -- |

### Table 2: SWE-bench Verified (Real-World Software Engineering)

| Model | Size (Active) | SWE-bench Verified |
|---|---|---|
| GLM-5 | 44B active | **77.8%** |
| GLM-4.7 | 32B active | 73.8% |
| Devstral 2 | 123B dense | 72.2% |
| Qwen3-Coder-Next | 3B active | 71.3% |
| Qwen3-Coder-480B | 35B active | ~70% |
| Devstral Small 2 | 24B dense | 68.0% |
| Kimi K2 | 32B active | 65.8% |
| DeepSeek-R1-0528 | 37B active | 57.6% |
| DeepSeek-V3 | 37B active | ~49.2% |
| Devstral (original) | 24B | 46.8% |

### Table 3: LiveCodeBench (Competitive Programming)

| Model | Size (Active) | LiveCodeBench |
|---|---|---|
| GLM-4.7 | 32B active | 84.9% |
| DeepSeek-R1-0528 | 37B active | 73.3% |
| DeepSeek-R1 | 37B active | 63.5% |
| DeepSeek-R1-Distill-Llama-70B | 70B | 57.5% |
| DeepSeek-R1-Distill-Qwen-32B | 32B | 57.2% |
| DeepSeek-V3.1 | 37B active | 45.8-49.2% |
| Llama 4 Maverick | 17B active | 43.4% |
| Codestral 25.01 | 22B | 37.9% |
| Qwen2.5-Coder-32B | 32B | 31.4% |
| Yi-Coder-9B-Chat | 9B | 23.4% |
| DeepSeek-R1-Distill-Qwen-1.5B | 1.5B | 16.9% |

---

## Size vs Performance Analysis

### Best Coding Performance Per VRAM Budget

| VRAM Budget | Best Model | Key Metric |
|---|---|---|
| **4-6 GB** | Qwen2.5-Coder-1.5B (Q4) or Qwen3-0.6B | Basic completion, 44-50% HumanEval |
| **8 GB** | Qwen2.5-Coder-7B (Q4) | 88.4% HumanEval -- exceptional for the VRAM |
| **12-16 GB** | Yi-Coder-9B or Phi-4 (Q4/Q6) | 85.4% / 82.6% HumanEval |
| **16-24 GB** | Devstral Small 2 (Q4) or Qwen2.5-Coder-14B | 68% SWE-bench / strong HumanEval |
| **24-32 GB** | Qwen2.5-Coder-32B (Q4) or QwQ-32B (Q4) | 92.7% HumanEval or reasoning mode |
| **32-48 GB** | Qwen3-Coder-Next (80B, 3B active) | 71.3% SWE-bench Verified with only 3B active |
| **48-80 GB** | Llama 3.3 70B (Q4) or DeepSeek-R1-Distill-Llama-70B | 88.4% HumanEval or 57.5% LiveCodeBench |
| **2x A100 (160GB)** | DeepSeek-V3.1 (quantized) | Full frontier performance |
| **4x A100+ (320GB+)** | Qwen3-Coder-480B or GLM-5 | State-of-the-art SWE-bench |

### Efficiency Champions (Performance / Active Parameters)

1. **Qwen3-Coder-Next** -- 71.3% SWE-bench with only 3B active parameters. The clear winner.
2. **Qwen2.5-Coder-7B** -- 88.4% HumanEval at just 7B parameters.
3. **Phi-4** -- 82.6% HumanEval at 14B. Best dense model efficiency.
4. **Llama 4 Maverick** -- 43.4% LiveCodeBench with 17B active parameters.
5. **DeepSeek-V3.1** -- Frontier performance with 37B active out of 671B total.

---

## Recommendations by Use Case

### Code Completion in IDE (Tab Autocomplete)
**Best:** Codestral 25.01 (22B) -- purpose-built for FIM, low-latency, #1 on copilot arena.
**Budget:** Qwen2.5-Coder-7B or CodeGemma-7B for FIM.
**Edge:** Qwen2.5-Coder-1.5B or CodeGemma-2B.

### Agentic Coding (Multi-File, Autonomous Engineering)
**Best:** Qwen3-Coder-480B or GLM-5 -- highest SWE-bench scores.
**Efficient:** Devstral Small 2 (24B) or Qwen3-Coder-Next (80B/3B active).
**API:** DeepSeek-V3.1 (cheapest frontier-class API).

### Competitive Programming / Algorithmic Challenges
**Best:** DeepSeek-R1-0528 or GLM-4.7 -- highest LiveCodeBench / Codeforces scores.
**Local:** QwQ-32B or DeepSeek-R1-Distill-Qwen-32B.

### Code Review & Explanation
**Best:** DeepSeek-V3.1 (thinking mode for thorough analysis).
**Local:** Qwen2.5-Coder-32B or Llama 3.3 70B.

### SQL Generation
**Best:** Snowflake Arctic (79% Spider) or DeepSeek-V3.1.
**Small:** Granite Code 8B (enterprise-oriented).

### Running on a Laptop (No GPU)
**Best:** Qwen2.5-Coder-7B (Q4_K_M) -- runs well on 16GB RAM Macs.
**Smaller:** Phi-4 (Q4), Yi-Coder-9B (Q4), or Qwen3-4B.
**Tiny:** Qwen2.5-Coder-1.5B or Qwen3-0.6B for machines with 8GB RAM.

### Enterprise / Production Deployment
**Best:** Granite Code (Apache 2.0, IBM support) or Qwen2.5-Coder (Apache 2.0).
**Compliance-sensitive:** Granite Code -- designed with enterprise guardrails.

### Research & Reproducibility
**Best:** OpenCoder -- full training pipeline, data, and checkpoints open-sourced.
**Also:** StarCoder2 -- transparent data sourcing via The Stack v2.

### Front-End / Web Development
**Best:** Kimi K2.5 -- specifically noted for front-end development excellence.
**Also:** Qwen3-Coder or Devstral Small 2.

### Multi-Language Support (Non-Python)
**Best:** StarCoder2-15B (600+ languages) or Qwen2.5-Coder-32B (92 languages).
**Also:** Codestral (80+ languages), DeepSeek-Coder-V2 (338 languages).

---

## How to Run These Models

### Ollama (Easiest Local Setup)
```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Run models
ollama run qwen2.5-coder:32b
ollama run deepseek-r1:32b
ollama run codestral
ollama run qwen3-coder
ollama run qwen3-coder-next
ollama run devstral
ollama run phi4
ollama run yi-coder:9b
ollama run starcoder2:15b
ollama run opencoder:8b
ollama run deepseek-v3          # Requires significant RAM
```

### llama.cpp (Maximum Performance, Custom Quantization)
```bash
# Build llama.cpp
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp && make -j

# Download GGUF models from HuggingFace (e.g., from TheBloke, Unsloth)
# Run with custom settings
./llama-server -m model.gguf -c 8192 -ngl 99 --port 8080
```

### vLLM (Production Serving)
```bash
pip install vllm

# Serve a model with OpenAI-compatible API
python -m vllm.entrypoints.openai.api_server \
  --model Qwen/Qwen2.5-Coder-32B-Instruct \
  --tensor-parallel-size 1 \
  --max-model-len 32768
```

### HuggingFace Transformers
```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_name = "Qwen/Qwen2.5-Coder-7B-Instruct"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name, device_map="auto")
```

### LM Studio (GUI for Mac/Windows/Linux)
Download from lmstudio.ai. Search for models directly in the app. Supports GGUF quantized models with one-click download and run.

---

## Tool Compatibility Matrix

### Aider (AI Pair Programming)
| Model | Support Level | Notes |
|---|---|---|
| DeepSeek-V3.1 | Excellent | Via API; 73.7% on Aider benchmark |
| Qwen2.5-Coder-32B | Excellent | Via Ollama or API; top Aider Polyglot score |
| Qwen3-Coder | Excellent | Via API or local |
| Llama 3.3 70B | Good | Via Ollama |
| Codestral | Good | Via Mistral API |
| Any Ollama model | Good | Aider supports `--model ollama/model-name` |

### Continue (VS Code / JetBrains Extension)
| Model | Support Level | Notes |
|---|---|---|
| All Ollama models | Native | Configure in `config.json` |
| All OpenAI-compatible APIs | Native | vLLM, llama.cpp server, LM Studio |
| Codestral | Excellent | Purpose-built for tab completion in Continue |
| Qwen2.5-Coder | Excellent | Recommended for autocomplete |

### Cline (VS Code Extension -- Autonomous Coding Agent)
| Model | Support Level | Notes |
|---|---|---|
| All Ollama models | Supported | Adjust context window to match VRAM |
| Devstral Small 2 | Excellent | Specifically designed for Cline-style agents |
| Qwen3-Coder-Next | Excellent | Optimized for agentic coding tools |
| DeepSeek-V3.1 | Excellent | Via OpenAI-compatible API |
| Any OpenAI-compatible API | Supported | LM Studio, vLLM, llama.cpp |

### Claude Code (via API Proxy)
| Model | Support Level | Notes |
|---|---|---|
| DeepSeek-V3.1 | Usable | Via OpenAI-compatible proxy (e.g., LiteLLM) |
| Qwen3-Coder | Usable | Via proxy with function calling support |
| Any model with tool-use | Experimental | Requires proxy that translates tool-calling format |

### Cursor / Windsurf / Other IDEs
Most IDEs support OpenAI-compatible APIs, so any model served via vLLM, llama.cpp, or LM Studio can be used. Performance varies based on the model's function-calling and code-completion capabilities.

---

## Notable Trends (March 2026)

1. **MoE dominance**: Nearly every frontier model uses Mixture-of-Experts. Active parameter counts of 3B-37B provide frontier performance at a fraction of dense model cost.

2. **SWE-bench is the new HumanEval**: HumanEval saturation (99%+ scores from Kimi K2.5) has shifted focus to SWE-bench Verified as the primary coding benchmark. Real-world repository-level tasks matter more than isolated function generation.

3. **Chinese labs lead open-source**: DeepSeek, Qwen (Alibaba), Zhipu AI (GLM), Moonshot AI (Kimi), and 01.AI (Yi) collectively produce the majority of top open coding models. Mistral (France) is the notable Western exception.

4. **Agentic coding models**: The latest generation (Qwen3-Coder, Devstral, GLM-4.7) is specifically trained for autonomous software engineering -- multi-file editing, tool use, terminal interaction -- not just code completion.

5. **Ultra-sparse efficiency**: Qwen3-Coder-Next (80B/3B active) demonstrates that extreme sparsity can achieve near-frontier SWE-bench scores while being runnable on consumer hardware.

6. **Reasoning models for code**: DeepSeek-R1, QwQ, Phi-4-Reasoning, and Qwen3's thinking mode bring chain-of-thought reasoning to coding, excelling on competitive programming and complex debugging.

7. **Context windows expanding**: 128K is now standard; 256K available on Codestral/Devstral/Qwen3-Coder; 1M available on Llama 4 Maverick and Qwen3-Coder (extrapolated).

8. **Apache 2.0 becoming standard**: Most new releases use Apache 2.0 or MIT, making commercial use straightforward. Restrictive licenses (Llama Community License, MNPL) are becoming the exception.

---

## Quick Reference: Model Release Timeline

| Date | Model | Milestone |
|---|---|---|
| Aug 2023 | Code Llama | Meta's first dedicated code model |
| Feb 2024 | StarCoder2 | 600+ language coverage |
| Apr 2024 | CodeGemma | Google's code-specialized Gemma |
| Apr 2024 | Snowflake Arctic | Enterprise SQL focus |
| May 2024 | Granite Code | IBM's enterprise code models |
| Jun 2024 | DeepSeek-Coder-V2 | First open model to match closed-source |
| Sep 2024 | Yi-Coder | SotA under 10B params |
| Nov 2024 | Qwen2.5-Coder | 92.7% HumanEval at 32B |
| Nov 2024 | OpenCoder | Fully reproducible training |
| Dec 2024 | DeepSeek-V3 | MoE efficiency breakthrough |
| Dec 2024 | Llama 3.3 | 70B matching 405B |
| Dec 2024 | Phi-4 | 82.6% HumanEval at 14B |
| Jan 2025 | DeepSeek-R1 | Open reasoning model revolution |
| Jan 2025 | Codestral 25.01 | #1 copilot arena |
| Mar 2025 | QwQ-32B | Reasoning at 32B |
| Apr 2025 | Llama 4 | MoE + 1M context |
| Apr 2025 | Phi-4-Reasoning | Reasoning at 14B |
| Apr 2025 | Qwen3 | 8 sizes, thinking mode |
| May 2025 | DeepSeek-R1-0528 | 57.6% SWE-bench |
| Jul 2025 | Qwen3-Coder-480B | 70% SWE-bench, agentic |
| Aug 2025 | DeepSeek-V3.1 | Unified thinking/non-thinking |
| Dec 2025 | GLM-4.7 | 84.9% LiveCodeBench, 73.8% SWE-bench |
| Dec 2025 | Devstral 2 / Small 2 | 72.2% / 68.0% SWE-bench |
| Dec 2025 | DeepSeek-V3.2 | Iterative improvement |
| Dec 2025 | Kimi K2.5 | 99.0% HumanEval |
| Feb 2026 | GLM-5 | 77.8% SWE-bench, trained on Ascend |
| Feb 2026 | Qwen3-Coder-Next | 71.3% SWE-bench with 3B active |
| TBD 2026 | DeepSeek-V4 | 1T params, 1M context (not yet released) |

---

## Summary

The open-source coding model landscape in March 2026 is remarkably competitive with closed-source alternatives. For practical use:

- **If you need the absolute best open coding model**: GLM-5 (77.8% SWE-bench) or Qwen3-Coder-480B (~70% SWE-bench) for agentic tasks; Kimi K2.5 (99% HumanEval) for raw code generation.
- **If you want frontier quality at reasonable compute**: DeepSeek-V3.1 (37B active) offers the best performance-per-dollar via API.
- **If you need to run locally on a single GPU**: Qwen2.5-Coder-32B (92.7% HumanEval) or Devstral Small 2 (68% SWE-bench at 24B).
- **If you want reasoning for hard problems**: DeepSeek-R1 or QwQ-32B.
- **If you have only a laptop CPU**: Qwen2.5-Coder-7B quantized or Qwen3-Coder-Next (3B active).
- **If reproducibility matters**: OpenCoder (full pipeline open-sourced).
- **If you need SQL specifically**: Snowflake Arctic.
- **If enterprise compliance matters**: IBM Granite Code (Apache 2.0, enterprise guardrails).

The gap between open and closed models has never been smaller. For many practical coding tasks, open models are now the better choice when considering cost, privacy, and customizability.

---

*Document compiled: March 25, 2026*
*Coverage: All notable open-source and open-weight coding models through March 2026*
