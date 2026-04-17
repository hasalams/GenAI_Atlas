# Migration Guide: Monolithic to Modular Structure

This document helps you find content that moved from the old single-file README.md to the new modular structure (April 18, 2026 restructure).

## Quick Reference: Where Did Content Move?

| Old README Section | New Location |
|-------------------|--------------|
| Text Models | [docs/models/text-models.md](docs/models/text-models.md) |
| Vision Models | [docs/models/vision-models.md](docs/models/vision-models.md) |
| Vector Databases | [docs/infrastructure/vector-databases.md](docs/infrastructure/vector-databases.md) |
| Graph Databases | [docs/infrastructure/graph-databases.md](docs/infrastructure/graph-databases.md) |
| Leaderboards & Benchmarks | [docs/evaluation/leaderboards.md](docs/evaluation/leaderboards.md) |
| On-Premise Deployment | [docs/infrastructure/on-premise-deployment.md](docs/infrastructure/on-premise-deployment.md) |
| Agentic Systems | [docs/frameworks/agentic-systems.md](docs/frameworks/agentic-systems.md) |
| Observability & Monitoring | [docs/operations/observability.md](docs/operations/observability.md) |
| Evaluation & Testing | [docs/evaluation/evaluation-frameworks.md](docs/evaluation/evaluation-frameworks.md) |
| Embeddings (from Additional) | [docs/models/embeddings.md](docs/models/embeddings.md) |
| Prompt Engineering | [docs/development/prompt-engineering.md](docs/development/prompt-engineering.md) |
| Guardrails & Safety | [docs/development/guardrails.md](docs/development/guardrails.md) |
| Fine-tuning & Training | [docs/development/fine-tuning.md](docs/development/fine-tuning.md) |
| Data Processing | [docs/development/data-processing.md](docs/development/data-processing.md) |
| Getting Started | [docs/guides/getting-started.md](docs/guides/getting-started.md) |
| Trends & Future Directions | [docs/guides/trends-2026.md](docs/guides/trends-2026.md) |

## Detailed Migration Map

### Models Section

**Old**: "1. 🤖 Text Models" in README.md  
**New**: [docs/models/text-models.md](docs/models/text-models.md)
- Proprietary models (OpenAI, Anthropic, Google, xAI, Cohere)
- Open source models (Meta, Alibaba, DeepSeek, Mistral, Microsoft, Google)
- Specialized models (reasoning, code, math, long context)

**Old**: "2. 👁️ Vision Models" in README.md  
**New**: [docs/models/vision-models.md](docs/models/vision-models.md)
- Vision-language models (VLMs)
- Image generation (Stable Diffusion, DALL-E, Midjourney, Flux)
- Video generation & understanding

**Old**: "Embeddings & Retrieval" from "Additional Categories" in README.md  
**New**: [docs/models/embeddings.md](docs/models/embeddings.md)
- MTEB leaderboard rankings
- Specialized embeddings and rerankers
- Selection guide

### Infrastructure Section

**Old**: "3. 🗄️ Vector Databases" in README.md  
**New**: [docs/infrastructure/vector-databases.md](docs/infrastructure/vector-databases.md)
- General purpose databases (FAISS, Chroma, Pinecone, Qdrant, Milvus, etc.)
- Specialized retrieval (ColBERT, SPLADE, HyDE)
- Hybrid search (Elasticsearch, OpenSearch, Vespa)

**Old**: "4. 📊 Graph Databases" in README.md  
**New**: [docs/infrastructure/graph-databases.md](docs/infrastructure/graph-databases.md)
- Property graphs (Neo4j, ArangoDB, TigerGraph)
- Knowledge graphs (RDF stores, triple stores)
- Graph analytics (NetworkX, PyG, DGL)

**Old**: "6. 🖥️ On-Premise Deployment" in README.md  
**New**: [docs/infrastructure/on-premise-deployment.md](docs/infrastructure/on-premise-deployment.md)
- Inference servers (vLLM, llama.cpp, TensorRT-LLM, TGI, SGLang)
- Model serving platforms (Ollama, LocalAI, Jan, LM Studio)
- Quantization methods (GGUF, AWQ, GPTQ, FP8)

### Frameworks Section

**Old**: "7. 🤝 Agentic Systems" in README.md  
**New**: Split into two files:
- [docs/frameworks/agentic-systems.md](docs/frameworks/agentic-systems.md) - MCP, multi-agent frameworks (AutoGen, CrewAI, LangGraph, MetaGPT), agent patterns
- [docs/frameworks/general-frameworks.md](docs/frameworks/general-frameworks.md) - LangChain, Haystack, Semantic Kernel, LlamaIndex

