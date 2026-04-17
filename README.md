# 🚀 LLMs and Generative AI Resources Repository

A comprehensive, well-structured collection of resources, tools, and frameworks for Large Language Models and Generative AI applications. This repository serves as a central hub for developers, researchers, and practitioners working with modern AI systems.

## 🗺️ Navigation

### 🤖 Models & Capabilities
Explore the latest LLMs, vision models, and embedding systems.

- **[Text Models](docs/models/text-models.md)** - Proprietary (GPT-4o, Claude 4.6, Gemini 2.5), open source (Llama 3.3, Qwen 2.5, DeepSeek R1), specialized models
- **[Vision Models](docs/models/vision-models.md)** - Vision-language models, image generation (Stable Diffusion 3.5, DALL-E 3, Flux), video generation (Sora, Runway Gen-3)
- **[Embeddings](docs/models/embeddings.md)** - SOTA embedding models (MTEB leaderboard), rerankers, specialized retrieval

### 🏗️ Infrastructure & Deployment
Build and deploy AI systems at scale.

- **[Vector Databases](docs/infrastructure/vector-databases.md)** - FAISS, Pinecone Serverless v2, Qdrant, Milvus, Chroma, specialized retrieval (ColBERTv3, SPLADE)
- **[Graph Databases](docs/infrastructure/graph-databases.md)** - Neo4j, ArangoDB, TigerGraph, knowledge graphs, graph analytics
- **[On-Premise Deployment](docs/infrastructure/on-premise-deployment.md)** - vLLM, llama.cpp, TensorRT-LLM, quantization methods (GGUF, AWQ, FP8)

### 🤝 Frameworks & Systems
Orchestrate complex AI workflows and agentic systems.

- **[Agentic Systems](docs/frameworks/agentic-systems.md)** - Model Context Protocol (MCP), AutoGen, CrewAI, LangGraph, MetaGPT, agent patterns
- **[General Frameworks](docs/frameworks/general-frameworks.md)** - LangChain, Haystack, Semantic Kernel, LlamaIndex

### 📊 Evaluation & Quality
Measure and improve AI system performance.

- **[Leaderboards](docs/evaluation/leaderboards.md)** - Chatbot Arena, BFCL (tool calling), MMMU (vision), GPQA, MATH, reasoning benchmarks
- **[Evaluation Frameworks](docs/evaluation/evaluation-frameworks.md)** - RAGAS (RAG evaluation), DeepEval, TruLens, PromptFoo, LLM-as-judge patterns

### 🔍 Operations & Monitoring
Ensure reliability, observability, and production readiness.

- **[Observability](docs/operations/observability.md)** - OpenTelemetry, LangFuse, LangSmith, Weights & Biases, Arize AI, Phoenix
- **[Production Checklist](docs/operations/production-checklist.md)** - Day one requirements, deployment strategies, best practices

### 🛠️ Development Tools
Essential tools for building and securing AI applications.

- **[Prompt Engineering](docs/development/prompt-engineering.md)** - Chain-of-thought, ReAct, tree-of-thoughts, techniques & tools
- **[Fine-tuning](docs/development/fine-tuning.md)** - Axolotl, Unsloth, PEFT (LoRA/QLoRA), DeepSpeed, Megatron-LM
- **[Guardrails & Safety](docs/development/guardrails.md)** - Guardrails AI, NeMo Guardrails, LLM Guard, content safety
- **[Data Processing](docs/development/data-processing.md)** - spaCy, Pydantic, synthetic data generation

### 📖 Comprehensive Guides
Step-by-step guides for common use cases and patterns.

- **[Getting Started](docs/guides/getting-started.md)** - Choose your use case, select deployment strategy, implementation roadmap
- **[Trends & Future (2026)](docs/guides/trends-2026.md)** - Current state, emerging directions, technology shifts

---

## 🚀 Quick Start

**New to LLMs?**  
→ Start with the [Getting Started Guide](docs/guides/getting-started.md)

**Building RAG Applications?**  
→ [Embeddings](docs/models/embeddings.md) + [Vector Databases](docs/infrastructure/vector-databases.md) + [Evaluation Frameworks](docs/evaluation/evaluation-frameworks.md)

**Building Agentic Systems?**  
→ [Agentic Systems](docs/frameworks/agentic-systems.md) + [Text Models](docs/models/text-models.md) + [Observability](docs/operations/observability.md)

**Deploying Locally?**  
→ [On-Premise Deployment](docs/infrastructure/on-premise-deployment.md) + [Text Models](docs/models/text-models.md)

**Going to Production?**  
→ [Production Checklist](docs/operations/production-checklist.md) + [Observability](docs/operations/observability.md) + [Guardrails](docs/development/guardrails.md)

---

## 📊 Repository Statistics

- **10 comprehensive categories** covering the entire LLM ecosystem
- **200+ tools & frameworks** with version information and performance data
- **50+ models** documented (proprietary and open source)
- **12+ vector databases** from embedded to distributed scale
- **20+ benchmarks** and evaluation frameworks
- **Last Major Update**: April 18, 2026

---

## 🤝 Contributing

This repository is designed to be a living document. Contributions are welcome for:

- Adding new tools and frameworks
- Updating benchmark results and model versions
- Improving categorization and organization
- Adding implementation examples and guides
- Sharing production lessons learned

**How to Contribute:**
1. Check the relevant section file in `docs/`
2. Submit updates with clear descriptions
3. Include links to official sources
4. Follow the existing markdown formatting

---

## 📈 Key Trends (April 2026)

- **Reasoning Breakthrough**: o3, DeepSeek R1 achieving significant advances
- **Multimodal Native**: Vision, audio, video integrated from ground up
- **Open Source Competitive**: DeepSeek-V3, Qwen 2.5 Max matching proprietary models
- **MoE Architecture**: Efficient large models (671B params, 37B active)
- **Agentic Systems**: Computer use, tool calling in production
- **MCP Adoption**: Model Context Protocol standardizing LLM-tool integration

See [Trends & Future (2026)](docs/guides/trends-2026.md) for detailed analysis.

---

## 🌐 Network Relationships

This repository documents relationships between components:
- How models depend on inference servers
- How vector databases integrate with agentic systems
- How observability tools track system performance
- How benchmarks assess different capabilities

---

## ⚠️ Important Notes

**Rapid Evolution**: The LLM ecosystem evolves rapidly. Model versions, benchmarks, and best practices change frequently. Always verify current versions, pricing, and capabilities before production implementation.

**Real-Time Data**: For live leaderboard data and current benchmarks, visit the linked sources directly as standings change frequently.

**Maintenance**: This repository is actively maintained with quarterly major updates and monthly patches for critical changes.

---

## 📝 License

This repository is licensed under the terms specified in [LICENSE](LICENSE).

Built with ❤️ for the LLM & GenAI community

**Last Updated**: April 18, 2026
