# 🚀 LLMs and Generative AI Resources Repository

A comprehensive, well-structured collection of resources, tools, and frameworks for Large Language Models and Generative AI applications. This repository serves as a central hub for developers, researchers, and practitioners working with modern AI systems.

## 📚 Repository Structure

### 1. 🤖 Text Models

#### Proprietary Models
| Provider | Models | Key Features |
|----------|--------|-------------|
| **OpenAI** | GPT-4o, GPT-4.1, GPT-o3, GPT-4o mini | Function calling, reasoning, multimodal |
| **Anthropic** | Claude 3.5 Sonnet, Claude 3.7 Sonnet | Long context, safety, computer use |
| **Google** | Gemini 2.5 Pro, Gemini 2.0 Flash | Multimodal, 2M token context |
| **xAI** | Grok-3 | Real-time data, X integration |
| **Cohere** | Command R+ | RAG optimization, multilingual |

#### Open Source Models
| Provider | Models | Parameters | Key Features |
|----------|--------|------------|-------------|
| **Meta** | Llama 3.1 405B, Llama 3.3 70B | 405B, 70B | Open weights, commercial use |
| **Alibaba** | Qwen 3, Qwen 2.5-Max | 235B+ | Multilingual, reasoning |
| **DeepSeek** | DeepSeek R1, DeepSeek-V3 | 671B | Reasoning, MoE architecture |
| **Mistral** | Mistral Large 2, Mixtral 8x22B | 123B, 141B | European, efficiency |
| **Microsoft** | Phi-3 | 3B-14B | Small models, high performance |

#### Specialized Models
- **Reasoning**: o1, o3-mini, DeepSeek R1
- **Code**: CodeLlama, DeepSeek Coder, StarCoder2
- **Math**: Llemma, MathLlama
- **Long Context**: Gemini 1.5 Pro (2M tokens), Claude-3 (200k tokens)

### 2. 👁️ Vision Models

#### Vision-Language Models
- **Proprietary**: GPT-4V, Claude 3.5 Sonnet, Gemini Vision Pro
- **Open Source**: LLaVA, Qwen2-VL, InternVL, CogVLM, LLaVA-NeXT
- **Specialized**: PaliGemma, Flamingo, BLIP-2, InstructBLIP

#### Image Generation
- **Diffusion Models**: Stable Diffusion XL, Midjourney, DALL-E 3
- **Other**: Imagen, Parti

#### Video Models
- Sora, Runway Gen-2, Pika Labs, VideoCrafter

### 3. 🗄️ Vector Databases