### Evaluation Section

**Old**: "5. 🏆 Leaderboards & Benchmarks" in README.md  
**New**: [docs/evaluation/leaderboards.md](docs/evaluation/leaderboards.md)
- Tool calling leaderboards (BFCL, ToolBench)
- Vision benchmarks (MMMU, MMBench)
- General LLM leaderboards (Chatbot Arena, Open LLM Leaderboard)
- Reasoning & math benchmarks (GPQA, MATH, GSM8K)

**Old**: "8. 📊 Observability & Monitoring" (Evaluation Frameworks part) and "9. 🧪 Evaluation & Testing" in README.md  
**New**: [docs/evaluation/evaluation-frameworks.md](docs/evaluation/evaluation-frameworks.md)
- Evaluation frameworks (RAGAS, DeepEval, TruLens, PromptFoo)
- LLM-as-judge patterns
- Specialized testing tools
- Benchmarking suites

### Operations Section

**Old**: "8. 📊 Observability & Monitoring" in README.md  
**New**: [docs/operations/observability.md](docs/operations/observability.md)
- LLM observability platforms (OpenTelemetry, LangFuse, LangSmith, W&B, Arize)
- Production monitoring tools
- Key metrics to track

**Old**: "Getting Started" section (Best Practices part) in README.md  
**New**: [docs/operations/production-checklist.md](docs/operations/production-checklist.md)
- Day one requirements
- Production checklist
- Deployment strategies

### Development Section

**Old**: "Prompt Engineering" from "Additional Categories" in README.md  
**New**: [docs/development/prompt-engineering.md](docs/development/prompt-engineering.md)
- Techniques & patterns (CoT, ReAct, ToT, few-shot)
- Tools & libraries (LangChain, DSPy, Guidance)

**Old**: "Guardrails & Safety" from "Additional Categories" in README.md  
**New**: [docs/development/guardrails.md](docs/development/guardrails.md)
- Guardrails AI, NeMo Guardrails, LLM Guard
- Safety frameworks and tools

**Old**: "Fine-tuning & Training" from "Additional Categories" in README.md  
**New**: [docs/development/fine-tuning.md](docs/development/fine-tuning.md)
- Training frameworks (HuggingFace, Axolotl, Unsloth)
- PEFT methods (LoRA, QLoRA)
- Distributed training (DeepSpeed, Megatron-LM)

**Old**: "Data Processing" from "Additional Categories" in README.md  
**New**: [docs/development/data-processing.md](docs/development/data-processing.md)
- Text processing (spaCy, NLTK, Tokenizers)
- Data validation (Pydantic, Pandera)
- Synthetic data (Faker, SDV, Gretel)

### Guides Section

**Old**: "Getting Started" in README.md  
**New**: [docs/guides/getting-started.md](docs/guides/getting-started.md)
- Choose your use case (text gen, RAG, agentic, multimodal)
- Select deployment strategy
- Implementation best practices

**Old**: "Trends & Future Directions" in README.md  
**New**: [docs/guides/trends-2026.md](docs/guides/trends-2026.md)
- Current state of LLM ecosystem
- Emerging directions
- Technology shifts

## What Changed?

### Structure
- **Before**: One 481-line README.md with all content
- **After**: Hub README.md + 18 specialized documentation files in `docs/`

### Navigation
- **Before**: Scroll through single file or use in-page anchors
- **After**: Click through to dedicated pages, each with table of contents and cross-references

### Updates
- **Before**: Edit single large file (risk of conflicts)
- **After**: Edit individual topic files (easier maintenance)

## For Bookmark/Link Updates

If you had bookmarks to specific sections in the old README:

### Old Bookmark Format
```
https://github.com/user/GenAI_Atlas#vector-databases
```

### New File Format
```
https://github.com/user/GenAI_Atlas/blob/main/docs/infrastructure/vector-databases.md
```

### Quick Conversion Table

| Old Anchor | New File Path |
|------------|---------------|
| `#text-models` | `docs/models/text-models.md` |
| `#vision-models` | `docs/models/vision-models.md` |
| `#vector-databases` | `docs/infrastructure/vector-databases.md` |
| `#on-premise-deployment` | `docs/infrastructure/on-premise-deployment.md` |
| `#agentic-systems` | `docs/frameworks/agentic-systems.md` |
| `#leaderboards--benchmarks` | `docs/evaluation/leaderboards.md` |
| `#observability--monitoring` | `docs/operations/observability.md` |

## Backup

The original README.md from before the restructure is saved as `README.old.md` for reference.

## Questions?

If you can't find where something moved, open an issue or use GitHub's search feature across the repository.

---

*Migration completed: April 18, 2026*
