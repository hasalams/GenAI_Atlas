# Embeddings & Retrieval Models

[Home](../../README.md) > [Models](../models/) > Embeddings

> State-of-the-art embedding models for semantic search, RAG systems, and information retrieval. Includes MTEB leaderboard rankings and specialized reranking models.

*Last Updated: April 18, 2026*

## Table of Contents

- [State-of-the-Art Embeddings (MTEB Leaderboard)](#state-of-the-art-embeddings-mteb-leaderboard)
- [Specialized Embeddings](#specialized-embeddings)
- [Selection Guide](#selection-guide)
- [Related Resources](#related-resources)

## State-of-the-Art Embeddings (MTEB Leaderboard)

Performance as of April 2026 on Massive Text Embedding Benchmark.

| Model | Provider | Dimensions | MTEB Score | Key Features |
|-------|----------|------------|------------|-------------|
| **Voyage-3-Large** | Voyage AI | 2048 | 68.5 | Domain-specific variants (code, finance, legal, medical) |
| **BGE-v2.5** | BAAI | 1024 | 68.2 | Matryoshka support, in-context learning, multilingual |
| **E5-Mistral-7B** | Microsoft | Variable | 67.1 | Instruction-tuned, task-specific prompts, best 7B model |
| **Cohere embed-v4** | Cohere | 1024→256 | 67.5 | Compression, int8 quantization, 100+ languages |
| **OpenAI text-embedding-3-large-turbo** | OpenAI | 3072 | 66.8 | Matryoshka-compatible, 3x faster, 50% cost reduction |
| **Jina-embeddings-v3** | Jina AI | 1024 | 66.3 | 8K context, multi-task training, Apache 2.0 |
| **Nomic-embed-v2** | Nomic | 768 | 64.5 | Fully reproducible, variable context (128-8192) |

### Key Trends

- **Matryoshka Embeddings**: Adaptive dimensionality (use fewer dimensions for speed/cost)
- **Instruction-Tuning**: Task-specific prompts improve retrieval quality
- **Compression**: Reduce dimensions without significant quality loss
- **Long Context**: Models supporting 8K+ input tokens

## Specialized Embeddings

### General Purpose Frameworks
- **Sentence Transformers 3.2+**: Matryoshka embeddings by default, BGE integration, cross-encoder distillation
- **CLIP / OpenCLIP**: Vision-language embeddings for multimodal search

### Reranking Models

Critical for improving retrieval quality in RAG systems.

| Model | Provider | BEIR Score | Key Features |
|-------|----------|------------|-------------|
| **Cohere rerank-v4** | Cohere | 74.1 | SOTA reranker, API-based, fast |
| **BGE-reranker-v2.5-gemma2** | BAAI | 73.8 | 27B model, open source, high quality |

### Domain-Specific
- **Voyage AI**: Specialized models for code, finance, legal, medical domains
- **E5-Mistral-7B**: Task-specific instruction prompts

## Selection Guide

### **For RAG Applications**
**Best Quality**: Voyage-3-Large or BGE-v2.5  
**Best Value**: Cohere embed-v4 (compression) or OpenAI text-embedding-3-large-turbo  
**Open Source**: Jina-embeddings-v3 or Nomic-embed-v2  

**Reranking**: Cohere rerank-v4 (managed) or BGE-reranker-v2.5 (self-hosted)

### **For Multilingual**
- Cohere embed-v4 (100+ languages)
- BGE-v2.5 (multilingual support)

### **For Long Context**
- Jina-embeddings-v3 (8K context)
- Nomic-embed-v2 (up to 8192 tokens)

### **For Code Search**
- Voyage-3-Large (code variant)
- OpenAI text-embedding-3-large-turbo

### **For Domain-Specific**
- Voyage-3-Large variants (finance, legal, medical)
- Fine-tune Sentence Transformers on domain data

### **For Local Deployment**
- Nomic-embed-v2 (fully reproducible)
- BGE-v2.5 (open source, efficient)
- Sentence Transformers models

### **For Cost Optimization**
- Use Matryoshka embeddings (reduce dimensions)
- Cohere embed-v4 with compression (1024→256)
- OpenAI text-embedding-3-large-turbo (3x faster, 50% cheaper)

## Implementation Tips

### Matryoshka Embeddings
```
# Start with full dimensions, reduce as needed:
Full: 1024 dimensions → Best quality
768 dimensions → 2-3% quality loss, 25% faster
512 dimensions → 5% quality loss, 50% faster
256 dimensions → 8-10% quality loss, 75% faster
```

### Two-Stage Retrieval
1. **First Stage**: Fast dense retrieval with embeddings (top 100-1000 results)
2. **Second Stage**: Rerank with Cohere rerank-v4 or BGE-reranker (top 10-20)

**Quality Improvement**: 10-15% better relevance scores

### Hybrid Search
Combine:
- **Dense**: Semantic similarity with embeddings
- **Sparse**: Keyword matching with BM25
- **Fusion**: Combine scores for best of both

See [Vector Databases - Hybrid Search](../infrastructure/vector-databases.md#hybrid-search) for implementation.

## Performance Comparison

| Model | Dimensions | Speed | Cost | Quality (MTEB) |
|-------|------------|-------|------|----------------|
| Voyage-3-Large | 2048 | Medium | $$ | 68.5 (Best) |
| BGE-v2.5 | 1024 | Fast | Free | 68.2 |
| Cohere embed-v4 | 1024→256 | Very Fast | $ | 67.5 |
| OpenAI (turbo) | 3072→N | Very Fast | $ | 66.8 |
| Jina-v3 | 1024 | Fast | Free | 66.3 |

## Related Resources

- [Vector Databases](../infrastructure/vector-databases.md) - Where to store embeddings
- [RAG Guide](../guides/rag-guide.md) - Building RAG systems with embeddings
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Testing retrieval quality (RAGAS)
- [Specialized Retrieval](../infrastructure/vector-databases.md#specialized-retrieval) - ColBERT, SPLADE, HyDE

---

[🏠 Back to Home](../../README.md)
