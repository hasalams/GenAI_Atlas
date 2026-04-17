# Graph Databases

[Home](../../README.md) > [Infrastructure](../infrastructure/) > Graph Databases

> Graph databases for knowledge graphs, relationship-heavy data, and network analysis in LLM applications.

*Last Updated: April 18, 2026*

## Table of Contents

- [Property Graphs](#property-graphs)
- [Knowledge Graphs](#knowledge-graphs)
- [Graph Analytics](#graph-analytics)
- [Use Cases with LLMs](#use-cases-with-llms)
- [Related Resources](#related-resources)

## Property Graphs

Native graph databases optimized for traversing relationships.

| Database | Type | Performance | Best For |
|----------|------|------------|----------|
| **Neo4j** | Native Graph | High | OLTP, real-time queries |
| **ArangoDB** | Multi-model | Very High | Graph + document + key-value |
| **TigerGraph** | Native Graph | Extreme | Analytics, large-scale |
| **Amazon Neptune** | Managed | High | AWS ecosystem |

### Neo4j
- **Use Case**: General-purpose graph database, relationships-first
- **Query Language**: Cypher (declarative, SQL-like for graphs)
- **Scale**: Billions of nodes and relationships
- **Features**: ACID transactions, full-text search, graph algorithms
- [Website](https://neo4j.com/)

### ArangoDB
- **Use Case**: Multi-model (graph + document + key-value) in one system
- **Query Language**: AQL (ArangoDB Query Language)
- **Scale**: Distributed, horizontally scalable
- **Features**: Flexible schema, joins across models
- [Website](https://www.arangodb.com/)

### TigerGraph
- **Use Case**: Real-time deep link analytics, fraud detection
- **Query Language**: GSQL (Graph SQL)
- **Scale**: Extreme scale, parallel graph processing
- **Features**: Native parallel graph, real-time updates
- [Website](https://www.tigergraph.com/)

### Amazon Neptune
- **Use Case**: Managed graph database, AWS integration
- **Query Languages**: Gremlin, SPARQL, openCypher
- **Scale**: Fully managed, auto-scaling
- **Features**: Both property graph and RDF support
- [Website](https://aws.amazon.com/neptune/)

## Knowledge Graphs

RDF (Resource Description Framework) and triple stores for semantic web and knowledge representation.

### RDF Stores
- **Apache Jena**: Java-based, complete semantic web framework
- **Stardog**: Enterprise knowledge graph platform, reasoning engine
- **GraphDB**: RDF database with reasoning, Ontotext

### Triple Stores
- **Blazegraph**: High-performance RDF graph database (formerly used by Wikidata)
- **Virtuoso**: Hybrid database (RDF + relational), OpenLink Software

### Use Cases
- **Ontologies**: Formal knowledge representation
- **Linked Data**: Connecting datasets across the web
- **Reasoning**: Inferring new facts from existing knowledge
- **LLM Integration**: Structured knowledge for RAG, fact-checking

## Graph Analytics

Libraries for graph analysis, machine learning on graphs, and network science.

### NetworkX
- **Language**: Python
- **Use Case**: General-purpose graph analysis, algorithms
- **Features**: 100+ graph algorithms, visualization
- **Scale**: Small to medium graphs (in-memory)
- [Website](https://networkx.org/)

### PyG (PyTorch Geometric)
- **Language**: Python (PyTorch)
- **Use Case**: Graph Neural Networks, deep learning on graphs
- **Features**: GNN layers, heterogeneous graphs, message passing
- **Integration**: PyTorch ecosystem
- [Website](https://pytorch-geometric.readthedocs.io/)

### DGL (Deep Graph Library)
- **Language**: Python (PyTorch/TensorFlow/MXNet)
- **Use Case**: GNNs for various backends
- **Features**: Efficient message passing, mini-batch training
- **Scale**: Large-scale graphs
- [Website](https://www.dgl.ai/)

## Use Cases with LLMs

### Knowledge Graph + RAG
**Pattern**: Graph-enhanced retrieval

1. **Structure**: Store entities and relationships in graph
2. **Retrieval**: Traverse graph to find relevant context
3. **Generation**: Use graph-retrieved context with LLM
4. **Benefit**: Better context through relationships

**Tools**: Neo4j + LangChain, GraphRAG (Microsoft)

### Entity Extraction → Graph
**Pattern**: Build knowledge graphs from text

1. **Extract**: Use LLM to extract entities and relationships
2. **Structure**: Store in graph database
3. **Query**: Natural language → graph query → answer
4. **Benefit**: Structured knowledge from unstructured text

### Graph Reasoning
**Pattern**: Multi-hop reasoning over graphs

1. **Question**: Complex multi-step query
2. **Traverse**: Walk graph to gather evidence
3. **Aggregate**: Combine findings across hops
4. **Answer**: Generate response with full context

**Use Case**: Supply chain analysis, fraud detection, scientific research

### Hybrid: Vector + Graph
**Pattern**: Combine semantic similarity with relationships

1. **Vector DB**: Semantic similarity search (embeddings)
2. **Graph DB**: Relationship traversal
3. **Fusion**: Combine results based on task
4. **Benefit**: Best of both approaches

**Example**: Weaviate (native graph + vector)

## Selection Guide

### **For General Graph Applications**
→ Neo4j (mature, ecosystem, Cypher)

### **For Multi-Model Needs**
→ ArangoDB (graph + document + key-value)

### **For Extreme Scale Analytics**
→ TigerGraph (parallel processing, real-time)

### **For AWS Ecosystem**
→ Amazon Neptune (managed, serverless)

### **For Semantic Web / Ontologies**
→ Stardog or GraphDB (RDF, reasoning)

### **For Graph Machine Learning**
→ PyG or DGL (GNNs, research)

### **For Python Analysis**
→ NetworkX (easy to use, well-documented)

## Integration Patterns

### Graph + LLM Architecture

```
User Query
    ↓
[LLM: Parse Query]
    ↓
[Graph DB: Execute Query]
    ↓
[LLM: Generate Answer from Graph Results]
    ↓
Response
```

### LangChain + Neo4j Example
- Cypher generation from natural language
- Graph traversal for context
- Answer generation with retrieved paths

### Microsoft GraphRAG
- Extract entities and relationships using LLMs
- Build community structure
- Answer questions with graph-based retrieval

## Related Resources

- [Vector Databases](vector-databases.md) - For semantic similarity search
- [Agentic Systems](../frameworks/agentic-systems.md) - Multi-step graph reasoning
- [RAG Guide](../guides/rag-guide.md) - Combining graph and vector retrieval
- [Knowledge Graphs (External)](https://en.wikipedia.org/wiki/Knowledge_graph)

---

[🏠 Back to Home](../../README.md)
