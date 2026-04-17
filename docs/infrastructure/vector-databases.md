# Vector Databases

[Home](../../README.md) > [Infrastructure](../infrastructure/) > Vector Databases

> Comprehensive guide to vector databases for semantic search, RAG applications, and similarity search at scale.

*Last Updated: April 18, 2026*

## Table of Contents

- [General Purpose Databases](#general-purpose-databases)
- [Specialized Retrieval Methods](#specialized-retrieval-methods)
- [Hybrid Search Solutions](#hybrid-search-solutions)
- [Selection Guide](#selection-guide)
- [Related Resources](#related-resources)

## General Purpose Databases

| Database | Type | Version | Key Features | Link |
|----------|------|---------|-------------|------|
| **FAISS** | Library | 1.8+ | GPU acceleration (H100), ARM/Metal support, binary quantization | [GitHub](https://github.com/facebookresearch/faiss) |
| **Chroma** | Embedded/Distributed | 0.5+ | Multi-modal embeddings, HNSW, async API, ColBERT integration | [GitHub](https://github.com/chroma-core/chroma) |
| **Pinecone** | Managed | Serverless v2 | Sparse-dense hybrid, multi-vector, sub-50ms latency, 70% cost reduction | [Website](https://pinecone.io/) |
| **Weaviate** | Open Source | 1.26+ | Native graph+vector, generative search, multi-tenancy (10K+ tenants) | [Website](https://weaviate.io/) |
| **Qdrant** | Rust-based | 1.11+ | Scalar quantization, multi-vector, Matryoshka embeddings, distributed | [Website](https://qdrant.tech/) |
| **Milvus** | Distributed | 2.5+ | GPU-DiskANN, billion-scale, time-travel queries, 5x faster filtering | [Website](https://milvus.io/) |
| **LanceDB** | Embedded | Latest | Lance columnar format, multimodal, zero-copy reads, auto-versioning | [GitHub](https://github.com/lancedb/lancedb) |
| **Marqo** | Managed | 2.0+ | Built-in embeddings, multimodal search, no preprocessing, tensor search | [GitHub](https://github.com/marqo-ai/marqo) |

### Performance Highlights (April 2026)

- **FAISS 1.8+**: 3x faster GPU search on H100, ARM/Metal optimization
- **Chroma 0.5+**: 50% latency reduction with async API, distributed mode
- **Pinecone v2**: Sub-50ms p99 latency, 70% cost reduction vs v1
- **Qdrant 1.11+**: 4x throughput with scalar quantization
- **Milvus 2.5+**: 5x faster filtered search, GPU-DiskANN for billion-scale

## Specialized Retrieval Methods

Advanced retrieval techniques beyond basic dense vector search.

### ColBERTv3
- **Performance**: 73.2 BEIR score (state-of-the-art)
- **Speed**: 40% faster than ColBERTv2
- **Features**: Late interaction, multi-vector per document, native DB integration
- **Use Case**: High-quality retrieval when accuracy is critical
- [GitHub](https://github.com/stanford-futuredata/ColBERT)

### Dense Passage Retrieval (DPR) v2
- **Multilingual**: 100+ languages
- **Training**: Hard negatives from GPT-4
- **Improvement**: 15% better than v1 on Natural Questions
- **Use Case**: Cross-lingual retrieval, question answering

### SPLADE v3
- **Architecture**: Sparse embeddings (85% efficiency)
- **Features**: Hybrid mode, learned term importance
- **Integration**: Native in Elasticsearch 8.15+, OpenSearch 2.17+
- **Use Case**: Combining semantic and keyword search

### RankGPT
- **Approach**: LLM-based reranking (GPT-4o or Claude)
- **Performance**: 12% improvement over cross-encoders
- **Cost**: $0.001 per query with batching
- **Use Case**: Final reranking stage for top-k results

### HyDE v2 (Hypothetical Document Embeddings)
- **Approach**: Generate hypothetical documents, embed, retrieve
- **Performance**: 18% improvement on complex queries
- **Features**: Multi-hop reasoning support
- **Integration**: Built into LangChain, LlamaIndex
- **Use Case**: Complex queries, when query-document mismatch exists

## Hybrid Search Solutions

Combining dense vectors with traditional full-text search.

### Elasticsearch 8.16+
- **ELSER v3**: Learned sparse encoders, 25% better relevance
- **Multi-vector**: Late interaction support
- **Adaptive Retrieval**: Auto-blend BM25 + dense + ELSER
- **Performance**: 3x faster vector search with quantized HNSW
- [Website](https://www.elastic.co/)

### OpenSearch 2.18+
- **Neural Search v2**: Model chaining, conversational search
- **Multi-modal**: Text + image + audio embeddings
- **Vector Streaming**: 10K+ docs/sec ingestion
- **Cost Optimizer**: Hybrid query cost-based optimization
- [Website](https://opensearch.org/)

### Vespa 8.3+
- **Tensor Expressions**: Custom ranking with tensors
- **Phased Retrieval**: BM25 → Dense → Neural Rerank
- **Performance**: Sub-50ms on billion-scale indexes
- **Features**: Matryoshka embedding support
- [Website](https://vespa.ai/)

### TypeSense 27+
- **Hybrid Search**: Semantic + keyword fusion
- **Built-in Embeddings**: No external service needed
- **Conversational**: Search with memory
- **Performance**: 10x faster filtered queries vs v26
- [Website](https://typesense.org/)

## Selection Guide

### By Use Case

**RAG Applications (General)**
- **Self-hosted**: Qdrant (best balance of features/performance)
- **Managed**: Pinecone Serverless v2 (sub-50ms latency, auto-scaling)
- **Embedded**: Chroma (developer-friendly, good for prototyping)

**Billion-Scale Deployments**
- Milvus 2.5+ with GPU-DiskANN
- Weaviate 1.26+ with multi-tenancy

**Multimodal Search (Text + Images)**
- LanceDB (native multimodal)
- Marqo (built-in embeddings)
- Chroma 0.5+ (multi-modal support)

**Hybrid Search (Keyword + Semantic)**
- Elasticsearch 8.16+ (mature, feature-rich)
- OpenSearch 2.18+ (open source, AWS ecosystem)
- Vespa 8.3+ (high performance)

**High-Quality Retrieval**
- Qdrant + ColBERTv3 integration
- Weaviate with generative search
- Custom: FAISS + Cohere rerank-v4

**Local/Edge Deployment**
- FAISS (library, maximum control)
- Chroma (embedded mode)
- LanceDB (zero-copy, efficient)

**Research/Experimentation**
- FAISS (most flexible, well-documented)
- Chroma (easy to get started)

### By Team/Resources

**Small Team, Quick Start**
→ Pinecone Serverless v2 or Chroma

**Self-Hosted, Open Source**
→ Qdrant or Weaviate

**Existing Elasticsearch/OpenSearch**
→ Add vector search capabilities to existing setup

**Python-First, Research**
→ FAISS or Chroma

**Production Scale, High Performance**
→ Milvus or Qdrant (distributed)

## Performance Comparison

| Database | Latency (p99) | Throughput | Scale | Ease of Use |
|----------|---------------|------------|-------|-------------|
| Pinecone v2 | <50ms | Very High | Billions | Easy |
| Qdrant | <100ms | High | Billions | Medium |
| Milvus | Variable | Very High | Billions | Medium |
| Weaviate | <100ms | High | Billions | Medium |
| Chroma | <200ms | Medium | Millions | Easy |
| FAISS | <10ms | Extreme | Billions | Hard |

## Best Practices

### Indexing Strategy
1. **HNSW** (default): Best balance of speed and recall
2. **IVF**: Better for billion-scale with GPU
3. **Flat**: Perfect recall, slow at scale

### Quantization
- **No quantization**: Best quality, highest memory
- **Scalar (8-bit)**: 4x memory reduction, minimal quality loss
- **Binary**: 32x compression, 5-8% recall loss
- **Product Quantization**: 8-16x compression, configurable quality

### Two-Stage Retrieval
1. **Fast retrieval**: Get top 100-1000 with vector search
2. **Reranking**: Use Cohere rerank-v4 or BGE-reranker for top 20

**Result**: 10-15% better relevance with minimal latency increase

### Hybrid Search Recipe
```
Score = (0.7 × semantic_score) + (0.3 × keyword_score)
```
Adjust weights based on your data and queries.

## Related Resources

- [Embeddings](../models/embeddings.md) - Models to generate vectors
- [RAG Guide](../guides/rag-guide.md) - Building RAG systems
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Testing retrieval quality
- [Getting Started](../guides/getting-started.md) - Vector database selection

---

[🏠 Back to Home](../../README.md)
