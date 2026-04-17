# Leaderboards & Benchmarks

[Home](../../README.md) > [Evaluation](../) > Leaderboards & Benchmarks

> Comprehensive overview of LLM benchmarks, leaderboards, and evaluation metrics across different capabilities including tool calling, vision, reasoning, and general performance.

*Last Updated: April 18, 2026*

## Table of Contents
- [Tool Calling & Function Use](#tool-calling--function-use)
- [Vision Benchmarks](#vision-benchmarks)
- [General LLM Leaderboards](#general-llm-leaderboards)
- [Reasoning & Math](#reasoning--math)
- [Specialized Benchmarks](#specialized-benchmarks)

## Tool Calling & Function Use

### Berkeley Function Calling Leaderboard (BFCL)

| Aspect | Details |
|--------|---------|
| **Focus** | Multi-step tool use, parallel calling, error recovery |
| **Top Performers** | Claude 3.5 Sonnet, GPT-4o, Gemini Pro |
| **Key Metrics** | Accuracy, parallel execution, error handling |
| **Link** | [Website](https://gorilla.cs.berkeley.edu/leaderboard.html) |

The BFCL evaluates models on their ability to:
- Call functions with correct parameters
- Handle multi-step tool workflows
- Execute parallel function calls
- Recover from errors gracefully
- Parse and validate function outputs

### ToolBench

| Aspect | Details |
|--------|---------|
| **Focus** | 16K+ real-world REST APIs |
| **Top Performers** | Command-R+, GPT-4 Turbo, Mixtral |
| **Key Features** | Real-world API complexity, diverse domains |
| **Link** | [GitHub](https://github.com/OpenBMB/ToolBench) |

ToolBench tests models on:
- Real-world REST API interactions
- Complex API parameter handling
- Multi-API workflow composition
- Authentication and error handling

## Vision Benchmarks

### MMMU (Massive Multi-discipline Multimodal Understanding)

| Benchmark | Details |
|-----------|---------|
| **Scope** | College-level multimodal understanding |
| **Questions** | 11,500+ expert-annotated questions |
| **Disciplines** | Art, business, science, health, engineering |
| **Top Performers** | GPT-4o, Gemini 2.0 Pro, Claude 4.5 Sonnet |

MMMU evaluates:
- Multi-image reasoning
- Chart and diagram interpretation
- Scientific visualization understanding
- Cross-modal knowledge integration

### MMBench

| Benchmark | Details |
|-----------|---------|
| **Methodology** | CircularEval for robust evaluation |
| **Capabilities** | 20+ vision-language abilities |
| **Performance** | 85%+ on top models |
| **Focus** | Comprehensive VLM assessment |

MMBench tests:
- Object recognition and localization
- OCR and text understanding
- Spatial reasoning
- Attribute recognition
- Social intelligence

### MMBench-Video

| Benchmark | Details |
|-----------|---------|
| **Focus** | Video understanding and temporal reasoning |
| **Top Performers** | Gemini 2.0 Pro, GPT-4o |
| **Capabilities** | Multi-frame analysis, temporal relationships |

Evaluates:
- Temporal reasoning across video frames
- Action recognition and prediction
- Event understanding
- Long-form video analysis

## General LLM Leaderboards

### Chatbot Arena (LMSYS)

| Aspect | Details |
|--------|---------|
| **Methodology** | Human preference, ELO rankings |
| **Evaluation** | Head-to-head model comparisons |
| **Top Models (April 2026)** | Claude 4.6 Opus, GPT-4o, Gemini 2.5 Pro |
| **Strengths** | Real-world user preferences |

**Key Features:**
- Crowdsourced evaluations
- Blind A/B testing
- ELO rating system
- Regular updates with new models
- Category-specific rankings (coding, creative writing, etc.)

### Open LLM Leaderboard

| Benchmark Component | Description |
|-------------------|-------------|
| **IFEval** | Instruction following accuracy |
| **BBH (Big-Bench Hard)** | Challenging reasoning tasks |
| **MATH** | Mathematical problem solving |
| **GPQA** | Graduate-level science questions |
| **MUSR** | Multi-step reasoning |

**Top Models (April 2026):**
- Llama 3.3 70B
- Qwen 2.5 Max
- DeepSeek-V3

**Strengths:**
- Focused on open-source models
- Reproducible evaluation
- Comprehensive capability coverage

### HELM (Holistic Evaluation of Language Models)

| Dimension | Focus |
|-----------|-------|
| **Accuracy** | Task performance across domains |
| **Calibration** | Confidence alignment with correctness |
| **Robustness** | Performance under perturbations |
| **Fairness** | Bias and representation analysis |
| **Efficiency** | Computational and economic costs |

**Evaluation Approach:**
- Multi-dimensional assessment
- Stanford-led research benchmark
- Transparency and reproducibility
- Comprehensive scenario coverage

### Artificial Analysis

| Aspect | Details |
|--------|---------|
| **Focus** | Performance, pricing, quality across providers |
| **Methodology** | Real-time API testing |
| **Metrics** | Latency, throughput, cost per token, quality |
| **Value** | Practical deployment decision-making |

**Key Metrics Tracked:**
- Time to first token (TTFT)
- Tokens per second
- Cost per million tokens
- Quality scores across benchmarks

## Reasoning & Math

### GPQA Diamond

| Aspect | Details |
|--------|---------|
| **Focus** | Graduate-level science questions (adversarial) |
| **Disciplines** | Physics, chemistry, biology |
| **Human Expert Baseline** | 34% accuracy |
| **SOTA Performance** | 70%+ (o3, DeepSeek R1) |

**Key Characteristics:**
- Expert-written questions
- Adversarial design
- Multiple choice format
- Requires deep domain knowledge

### MATH

| Level | Description | Difficulty |
|-------|-------------|-----------|
| **1-2** | Basic algebra and arithmetic | Introductory |
| **3-4** | Intermediate problem solving | Advanced high school |
| **5** | Competition-level mathematics | IMO-level |

**SOTA Performance:**
- 90%+ on MATH-500 benchmark
- Top models: o3, DeepSeek R1, Claude 4.6 Opus

**Evaluation Focus:**
- Step-by-step reasoning
- Formula manipulation
- Proof construction
- Problem-solving strategies

### GSM8K

| Aspect | Details |
|--------|---------|
| **Focus** | Grade school math word problems |
| **Status** | Largely saturated (95%+ accuracy) |
| **Successor Benchmarks** | GSM-Plus, GSM-Symbolic for harder evaluation |

### MuSR (Multi-Step Reasoning)

| Aspect | Details |
|--------|---------|
| **Focus** | Complex multi-step reasoning tasks |
| **Top Performers** | o3, DeepSeek R1, Claude 4.6 |
| **Capabilities** | Planning, decomposition, logical chains |

**Evaluates:**
- Multi-hop logical reasoning
- Planning and decomposition
- Intermediate step validation
- Error recovery in reasoning chains

### ARC-AGI

| Aspect | Details |
|--------|---------|
| **Focus** | Abstract reasoning challenge |
| **Breakthrough** | o3 showing significant progress |
| **Goal** | Measure general intelligence |

**Key Characteristics:**
- Visual pattern recognition
- Abstract rule learning
- Minimal prior knowledge required
- Tests adaptability and generalization

## Specialized Benchmarks

### Embedding & Retrieval

**MTEB (Massive Text Embedding Benchmark)**
- 56 datasets across 8 tasks
- Classification, clustering, retrieval, semantic similarity
- Top performers: Voyage-3-Large, BGE-v2.5, E5-Mistral-7B

### Code Generation

**HumanEval & MBPP**
- Python code generation from docstrings
- SOTA: 90%+ on HumanEval
- Leading models: DeepSeek-Coder-V2, GPT-4o, Claude Sonnet

**LiveCodeBench**
- Real-world coding challenges
- Updated regularly to prevent memorization
- More challenging than static benchmarks

### Multilingual

**XTREME & XTREME-R**
- Cross-lingual understanding
- 40+ languages
- Translation, QA, classification tasks

## Benchmark Limitations & Best Practices

### Known Issues

1. **Saturation**: GSM8K and other early benchmarks showing ceiling effects
2. **Contamination**: Training data overlap concerns
3. **Narrow Scope**: Single-capability focus missing real-world complexity
4. **Adversarial Robustness**: Models vulnerable to rephrasing

### Best Practices for Evaluation

1. **Use Multiple Benchmarks**: No single benchmark captures all capabilities
2. **Test on Domain Data**: Public benchmarks may not reflect your use case
3. **Monitor Over Time**: Track performance on holdout sets regularly
4. **Combine Automated & Human**: Balance efficiency with real-world validity
5. **Test Robustness**: Evaluate on perturbed inputs and edge cases

## Emerging Benchmarks (2026)

### New Focus Areas

- **Long-Context Understanding**: "Needle in haystack" tests at 1M+ tokens
- **Agentic Capabilities**: Multi-step tool use with real-world APIs
- **Video Understanding**: Temporal reasoning over extended videos
- **Safety & Alignment**: Red-teaming, jailbreak resistance
- **Efficiency**: Performance per dollar, latency-quality tradeoffs

## Related Resources
- [Evaluation Frameworks](./evaluation-frameworks.md) - Tools for testing and benchmarking
- [Text Models](../models/text-models.md) - Models and their capabilities
- [Vision Models](../models/vision-models.md) - Multimodal model performance
- [Observability](../operations/observability.md) - Production monitoring and metrics

---

[🏠 Back to Home](../../README.md)
