# Chinese AI Coding Models, Tools & Platforms: Comprehensive Guide (March 2026)

> The Chinese AI coding ecosystem has undergone a dramatic transformation since 2024. What was once a 30+ percentage-point gap on HumanEval has collapsed to near parity -- and in several categories, Chinese models now lead. This document covers every major model, tool, platform, and ecosystem development as of March 2026.

---

## Table of Contents

1. [Models by Company](#1-models-by-company)
   - [DeepSeek](#deepseek)
   - [Alibaba / Qwen](#alibaba--qwen)
   - [Moonshot AI / Kimi](#moonshot-ai--kimi)
   - [Zhipu AI (Z.ai)](#zhipu-ai-zai)
   - [MiniMax](#minimax)
   - [01.AI (Yi)](#01ai-yi)
   - [Baidu (ERNIE)](#baidu-ernie)
   - [Ant Group (CodeFuse / Ling)](#ant-group-codefuse--ling)
   - [SenseTime (SenseNova)](#sensetime-sensenova)
   - [Baichuan](#baichuan)
   - [Shanghai AI Lab (InternLM)](#shanghai-ai-lab-internlm)
2. [IDE & Coding Tools](#2-ide--coding-tools)
   - [Tongyi Lingma (Alibaba)](#tongyi-lingma-alibaba)
   - [Qwen Code CLI (Alibaba)](#qwen-code-cli-alibaba)
   - [Kimi Code CLI (Moonshot)](#kimi-code-cli-moonshot)
   - [CodeGeeX (Zhipu AI)](#codegeex-zhipu-ai)
   - [Trae IDE (ByteDance)](#trae-ide-bytedance)
   - [Baidu Comate](#baidu-comate)
   - [Tencent CodeBuddy](#tencent-codebuddy)
   - [Fitten Code](#fitten-code)
   - [DevChat (Merico)](#devchat-merico)
3. [Benchmarks Comparison Table](#3-benchmarks-comparison-table)
4. [Unique Strengths of Chinese Models](#4-unique-strengths-of-chinese-models)
5. [Access & Availability Outside China](#5-access--availability-outside-china)
6. [Chinese Coding Benchmarks & Communities](#6-chinese-coding-benchmarks--communities)
7. [Regulatory Considerations](#7-regulatory-considerations)

---

## 1. Models by Company

### DeepSeek

DeepSeek, founded in 2023 and funded by the quantitative trading firm High-Flyer, has become the most prominent Chinese AI lab in global developer consciousness. Their models are fully open-source under the MIT License.

#### DeepSeek-Coder-V2 (June 2024)

| Attribute | Details |
|-----------|---------|
| **Creator** | DeepSeek |
| **Release** | June 2024 |
| **License** | DeepSeek License (commercial use allowed) |
| **Architecture** | MoE (Mixture-of-Experts) |
| **Total Parameters** | 236B (large) / 16B (lite) |
| **Active Parameters** | 21B (large) / 2.4B (lite) |
| **Context Window** | 128K tokens |
| **Languages Supported** | 338 programming languages |
| **Training Data** | 6T additional tokens on top of DeepSeek-V2 |
| **HumanEval** | ~85% (Pass@1) |
| **Availability** | HuggingFace, ModelScope, API |

DeepSeek-Coder-V2 was the first open-source model to match GPT-4 Turbo on code-specific tasks. It was further pre-trained from an intermediate checkpoint of DeepSeek-V2, substantially enhancing coding and mathematical reasoning while maintaining general language capabilities.

#### DeepSeek-V3 (December 2024)

| Attribute | Details |
|-----------|---------|
| **Creator** | DeepSeek |
| **Release** | December 2024 |
| **License** | MIT License |
| **Architecture** | MoE with Multi-head Latent Attention (MLA) |
| **Total Parameters** | 671B |
| **Active Parameters** | 37B per token |
| **Context Window** | 128K tokens |
| **Training Cost** | ~$5.6M (2.788M H800 GPU hours) |
| **HumanEval** | 85.7% |
| **MBPP** | 75.4% |
| **SWE-bench Verified** | 47.8% |

**Key Innovations:**
- **FP8 Mixed Precision Training**: First model to validate FP8 training at extreme scale, reducing both GPU memory and compute.
- **Multi-Head Latent Attention (MLA)**: Reduces KV-cache memory by 93.3%, dramatically cutting inference costs.
- **Auxiliary-Loss-Free Load Balancing**: Eliminates auxiliary losses for MoE routing, using bias terms instead -- a novel approach that improves both training stability and quality.
- **Training Cost**: The reported $5.6M figure covers only GPU compute for pre-training. Total R&D costs (including prior research, failed experiments, and team salaries) are estimated at $500M-$1.3B. Regardless, the per-token training efficiency is extraordinary.

#### DeepSeek-R1 (January 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | DeepSeek |
| **Release** | January 20, 2025 |
| **License** | MIT License |
| **Architecture** | Same 671B MoE as V3, with RL-enhanced reasoning |
| **Context Window** | 64K tokens |
| **API Pricing** | $0.55/M input, $2.19/M output tokens |
| **HumanEval-Mul** | 82.6% |
| **SWE-bench Verified** | 50.8% |
| **MATH-500** | 90.2% |
| **Codeforces Rating** | 2,029 (Candidate Master) |

R1 was trained with heavy reinforcement learning to develop Chain-of-Thought reasoning, reflection, and multi-step verification. It matches or exceeds OpenAI's o1 on most mathematical and reasoning benchmarks.

#### DeepSeek-V3.1 (August 2025)

| Attribute | Details |
|-----------|---------|
| **Release** | August 2025 |
| **License** | MIT License |
| **Key Improvements** | Optimized for domestic AI accelerators; hybrid thinking/non-thinking modes |
| **Aider Benchmark** | 71.6% pass rate (surpassing Claude Opus) |
| **Cost** | 68x cheaper than Claude Opus |

V3.1 marked DeepSeek's deliberate pivot toward hardware independence and supply chain resilience. Its Deep Thinking Mode achieves 90-95% of R1's reasoning performance.

#### DeepSeek-V3.2 (December 2025)

| Attribute | Details |
|-----------|---------|
| **Release** | December 2025 |
| **License** | MIT License |
| **Key Innovation** | DeepSeek Sparse Attention (DSA) -- O(n) complexity |
| **AIME** | 96.0% (V3.2-Speciale) |
| **Competition Results** | Gold-level at IMO, CMO, ICPC World Finals, IOI 2025 |

V3.2-Speciale outperforms GPT-5 on several reasoning benchmarks. It is the first model to integrate thinking directly into tool-use, supporting both thinking and non-thinking modes during tool calls.

---

### Alibaba / Qwen

Alibaba's Qwen (Tongyi Qianwen) team has built the most prolific open-source model family in the world. By mid-2025, Qwen became the model with the most derivatives on HuggingFace, surpassing Meta's Llama with over 113,000 derivative models.

#### Qwen2.5-Coder (November 2024)

| Attribute | Details |
|-----------|---------|
| **Creator** | Alibaba / Qwen Team |
| **Release** | November 2024 |
| **License** | Apache 2.0 (most sizes), Qwen License (larger) |
| **Architecture** | Dense Transformer |
| **Sizes** | 0.5B, 1.5B, 3B, 7B, 14B, 32B |
| **Context Window** | 128K tokens |
| **Training Data** | 5.5T tokens, 92+ programming languages |
| **Variants** | Base and Instruct for each size |
| **Availability** | HuggingFace, ModelScope, Ollama |

**HumanEval Pass@1 scores by size (Instruct variants):**

| Size | HumanEval | Notes |
|------|-----------|-------|
| 0.5B | ~61% | Smallest competitive code model |
| 1.5B | 70.7% | |
| 3B | 78.7% | |
| 7B | 79.7% | Surpasses CodeStral-22B |
| 14B | 80.5% | Surpasses DS-Coder-33B-Instruct |
| 32B | 92.7% (base) / 88.4% (instruct) | SOTA among open-source |

**Additional 32B-Instruct scores:**
- MBPP: 84.0%
- LiveCodeBench: 51.2%
- BigCodeBench, EvalPlus, CrossCodeEval: SOTA among open-source

The Qwen2.5-Coder series demonstrates remarkable parameter efficiency -- the 7B model outperforms models 3-4x its size.

#### Qwen3-Coder (Mid-2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Alibaba / Qwen Team |
| **Release** | Mid-2025 |
| **Architecture** | MoE |
| **Total Parameters** | 480B |
| **Active Parameters** | 35B per token |
| **SWE-bench Verified** | ~69.6% |
| **Key Feature** | Performs on par with Claude Sonnet 4 on agentic coding |

Accompanied by the Qwen Code CLI tool, Qwen3-Coder set new benchmarks among open models for agentic coding, browser use, and tool use.

#### Qwen3-Coder-Next (February 2026)

| Attribute | Details |
|-----------|---------|
| **Creator** | Alibaba / Qwen Team |
| **Release** | February 2026 |
| **Architecture** | Ultra-sparse MoE |
| **Total Parameters** | 80B |
| **Active Parameters** | 3B per token |
| **SWE-bench Verified** | 70.6% |
| **SWE-bench Pro** | 44.3% |
| **SWE-bench Multilingual** | 62.8% |
| **Throughput** | Up to 10x higher than dense models of similar size |

Designed specifically for coding agents and local development. Trained on ~800K verifiable tasks with executable environments, using large-scale RL. Outperforms Claude Opus 4.5 on secure code generation benchmarks.

---

### Moonshot AI / Kimi

Moonshot AI, founded by former Tsinghua and Google researchers, has rapidly risen to become one of China's most capable AI labs, particularly in agentic coding.

#### Kimi K2 (July 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Moonshot AI |
| **Release** | July 2025 |
| **License** | Modified MIT License |
| **Architecture** | MoE with MLA |
| **Total Parameters** | 1 trillion |
| **Active Parameters** | 32B |
| **Layers** | 61 (including 1 dense layer) |
| **Experts** | 384 total, 8 selected + 1 shared per token |
| **Context Window** | 128K tokens |
| **SWE-bench Verified** | 65.8% |
| **GSM8K** | 94.4% (surpassing GPT-4.1 and Claude Opus 4) |

#### Kimi K2.5 (January 2026)

| Attribute | Details |
|-----------|---------|
| **Creator** | Moonshot AI |
| **Release** | January 27, 2026 |
| **License** | Open-weight |
| **Architecture** | 1T MoE + MoonViT-3D (400M vision encoder) |
| **Context Window** | 256K tokens |
| **SWE-bench Verified** | 76.8% |
| **AIME 2025** | 96.1% |
| **Humanity's Last Exam** | 50.2% (at 76% lower cost than Claude Opus 4.5) |
| **API Pricing** | $0.60/M input tokens |
| **Availability** | HuggingFace, NVIDIA NIM, Kimi API |

**Key Innovation -- Agent Swarm Technology**: Coordinates up to 100 specialized AI agents working simultaneously, cutting execution time by 4.5x. Uses Parallel Agent Reinforcement Learning (PARL), a novel RL technique that addresses training instability, credit assignment, and "serial collapse" in multi-agent settings.

**Visual-to-Code**: As a native multimodal model, K2.5 turns text, images, and video inputs into functional front-end code with high fidelity. Powers complete visual-to-code workflows including complex page layouts, full websites with animations, and interactive UI.

**Industry Impact**: Cursor confirmed that its Composer 2 was built partially on Kimi technology (~25% of compute from Kimi base model).

---

### Zhipu AI (Z.ai)

Zhipu AI, spun out of Tsinghua University's KEG Lab, rebranded as Z.ai in late 2025. Their GLM series has become a serious contender in coding.

#### GLM-4.7 (December 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Zhipu AI / Z.ai |
| **Release** | December 22, 2025 |
| **License** | Open-weight |
| **Architecture** | MoE |
| **Total Parameters** | ~355B |
| **Active Parameters** | 32B per forward pass |
| **Context Window** | 200K tokens (128K max output) |
| **Inference Speed** | 55 tokens/sec |
| **API Pricing** | ~$3/month |

**Benchmark Scores:**

| Benchmark | Score |
|-----------|-------|
| HumanEval | 94.2% |
| SWE-bench Verified | 73.8% |
| LiveCodeBench v6 | 84.9% |
| AIME 2025 | 95.7% |
| MATH | 92% |
| GSM8k | 98% |
| MMLU | 88% |

**Advanced Features:**
- **Preserved Thinking**: Maintains reasoning chains across multiple conversation turns.
- **Interleaved Thinking**: Pauses to "reason aloud" before executing tool calls.

GLM-4.7 is arguably the most well-rounded open-source coding model available as of early 2026, matching premium competitors while costing a fraction.

**Industry Impact**: Windsurf confirmed that its core model (SWE-1.5) originated from Z.ai / Zhipu AI technology.

#### GLM-5 (February 2026)

| Attribute | Details |
|-----------|---------|
| **Release** | February 2026 |
| **Pricing** | ~30% higher than GLM-4.7 |
| **Improvements** | Enhanced reasoning and code generation |

---

### MiniMax

MiniMax, founded in 2021 by former SenseTime VP Yan Junjie, has made an aggressive push into coding with its M-series models.

#### MiniMax-M2 (Q4 2025)

| Attribute | Details |
|-----------|---------|
| **Release** | Q4 2025 |
| **License** | Open-source |
| **Key Focus** | Coding, tool use, deep search |
| **Integration** | Claude Code, Cursor, Cline, Kilo Code, Droid |

#### MiniMax-M2.5 (February 2026)

| Attribute | Details |
|-----------|---------|
| **Creator** | MiniMax |
| **Release** | February 12, 2026 |
| **License** | Open-source |
| **Architecture** | MoE with Lightning Attention, 8 experts per token |
| **Total Parameters** | 230B |
| **Active Parameters** | 10B |
| **SWE-bench Verified** | 80.2% (#1 among open-source, ahead of Claude Opus 4.6) |
| **Multi-SWE-Bench** | 51.3% (#1 overall, ahead of Opus 4.6's 50.3%) |
| **BrowseComp** | 76.3% |
| **HumanEval** | 89.6% |
| **Training Languages** | 10+ (Go, C, C++, TypeScript, Rust, Kotlin, Python, Java, JS, PHP, Lua, Dart, Ruby) |
| **Training Environments** | 200,000+ real-world RL environments |

M2.5 plans features like an architect -- actively decomposing tasks, planning structure and UI before writing code. It's 37% faster than M2.1 on agentic tasks. At 10B active parameters, it delivers frontier performance at roughly 1/20th the cost.

---

### 01.AI (Yi)

01.AI was founded by Dr. Kai-Fu Lee (former president of Google China, Microsoft Research, and Apple).

#### Yi-Coder (September 2024)

| Attribute | Details |
|-----------|---------|
| **Creator** | 01.AI |
| **Release** | September 2024 |
| **License** | Apache 2.0 |
| **Architecture** | Dense Transformer (based on Yi-9B) |
| **Sizes** | 1.5B, 9B |
| **Context Window** | 128K tokens |
| **Training Data** | 2.4T tokens, 52 programming languages |
| **Availability** | HuggingFace, Ollama |

**Yi-Coder-9B-Chat Benchmarks:**

| Benchmark | Score |
|-----------|-------|
| HumanEval | 85.4% |
| MBPP | 73.8% |
| LiveCodeBench | 23.4% (first <10B model to exceed 20%) |
| CRUXEval-O | >50% (first open-source to pass this threshold) |
| PAL Math | 70.3% (surpasses DeepSeek-Coder-33B) |

Yi-Coder proves that sub-10B models can deliver serious coding performance. However, the company's focus has shifted more toward general-purpose models and consumer products (Yi Lightning, Yi Chat) in 2025-2026.

---

### Baidu (ERNIE)

Baidu, often called "China's Google," has a deep AI research tradition through its PaddlePaddle framework and ERNIE model series.

#### ERNIE 4.5 (March 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Baidu |
| **Release** | March 2025 |
| **License** | Apache 2.0 |
| **Architecture** | MoE |
| **Sizes** | 10 variants from 0.3B dense to 424B MoE |
| **Active Parameters** | 3B to 47B depending on variant |
| **Context Window** | 128K tokens |
| **HumanEval+** | >90% |
| **MBPP** | >80% |

**Caveats**: Independent assessments show ERNIE 4.5 performs significantly worse than GPT-4.5 and DeepSeek on LiveCodeBench and more challenging coding benchmarks. Its strengths are more in general knowledge, content creation, and Chinese-language tasks.

#### ERNIE 5.0 (November 2025)

Announced at Baidu World 2025 with improved reasoning capabilities. Baidu reports that 45% of new code within Baidu is now AI-generated.

#### ERNIE X1.1 (Reasoning Model)

A dedicated reasoning model with upgrades in mathematical computation, code generation, and tool use. Supports 128K context window.

---

### Ant Group (CodeFuse / Ling)

Ant Group, Alibaba's fintech arm (Alipay parent), operates a distinct AI research organization.

#### CodeFuse (2023-2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Ant Group |
| **Release** | September 2023 (initial), ongoing |
| **License** | Open-source |
| **Focus** | Full SDLC: design, requirements, coding, testing, deployment, ops |
| **Notable Research** | Code Graph Model (CGM) -- accepted at NeurIPS 2025 |

CGM is a graph-based LLM framework for repository-level software engineering, using a chain of four atomic nodes (Rewriter, Retriever, Reranker, Reader) to navigate complex codebases.

#### Ling-1T (October 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Ant Group |
| **Release** | October 2025 |
| **License** | Open-source |
| **Architecture** | MoE with Evolutionary Chain-of-Thought (Evo-CoT) |
| **Total Parameters** | 1 trillion |
| **Active Parameters** | ~50B per token |
| **Training Data** | 20T+ reasoning-dense tokens |
| **Context Window** | 128K tokens |
| **LiveCodeBench** | Leading among 1T models (surpasses Kimi K2 at 53.7%, GPT-5 at 44.7%) |
| **MMLU** | 91.76% (surpasses GPT-5, Claude 4.5 Sonnet, DeepSeek V3.1) |
| **AIME 2025** | 70.42% |
| **Availability** | HuggingFace (inclusionAI/Ling-1T) |

Ling-1T is the first flagship non-thinking model in the Ling 2.0 series, part of a family comprising Ling (non-thinking), Ring (thinking), and Ming (multimodal).

---

### SenseTime (SenseNova)

SenseTime, originally a computer vision company, has expanded into general AI.

#### SenseNova V6 (April 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | SenseTime |
| **Release** | April 2025 |
| **Architecture** | Hybrid MoE |
| **Key Strengths** | Multimodal reasoning, long CoT, mathematics, coding |
| **Benchmarks** | Multimodal reasoning ranked #1 in China (vs GPT-o1) |
| **Cost** | Lowest training and reasoning costs in Chinese industry |
| **Notable** | First Chinese model supporting 10-minute mid-to-long video analysis |

SenseNova is stronger in multimodal and vision tasks than in pure coding. SenseTime reported record revenue of over RMB 5 billion in 2025, with EBITDA turning positive in H2.

---

### Baichuan

Baichuan Intelligence, founded by former Sogou CEO Wang Xiaochuan, has pivoted primarily toward medical AI.

#### Baichuan-M3-235B (2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Baichuan Intelligence |
| **Architecture** | MoE (235B total) |
| **Primary Focus** | Medical AI, with general coding as secondary |
| **Coding Benchmarks** | Competitive at its scale on HumanEval/MBPP, but behind dedicated coding models |
| **Availability** | HuggingFace |

Baichuan models support coding tasks but are not specialized for them. The company's primary differentiation is in medical AI (Baichuan-M1, M2, M3 series).

---

### Shanghai AI Lab (InternLM)

Shanghai AI Laboratory is a national-level research institution.

#### InternLM3 (January 2025)

| Attribute | Details |
|-----------|---------|
| **Creator** | Shanghai AI Lab |
| **Release** | January 2025 |
| **License** | Open-source |
| **Size** | 8B (InternLM3-8B-Instruct) |
| **Training Data** | 4T tokens |
| **Key Innovation** | Integrates conversational capabilities with deep thinking in single model |
| **Efficiency** | Cuts training costs by 75%+ vs comparable models |

InternLM3 achieves state-of-the-art performance in knowledge understanding, reading comprehension, mathematics, and coding at its scale. However, InternLM does not have a dedicated "Code" variant -- coding is integrated into the general-purpose model.

---

## 2. IDE & Coding Tools

### Tongyi Lingma (Alibaba)

| Attribute | Details |
|-----------|---------|
| **Creator** | Alibaba Cloud |
| **Launched** | October 2023 |
| **Model Backend** | Qwen series |
| **IDE Support** | VS Code, JetBrains (IntelliJ, PyCharm, GoLand, WebStorm, etc.) |
| **Pricing** | Free tier available; enterprise plans |
| **Downloads** | 2M+ shortly after launch |
| **Market Share** | 12.9% in China (vs GitHub Copilot's 64.5%) |
| **Employee ID** | AI001 at Alibaba -- the company's first "AI employee" |

**Key Features:**
- Line-level and method-level code generation
- Natural language to code translation
- Multi-file simultaneous modification
- Unit test generation, code comments, code explanation
- Cross-file context awareness
- Intent understanding and reflective iteration
- AI-assisted code search across documentation

Alibaba projects Tongyi Lingma will write at least 20% of the company's code going forward.

---

### Qwen Code CLI (Alibaba)

| Attribute | Details |
|-----------|---------|
| **Creator** | Alibaba / Qwen Team |
| **Launched** | 2025, v0.5.0 in late 2025 |
| **License** | Open-source |
| **Model Backend** | Qwen3-Coder (model-agnostic, supports others) |
| **Interface** | Terminal CLI + VS Code plugin |
| **SWE-bench** | 69.6% |
| **GitHub** | github.com/QwenLM/qwen-code |

A direct competitor to Claude Code and Gemini CLI (it's a Gemini CLI fork). Key v0.5.0 features include:
- 4 concurrent instances in a single terminal
- VS Code plugin with sidebar integration
- TypeScript SDK for programmatic integration
- Workflow automation (PR handling, rebases, formatting)
- Enhanced parser optimized for Qwen-Coder structured outputs

---

### Kimi Code CLI (Moonshot)

| Attribute | Details |
|-----------|---------|
| **Creator** | Moonshot AI |
| **Launched** | January 2026 (with K2.5) |
| **License** | Apache 2.0 |
| **Model Backend** | Kimi K2.5 |
| **Interface** | Terminal CLI |
| **GitHub Stars** | 6,400+ (as of Feb 2026) |
| **IDE Integration** | VS Code, Cursor, Zed |
| **MCP Support** | Yes |

An autonomous coding agent that can analyze repos, propose plans, execute shell commands, and iterate. Supports file read/edit, command execution, code search, web content fetching, and multi-step action planning.

---

### CodeGeeX (Zhipu AI)

| Attribute | Details |
|-----------|---------|
| **Creator** | Zhipu AI / Tsinghua KEG Lab |
| **Model** | CodeGeeX4-ALL-9B (latest, based on GLM-4-9B) |
| **License** | Free for individual use |
| **IDE Support** | VS Code, JetBrains (all IDEs) |
| **HumanEval** | 82.3% |
| **MBPP** | 75.7% |
| **Context Window** | 128K tokens |

**Key Features:**
- Code completion, explanation, fixes, translation
- Code interpreter, web search, function calling
- Repository-level Q&A
- Long-text context memory, cross-file analysis
- Local mode support
- NL2SQL capabilities
- Automatic README generation

CodeGeeX is completely free for individuals -- no token limits, no premium tier required.

---

### Trae IDE (ByteDance)

| Attribute | Details |
|-----------|---------|
| **Creator** | ByteDance |
| **Launched** | January 20, 2025 |
| **Formerly** | MarsCode |
| **Base** | VS Code fork |
| **Model Backend** | Doubao (ByteDance) + Claude 4, GPT-4o, DeepSeek R1 |
| **Pricing** | Free tier: 5,000 auto-completions/month + premium models; Pro: $10/month |
| **Interface** | Full IDE (desktop app) |

**Key Features:**
- **Builder Mode**: Generates full-stack apps from natural language prompts
- **Chat Mode**: Step-by-step code analysis, debugging, suggestions
- Multimodal input (images for UI generation)
- Access to premium models (Claude 4, GPT-4o, DeepSeek R1)
- VS Code extension compatibility
- Strong Chinese language support (native Mandarin interface)

**Privacy Concerns**: Personal data retained for 5 years after account closure. Extensive telemetry collection with no opt-out. ByteDance's Unit221B blog exposed the data collection system in detail.

**MarsCode Agent** (the research arm) fixed 39.33% of real software bugs on SWE-bench Lite.

---

### Baidu Comate

| Attribute | Details |
|-----------|---------|
| **Creator** | Baidu |
| **Model Backend** | ERNIE (Wenxin) large models |
| **IDE Support** | VS Code, JetBrains (all IDEs), Xcode, Visual Studio |
| **Adoption** | 10M+ developers; 43-45% of new code at Baidu is AI-generated |
| **Pricing** | Free tier + enterprise plans |
| **Enterprise Partners** | ~200 organizations testing Comate X |

**Comate 3.5S Features:**
- 5 specialized agents: code Q&A, coding, unit testing, debugging, security
- **Zulu Agent**: Autonomous task decomposition and decision-making
- Design-to-code conversion (F2C)
- Multi-agent collaboration (agents autonomously coordinate)
- MCP integration for team knowledge sharing

**Comate AI IDE** is the industry's first multimodal, multi-agent collaborative AI IDE, putting Baidu in direct competition with GitHub Copilot and Cognition's Devin.

---

### Tencent CodeBuddy

| Attribute | Details |
|-----------|---------|
| **Creator** | Tencent Cloud |
| **Model Backend** | Hunyuan foundation model (Yuanbao Code) |
| **Launched** | Mid-2025 |
| **IDE Support** | Standalone desktop app, VS Code, JetBrains |
| **Adoption** | 85% of Tencent engineers use daily; 50%+ of Tencent programmers |
| **Productivity Gain** | 40% reported improvement |
| **Interface** | Mandarin and English |
| **Availability** | International versions available |

Features conversation-to-code workflows, allowing non-technical users to build applications via natural language. Tencent's overseas client base doubled year-over-year.

---

### Fitten Code

| Attribute | Details |
|-----------|---------|
| **Creator** | Fitten Tech (Tsinghua PhD team) |
| **Pricing** | Free |
| **IDE Support** | VS Code, JetBrains, Vim, Neovim |
| **Languages** | 80+ programming languages |
| **GitHub** | fittencode.nvim (Neovim), fittencode.vim (Vim) |

Features real-time code completion, generation, comment generation, editing, explanation, test generation, and error detection. Represents the indie/academic tier of China's AI coding ecosystem -- built by researchers, offered free.

---

### DevChat (Merico)

| Attribute | Details |
|-----------|---------|
| **Creator** | Merico |
| **IDE Support** | VS Code, JetBrains |
| **Interface** | Chat panel within IDE |
| **Backend** | OpenAI-compatible (routes to various LLMs) |

Open-source tool for prompt-driven code and documentation generation. Supports smart completion, error correction, and code specification checking. Less actively developed in 2025-2026 compared to competitors.

---

## 3. Benchmarks Comparison Table

### Coding Benchmarks: Chinese vs. Western Models (March 2026)

| Model | Origin | HumanEval | SWE-bench Verified | LiveCodeBench | AIME 2025 | Architecture |
|-------|--------|-----------|---------------------|---------------|-----------|--------------|
| **MiniMax M2.5** | China | 89.6% | **80.2%** | -- | -- | 230B MoE (10B active) |
| **Claude Opus 4.6** | US | ~92% | 80.8% | -- | -- | Dense (proprietary) |
| **Kimi K2.5** | China | ~99% | 76.8% | 85.0% | 96.1% | 1T MoE (32B active) |
| **GLM-4.7** | China | 94.2% | 73.8% | 84.9% | 95.7% | 355B MoE (32B active) |
| **Qwen3-Coder-Next** | China | -- | 70.6% | -- | -- | 80B MoE (3B active) |
| **Gemini 3.1 Pro** | US | 93.0% | 78.0% | 81.3% | -- | MoE (proprietary) |
| **DeepSeek V3.2-Speciale** | China | -- | -- | -- | 96.0% | 671B MoE (37B active) |
| **Qwen2.5-Coder-32B** | China | 92.7% | -- | 51.2% | -- | 32B Dense |
| **GPT-5** | US | -- | -- | -- | 94.6% | Proprietary |
| **Ling-1T** | China | -- | -- | Leading (1T class) | 70.4% | 1T MoE (50B active) |
| **Yi-Coder-9B** | China | 85.4% | -- | 23.4% | -- | 9B Dense |
| **ERNIE 4.5** | China | >90% | -- | Below leaders | -- | 424B MoE |

**Key Observations:**
1. **SWE-bench Verified** (the gold standard for real-world coding): Chinese models hold 3 of the top 5 spots (MiniMax M2.5, Kimi K2.5, GLM-4.7).
2. **HumanEval** is saturating -- most frontier models score >90%, making it less discriminating.
3. **Multi-SWE-Bench** (multilingual): MiniMax M2.5 leads at 51.3%, ahead of Claude Opus 4.6.
4. **Cost-adjusted performance**: Chinese models deliver comparable results at 10-30x lower cost.

---

## 4. Unique Strengths of Chinese Models

### 4.1 Training Efficiency & Cost

Chinese labs have pioneered techniques that fundamentally reduce training and inference costs:

- **DeepSeek's MLA**: 93.3% reduction in KV-cache memory
- **FP8 Mixed Precision**: First validated at trillion-parameter scale by DeepSeek
- **MiniMax M2.5**: Frontier performance at 1/20th the cost of Western alternatives
- **Qwen3-Coder-Next**: Only 3B active parameters deliver 70.6% SWE-bench
- **DeepSeek V3**: Trained for $5.6M in GPU compute vs. GPT-4's estimated $50-100M

This efficiency was partly born of necessity (US export controls limiting access to top-tier GPUs), but has become a genuine competitive advantage.

### 4.2 Open-Source Leadership

As of late 2025, four of the top five open-source models globally come from Chinese labs (MiniMax, Alibaba, DeepSeek, Z.ai). Key stats:

- Qwen has 113,000+ derivative models on HuggingFace (most of any model family)
- DeepSeek models are MIT-licensed with full commercial use rights
- Kimi K2.5 is open-weight under Modified MIT
- MiniMax M2.5, GLM-4.7, and ERNIE 4.5 are all open-source

### 4.3 MoE Architecture Innovation

Chinese labs have pushed MoE architecture further than Western counterparts:

| Model | Total Params | Active Params | Ratio |
|-------|-------------|---------------|-------|
| Qwen3-Coder-Next | 80B | 3B | 26.7:1 |
| MiniMax M2.5 | 230B | 10B | 23:1 |
| DeepSeek V3 | 671B | 37B | 18:1 |
| Kimi K2.5 | 1T | 32B | 31.25:1 |
| Ling-1T | 1T | 50B | 20:1 |

Higher sparsity ratios mean more knowledge packed into fewer active compute cycles -- a direct response to compute constraints.

### 4.4 Multilingual & Chinese-Language Superiority

Chinese models naturally excel at:
- **Mandarin code comments and documentation**
- **Chinese variable names and identifiers** (full Unicode support)
- **Chinese-language error messages and debugging**
- **Bilingual codebases** (mixed Chinese/English)
- **Chinese technical documentation understanding**

This matters for the enormous domestic Chinese developer market (estimated at 7-10 million professional developers).

### 4.5 Agentic Coding Innovation

Several unique agentic features emerged from Chinese labs:

- **Kimi K2.5's Agent Swarm**: 100 agents coordinating via PARL, 4.5x speedup
- **Baidu Comate's Zulu**: Autonomous multi-agent task decomposition
- **MiniMax M2.5's Architect Mode**: Plans features and structure before writing code
- **DeepSeek V3.2's Thinking-in-Tool-Use**: First to integrate reasoning into tool calls

### 4.6 Vertical Integration

Chinese tech giants integrate coding AI across their entire stack:

| Company | Model | IDE Tool | CLI Agent | Cloud Platform |
|---------|-------|----------|-----------|----------------|
| Alibaba | Qwen3-Coder | Tongyi Lingma | Qwen Code | Alibaba Cloud |
| Baidu | ERNIE | Comate | -- | Baidu Cloud |
| Tencent | Hunyuan | CodeBuddy | -- | Tencent Cloud |
| ByteDance | Doubao | Trae IDE | -- | Volcano Engine |
| Zhipu AI | GLM-4.7 | CodeGeeX | -- | Z.ai Platform |
| Moonshot | Kimi K2.5 | -- | Kimi Code | Kimi API |

---

## 5. Access & Availability Outside China

### Freely Available Globally

| Model/Tool | Access Method | Notes |
|------------|--------------|-------|
| DeepSeek (all models) | HuggingFace, API, Ollama | MIT License, no restrictions |
| Qwen2.5-Coder (all sizes) | HuggingFace, ModelScope, Ollama | Apache 2.0 |
| Qwen3-Coder / Qwen3-Coder-Next | HuggingFace, Ollama | Open-weight |
| Yi-Coder | HuggingFace, Ollama | Apache 2.0 |
| Kimi K2/K2.5 | HuggingFace, NVIDIA NIM, API | Modified MIT |
| GLM-4.7 | HuggingFace, API | Open-weight |
| MiniMax M2/M2.5 | HuggingFace, API, Ollama | Open-source |
| ERNIE 4.5 | HuggingFace | Apache 2.0 |
| Ling-1T | HuggingFace (inclusionAI) | Open-source |
| CodeGeeX plugin | VS Code / JetBrains Marketplace | Free |
| Trae IDE | trae.ai | Free tier globally |
| Fitten Code | VS Code / JetBrains / Vim Marketplace | Free |

### Restricted or China-Focused

| Tool | Access | Notes |
|------|--------|-------|
| Tongyi Lingma | Alibaba Cloud account needed | Available internationally via Alibaba Cloud |
| Baidu Comate | Primarily China-focused | JetBrains plugin available globally |
| Tencent CodeBuddy | International version launched | Expanding globally |
| Qwen Code CLI | Open-source (GitHub) | Usable anywhere |
| Kimi Code CLI | Open-source (GitHub) | Usable anywhere |

### Third-Party Inference Providers

Chinese models are available through global inference providers at competitive rates:

- **SiliconFlow**: All-in-one Chinese AI inference platform (16M+ developers, 70K+ models)
- **Together AI**: Hosts Qwen3-Coder, DeepSeek, and others
- **OpenRouter**: DeepSeek V3.2, Kimi K2.5, GLM-4.7
- **NVIDIA NIM**: Kimi K2.5, MiniMax M2.5
- **Featherless**: Kimi K2.5
- **Ollama**: Most open-source Chinese models available for local inference

### Integration with Western Developer Tools

Chinese models work with major Western development tools:

| Tool | Chinese Model Support |
|------|-----------------------|
| **Cursor** | Built Composer 2 on Kimi + DeepSeek + Qwen foundations |
| **Windsurf** | Core model from Z.ai (Zhipu AI) |
| **Continue.dev** | DeepSeek, Qwen via OpenAI-compatible API |
| **Aider** | DeepSeek via API; Qwen via local/API |
| **VS Code** | CodeGeeX, Fitten Code, Tongyi Lingma, Trae plugins |
| **JetBrains** | CodeGeeX, Fitten Code, Tongyi Lingma, Comate plugins |
| **Claude Code / Gemini CLI** | Can use DeepSeek, Qwen via API configuration |

---

## 6. Chinese Coding Benchmarks & Communities

### Benchmarks

**CRUXEval-X**: An expanded multilingual code reasoning benchmark covering 19 programming languages. Developed as an extension of CRUXEval with focus on cross-lingual capabilities. Yi-Coder-9B was the first open-source model to surpass 50% on CRUXEval-O.

**HumanEval Gap Closure**: At the end of 2023, the performance gap on HumanEval between US and Chinese models was 31.6 percentage points. By end of 2024, this had narrowed to just 3.7 points. As of 2026, the gap has essentially vanished -- Chinese models now lead on some coding benchmarks.

**Benchmark Saturation**: Traditional benchmarks like HumanEval are saturating (most frontier models >90%). The field is migrating to:
- **SWE-bench Verified**: Real-world GitHub issue resolution
- **Multi-SWE-Bench**: Multilingual real-world coding
- **LiveCodeBench**: Live competitive programming
- **BigCodeBench**: Only 35.5% AI success rate vs. 97% human baseline

### Open-Source Communities & Platforms

**ModelScope (Alibaba)**:
- China's largest AI open-source platform
- 70,000+ open-source models
- 16M+ developers globally
- Launched November 2022
- Functions as "Model-as-a-Service" (MaaS)
- Chinese equivalent of HuggingFace

**Gitee**:
- MIIT-backed domestic alternative to GitHub
- Important for data sovereignty compliance
- China's State Council proposed counting open-source contributions on Gitee toward university academic credit

**HuggingFace Presence**:
- Chinese models are extensively published on HuggingFace
- Qwen family: 113K+ derivative models (most of any family)
- DeepSeek, Kimi, MiniMax, GLM, ERNIE, Ling -- all have official HuggingFace organizations

---

## 7. Regulatory Considerations

### Data Sovereignty

China is pushing for "algorithmic sovereignty" -- complete control over computing infrastructure by 2027. Key implications for coding tools:

- Chinese companies must store code processed by AI within China
- Foreign AI coding tools used in Chinese enterprises face data residency requirements
- Domestic alternatives (Tongyi Lingma, Comate, CodeBuddy) are preferred for government and state-owned enterprise contracts

### US Export Controls Impact

The Bureau of Industry and Security (BIS) maintains aggressive restrictions on GPU and accelerator exports to China:

- **Hardware restrictions**: Advanced GPUs (H100, H200) cannot be exported to China. DeepSeek V3 was trained on H800s (less restricted variant), but even these face increasing restrictions.
- **Chinese response**: "Using software to supplement hardware" -- algorithmic innovation to overcome material constraints. DeepSeek's MLA, FP8 training, and sparse attention are direct results.
- **Domestic chip development**: DeepSeek V3.1 was explicitly optimized for domestic AI accelerators (Huawei Ascend, etc.)
- **Impact on researchers**: Sharing controlled source code with foreign nationals (even within the US) can trigger licensing requirements. BIS penalties regularly exceed $1 million.

### Open-Source as Strategic Policy

China has embraced open-source AI as national strategy:
- State Council policies encourage open-source contributions
- Universities may count open-source work toward academic credit
- Open-source models enable global adoption without direct technology transfer issues
- MIT and Apache 2.0 licenses dominate Chinese model releases

### Implications for Western Developers

1. **All major Chinese coding models are freely available** for download and local use -- no Chinese account or residency required
2. **API access** is available through both Chinese platforms and Western providers (OpenRouter, Together AI, SiliconFlow)
3. **Privacy considerations**: Using Chinese-hosted APIs means data transits Chinese servers. For sensitive code, prefer local inference or Western-hosted providers
4. **Cursor and Windsurf already use Chinese models** as backbone technology -- this is not hypothetical, it's reality

---

## Summary

The Chinese AI coding ecosystem in March 2026 is not a secondary player catching up to Western leaders -- it is, in several dimensions, the global leader:

- **SWE-bench Verified**: MiniMax M2.5 (80.2%) rivals Claude Opus 4.6 (80.8%). Three of the top five models are Chinese.
- **Cost efficiency**: DeepSeek is 30x cheaper than OpenAI; Qwen is 10x cheaper. MiniMax delivers frontier performance at 1/20th the cost.
- **Open-source dominance**: Four of the top five open-source models are Chinese. Qwen has more HuggingFace derivatives than any other model family.
- **Architectural innovation**: MLA, FP8 training, DeepSeek Sparse Attention, Agent Swarms, Lightning Attention -- many of the most impactful recent innovations in efficient AI come from Chinese labs.
- **IDE tools**: Every major Chinese tech company has a competitive coding assistant, with several (CodeGeeX, Trae) available free globally.
- **Western adoption**: Cursor and Windsurf both build on Chinese model foundations. This is the strongest possible validation.

The competitive pressure from Chinese AI labs has materially benefited developers worldwide through lower costs, more open-source options, and faster innovation cycles. Any assessment of the AI coding tool landscape that ignores Chinese contributions is fundamentally incomplete.

---

*Last updated: March 25, 2026*
