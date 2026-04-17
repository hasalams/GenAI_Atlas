# Text Models

[Home](../../README.md) > [Models](../models/) > Text Models

> Comprehensive listing of proprietary, open source, and specialized text generation models. Includes context windows, key features, parameter counts, and use case recommendations.

*Last Updated: April 18, 2026*

## Table of Contents

- [Proprietary Models](#proprietary-models)
- [Open Source Models](#open-source-models)
- [Specialized Models](#specialized-models)
- [Model Selection Guide](#model-selection-guide)
- [Related Resources](#related-resources)

## Proprietary Models

| Provider | Models | Context | Key Features |
|----------|--------|---------|-------------|
| **OpenAI** | GPT-4o, GPT-4o mini, o1, o3 | 128K-200K | Multimodal (vision/audio), advanced reasoning, function calling |
| **Anthropic** | Claude 4.6 Opus, Claude 4.5/4.6 Sonnet, Claude 3.5 Haiku | 200K | Long context, computer use, agentic coding, vision |
| **Google** | Gemini 2.5 Pro, Gemini 2.0 Flash | 1M-2M | Extreme long context, native multimodal, video understanding |
| **xAI** | Grok-2, Grok-2 mini | 128K | Real-time X data, image generation (FLUX) |
| **Cohere** | Command R+, Command R | 128K | RAG optimization, multilingual (10 languages), tool use |

## Open Source Models

| Provider | Models | Parameters | Key Features |
|----------|--------|------------|-------------|
| **Meta** | Llama 3.3 70B, Llama 3.1 405B/70B/8B | 405B, 70B, 8B | Open weights, commercial use, 128K context, tool use |
| **Alibaba** | Qwen 2.5 Max, Qwen 2.5 72B, Qwen 2.5-Coder | 235B+, 72B, 7-32B | Multilingual, reasoning, coding, vision |
| **DeepSeek** | DeepSeek R1, DeepSeek-V3, DeepSeek-Coder-V2 | 671B MoE (37B active) | Advanced reasoning, cost-efficient training, o1-competitive |
| **Mistral** | Mistral Large 2, Mixtral 8x22B | 123B, 141B MoE (39B active) | European, efficiency, multilingual, 64K-128K context |
| **Microsoft** | Phi-4, Phi-3 (Mini/Small/Medium) | 14B, 3.8-14B | Small models, high performance, STEM reasoning |
| **Google** | Gemma 2 27B/9B | 27B, 9B | Efficient architecture, edge-friendly |

## Specialized Models

### Reasoning Models
- **o1, o3, o3-mini** (OpenAI): Advanced chain-of-thought reasoning, graduate-level problem solving
- **DeepSeek R1** (DeepSeek): Open reasoning model, o1-competitive performance
- **QwQ-32B** (Alibaba): Reasoning-focused model

### Code Models
- **DeepSeek-Coder-V2** (236B MoE): State-of-the-art coding capabilities
- **Qwen2.5-Coder** (up to 32B): Strong code generation, 128K context
- **CodeLlama** (Meta): Code-specialized Llama variants
- **StarCoder2** (BigCode): Open coding model

### Math & Science
- **Llemma**: Mathematical reasoning
- **MathLlama**: Math problem solving
- **DeepSeek-Math**: Mathematical capabilities

### Long Context
- **Gemini 2.5 Pro**: 2M tokens
- **Claude 4.x**: 200K tokens
- **GPT-4o**: 128K tokens
- **Llama 3.1/3.3**: 128K tokens

## Model Selection Guide

### **For General Chat & Assistance**
- **Best Quality**: Claude 4.6 Opus, GPT-4o
- **Best Value**: Claude 4.5 Sonnet, GPT-4o mini
- **Open Source**: Llama 3.3 70B, Qwen 2.5 72B

### **For Long Documents**
- Gemini 2.5 Pro (2M tokens)
- Claude 4.x (200K tokens)

### **For Reasoning & Problem Solving**
- o3, o1 (OpenAI)
- DeepSeek R1 (open source)
- Claude 4.6 Opus

### **For Code Generation**
- DeepSeek-Coder-V2
- Claude 4.5 Sonnet
- Qwen2.5-Coder

### **For Multimodal Tasks**
- GPT-4o (vision + audio)
- Claude 4.5/4.6 Sonnet (vision + computer use)
- Gemini 2.0 Pro (vision + video)

### **For Local Deployment**
- Llama 3.3 70B
- Qwen 2.5 72B
- Phi-4 14B (resource-constrained)

## Related Resources

- [Vision Models](vision-models.md) - For multimodal capabilities beyond text
- [Embeddings](embeddings.md) - Text representation models for RAG
- [On-Premise Deployment](../infrastructure/on-premise-deployment.md) - How to deploy these models locally
- [Getting Started Guide](../guides/getting-started.md) - Model selection for your use case

---

[🏠 Back to Home](../../README.md)