#### General Purpose
| Database | Type | Key Features | Link |
|----------|------|-------------|------|
| **FAISS** | Library | Facebook's similarity search | [GitHub](https://github.com/facebookresearch/faiss) |
| **Chroma** | Embedded | Developer-friendly, SQL-like | [GitHub](https://github.com/chroma-core/chroma) |
| **Pinecone** | Managed | Serverless, real-time updates | [Website](https://pinecone.io/) |
| **Weaviate** | Open Source | GraphQL, vector + object search | [Website](https://weaviate.io/) |
| **Qdrant** | Rust-based | High performance, filtering | [Website](https://qdrant.tech/) |
| **Milvus** | Distributed | Scalable, cloud-native | [Website](https://milvus.io/) |

#### Specialized Retrieval
- **ColBERT**: Late interaction, Stanford Research - [GitHub](https://github.com/stanford-futuredata/ColBERT)
- **Dense Passage Retrieval (DPR)**: Facebook's dense retrieval
- **SPLADE**: Sparse + dense hybrid retrieval

#### Hybrid Search
- **Elasticsearch**: Full-text + vector search
- **OpenSearch**: AWS's Elasticsearch fork
- **Vespa**: Yahoo's big data serving engine

### 4. 📊 Graph Databases

#### Property Graphs
| Database | Type | Performance | Best For |
|----------|------|------------|----------|
| **Neo4j** | Native Graph | High | OLTP, real-time queries |
| **ArangoDB** | Multi-model | Very High | Graph + document + key-value |
| **TigerGraph** | Native Graph | Extreme | Analytics, large-scale |
| **Amazon Neptune** | Managed | High | AWS ecosystem |

#### Knowledge Graphs
- **RDF Stores**: Apache Jena, Stardog, GraphDB
- **Triple Stores**: Blazegraph, Virtuoso

#### Graph Analytics
- **NetworkX**: Python graph analysis
- **PyG**: PyTorch Geometric for GNNs
- **DGL**: Deep Graph Library

### 5. 🏆 Leaderboards & Benchmarks

#### Tool Calling
| Benchmark | Focus | Link |
|-----------|-------|------|
| **Berkeley Function Calling Leaderboard (BFCL)** | Function accuracy | [Website](https://gorilla.cs.berkeley.edu/leaderboard.html) |
| **ToolBench** | Tool use evaluation | [GitHub](https://github.com/OpenBMB/ToolBench) |
| **ToolScan** | Error pattern analysis | Research paper |
| **DPAB-α** | Pythonic vs JSON calling | [GitHub](https://github.com/firstbatch/function-c-eval) |

#### Vision Benchmarks
- **MMMU**: Multi-discipline multimodal understanding
- **MMBench**: Comprehensive vision-language evaluation
- **SEED-Bench**: Multimodal LLM evaluation
- **LLaVA-Bench**: Visual instruction following

#### General LLM Leaderboards
- **Open LLM Leaderboard**: Hugging Face's comprehensive ranking
- **Chatbot Arena**: Human preference evaluation (LMSYS)
- **HELM**: Stanford's holistic evaluation
- **BigBench**: Google's diverse task collection

#### Reasoning & Math
- **GPQA**: Graduate-level science questions
- **MATH**: Competition mathematics
- **GSM8K**: Grade school math word problems
- **MuSR**: Multi-step reasoning tasks

### 6. 🖥️ On-Premise Deployment

#### Inference Servers
| Server | Optimization | Best For | Key Features |
|--------|-------------|----------|-------------|
| **vLLM** | GPU | High throughput | Tensor parallelism, continuous batching, PagedAttention |
| **Llama.cpp** | CPU/GPU | Edge deployment | GGUF quantization, Metal/CUDA support |
| **TensorRT-LLM** | NVIDIA GPU | Maximum performance | TensorRT optimization |
| **Text Generation Inference (TGI)** | GPU | Production | HuggingFace integration |
| **SGLang** | GPU | Structured generation | Fast serving with constraints |
| **ExLlamaV2** | GPU | Memory efficiency | EXL2 quantization |

#### Model Serving Platforms
- **Ollama**: Simple local model serving
- **LocalAI**: OpenAI API compatibility
- **Jan**: Desktop AI assistant
- **LM Studio**: GUI for local models
- **GPT4All**: Cross-platform local AI

#### Quantization Methods
| Method | Target | Bits | Best For |
|--------|--------|------|----------|
| **GGUF** | CPU/GPU | 2-8 bit | General purpose, llama.cpp |
| **GPTQ** | GPU | 4 bit | GPU inference, older method |
| **AWQ** | GPU | 4 bit | Activation-aware, 2x faster than GPTQ |
| **EXL2** | GPU | Mixed | Best performance, ExLlama |
| **BitsAndBytes** | GPU | 4/8 bit | Hugging Face integration |

### 7. 🤝 Agentic Systems

#### Tools & Function Calling
- **LangChain Tools**: Comprehensive tool ecosystem
- **Haystack Tools**: Enterprise-focused tools
- **ReAct**: Reasoning and Acting pattern
- **Toolformer**: Self-supervised tool learning

#### Model Context Protocol (MCP)
| Component | Description | Link |
|-----------|-------------|------|
| **Core Protocol** | Anthropic's standardization | [Docs](https://docs.anthropic.com/en/docs/mcp) |
| **MCP Servers** | Playwright, Database, Filesystem | Various implementations |
| **MCP Clients** | Claude Desktop, Semantic Kernel | Integration examples |

#### Multi-Agent Frameworks

##### Collaborative Frameworks
| Framework | Focus | Language | Key Features |
|-----------|-------|----------|-------------|
| **AutoGen** | Multi-agent conversation | Python | Microsoft's framework, role-based agents |
| **CrewAI** | Team-based AI | Python | Task delegation, collaborative workflows |
| **LangGraph** | Graph-based orchestration | Python | State management, complex workflows |
| **MetaGPT** | Software development | Python | Multi-role software team simulation |

##### General Purpose
- **LangChain**: Comprehensive LLM framework
- **Haystack**: NLP pipeline framework  
- **Semantic Kernel**: Microsoft's AI orchestration
- **Phidata**: Production-ready agent framework

##### Specialized
- **JADE**: Java Agent Development Framework
- **Mesa**: Agent-based modeling in Python
- **Ray RLlib**: Multi-agent reinforcement learning
- **RASA**: Conversational AI framework

### 8. 📊 Observability & Monitoring

#### LLM Observability
| Tool | Type | Key Features |
|------|------|-------------|
| **OpenTelemetry** | Standard | Distributed tracing, vendor-neutral |
| **LangFuse** | Platform | LLM-specific observability |
| **Weights & Biases** | Platform | Experiment tracking, model monitoring |
| **Arize** | Platform | ML monitoring, drift detection |
| **LangSmith** | Platform | LangChain's debugging tool |

#### ML Experiment Tracking
- **MLFlow**: Open source ML lifecycle management
- **Neptune**: Experiment tracking and model registry
- **ClearML**: ML/DL experiment manager
- **TensorBoard**: TensorFlow's visualization toolkit

#### Production Monitoring
- **Prometheus**: Time series monitoring
- **Grafana**: Observability dashboards
- **Datadog**: Cloud monitoring platform
- **New Relic**: Application performance monitoring

### 9. 🧪 Evaluation Frameworks

#### General Purpose
| Framework | Focus | Key Features |
|-----------|-------|-------------|
| **Arize Phoenix** | LLM evaluation | Trace analysis, hallucination detection |
| **RAGAS** | RAG evaluation | Retrieval and generation metrics |
| **DeepEval** | LLM testing | Unit testing for LLMs |
| **TruLens** | Truthfulness | Trust and transparency evaluation |

#### Specialized
- **LangChain Evaluation**: Built-in evaluation tools
- **Promptfoo**: CLI evaluation tool
- **OpenAI Evals**: OpenAI's evaluation suite
- **LlamaIndex Evaluation**: RAG-specific evaluations

#### Benchmarking Suites
- **LM Evaluation Harness**: Standardized LLM evaluation
- **BigBench**: Google's comprehensive benchmark
- **HELM**: Stanford's holistic evaluation

### 10. 🎯 Additional Categories

#### Embeddings & Retrieval
- **Sentence Transformers**: Easy sentence embeddings
- **BGE Models**: BAAI's general embeddings
- **E5 Models**: Microsoft's embedding models
- **CLIP**: Vision-language embeddings

#### Prompt Engineering
- **Templates & Libraries**: LangChain prompts, Promptify
- **Techniques**: Few-shot, Chain-of-Thought, ReAct, Tree of Thoughts

#### Guardrails & Safety
| Framework | Focus | Key Features |
|-----------|-------|-------------|
| **Guardrails AI** | Output validation | Pydantic integration, validators |
| **NeMo Guardrails** | Conversation control | NVIDIA's dialogue management |
| **LlamaGuard** | Content safety | Facebook's safety classifier |

#### Fine-tuning & Training
- **Hugging Face Transformers**: Comprehensive ML framework
- **Axolotl**: Fine-tuning toolkit
- **Unsloth**: Fast fine-tuning
- **LLaMA Factory**: Easy LLM fine-tuning

#### Data Processing
- **Text Processing**: spaCy, NLTK, Tokenizers
- **Data Validation**: Pydantic, Pandera, Great Expectations
- **Synthetic Data**: Faker, SDV, Gretel

## 🌐 Network Relationships

This repository includes a comprehensive network graph showing relationships between different components:

- **Core Dependencies**: How models depend on inference servers
- **Integration Patterns**: How vector databases connect to agentic systems
- **Monitoring Flows**: How observability tools track different components
- **Evaluation Chains**: How benchmarks assess various capabilities

## 🚀 Getting Started

1. **Choose Your Use Case**:
   - Text generation → Text Models + Inference Servers
   - RAG applications → Text Models + Vector Databases + Embeddings
   - Multi-agent systems → Agentic Frameworks + Tools
   - Production deployment → Observability + Guardrails + Evaluation

2. **Select Appropriate Tools**:
   - Local deployment: Ollama + llama.cpp + GGUF quantization
   - Cloud deployment: vLLM + OpenTelemetry + MLFlow
   - Research: Hugging Face + Evaluation frameworks

3. **Implement Monitoring**:
   - Add observability from day one
   - Set up evaluation benchmarks
   - Implement safety guardrails

## 🤝 Contributing

This repository is designed to be a living document. Contributions are welcome for:

- Adding new tools and frameworks
- Updating benchmark results
- Improving categorization
- Adding relationship mappings
- Sharing implementation examples

## 📈 Trends & Future Directions

- **Multimodal Integration**: Vision + Text + Audio models
- **Edge Deployment**: Smaller, more efficient models
- **Agentic Workflows**: Complex multi-step reasoning
- **Safety & Alignment**: Robust guardrails and monitoring
- **Standardization**: Protocols like MCP gaining adoption

---

**Note**: This repository focuses on the rapidly evolving LLM ecosystem. Tools, benchmarks, and best practices are constantly changing. Please verify current versions and compatibility before implementation.

## 📊 Repository Statistics

- **Total Categories**: 10 major categories
- **Tools & Frameworks**: 100+ listed resources  
- **Network Nodes**: 39 key components
- **Relationships**: 31+ documented connections
- **Update Frequency**: Monthly updates planned

Built with ❤️ for the LLM & GenAI community

Note: This is still WIP
Date: 25 Aug 2025