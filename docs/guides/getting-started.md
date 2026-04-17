# Getting Started with LLM Applications

[Home](../../README.md) > [Guides](../) > Getting Started

> Step-by-step guide to choosing the right tools, models, and deployment strategies for your LLM application.

*Last Updated: April 18, 2026*

## Table of Contents
- [Choose Your Use Case](#choose-your-use-case)
- [Select Deployment Strategy](#select-deployment-strategy)
- [Implement Best Practices](#implement-best-practices)
- [Next Steps](#next-steps)

## Choose Your Use Case

### Text Generation / Chat

Building conversational AI, chatbots, or text generation applications.

#### Proprietary Models

**Claude 4.6 Opus/Sonnet**
- **Best For:** Long context reasoning, coding, analysis
- **Context:** 200K tokens
- **Strengths:** Strong reasoning, computer use, agentic capabilities
- **Cost:** Premium tier
- **Link:** [Anthropic](https://anthropic.com)

**GPT-4o**
- **Best For:** Multimodal applications, fast response times
- **Context:** 128K tokens
- **Strengths:** Vision, audio, function calling, broad capabilities
- **Cost:** Balanced performance/cost
- **Link:** [OpenAI](https://openai.com)

**Gemini 2.5 Pro**
- **Best For:** Extreme long context, video understanding
- **Context:** 2M tokens
- **Strengths:** Native multimodal, massive context window
- **Cost:** Variable by context usage
- **Link:** [Google AI](https://ai.google.dev)

#### Open Source Models

**Llama 3.3 70B**
- **Best For:** General purpose, commercial use
- **Context:** 128K tokens
- **Strengths:** Open weights, strong performance, tool use
- **Deployment:** Local or cloud
- **Link:** [Meta AI](https://llama.meta.com)

**Qwen 2.5 72B**
- **Best For:** Multilingual applications
- **Context:** 128K tokens
- **Strengths:** 29 languages, reasoning, coding
- **Deployment:** Local or cloud
- **Link:** [Qwen](https://qwenlm.github.io)

**DeepSeek-V3**
- **Best For:** Advanced reasoning, cost-efficient inference
- **Parameters:** 671B MoE (37B active)
- **Strengths:** o1-competitive reasoning, efficient architecture
- **Deployment:** Cloud (requires significant resources)
- **Link:** [DeepSeek](https://deepseek.com)

#### Local Deployment

**Ollama + llama.cpp**
- **Quantization:** Q5_K_M (best quality/size balance)
- **Models:** Llama 3.3 70B, Qwen 2.5, Phi-4
- **Hardware:** Mac (Metal), NVIDIA (CUDA), AMD (ROCm)
- **Setup:**
  ```bash
  # Install Ollama
  curl -fsSL https://ollama.ai/install.sh | sh
  
  # Pull model
  ollama pull llama3.3:70b-instruct-q5_K_M
  
  # Run
  ollama run llama3.3:70b-instruct-q5_K_M
  ```

### RAG Applications

Retrieval-Augmented Generation for question answering over documents.

#### Full Stack Recommendation

**Embeddings:**
- **BGE-v2.5** (open source, Matryoshka support)
- **Voyage-3-Large** (domain-specific variants)
- **Cohere embed-v4** (multilingual, compression)

**Vector Database:**
- **Qdrant** (self-hosted, scalar quantization)
- **Pinecone Serverless v2** (managed, sub-50ms latency)
- **Chroma** (embedded, easy start)

**Retrieval Strategy:**
- **Hybrid Search:** BM25 + dense embeddings
- **ColBERTv3:** Late interaction for better quality
- **Reranking:** Cohere rerank-v4 or BGE-reranker-v2.5

**Framework:**
- **LlamaIndex** (data-centric RAG)
- **LangChain** (comprehensive ecosystem)
- **Haystack** (enterprise search)

**Evaluation:**
- **RAGAS:** Faithfulness, answer relevancy, context precision/recall
- **Custom metrics:** Domain-specific accuracy

#### Simple RAG Implementation

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader
from llama_index.embeddings.huggingface import HuggingFaceEmbedding
from llama_index.llms.anthropic import Anthropic

# 1. Load documents
documents = SimpleDirectoryReader("./data").load_data()

# 2. Setup embeddings
embed_model = HuggingFaceEmbedding(model_name="BAAI/bge-base-en-v1.5")

# 3. Create index
index = VectorStoreIndex.from_documents(
    documents,
    embed_model=embed_model
)

# 4. Setup LLM
llm = Anthropic(model="claude-3-5-sonnet-20241022")

# 5. Query
query_engine = index.as_query_engine(llm=llm)
response = query_engine.query("What is the main topic?")
```

#### Best Practices for RAG

1. **Chunking Strategy:**
   - 512-1024 tokens per chunk
   - Overlap 10-20%
   - Preserve semantic boundaries (paragraphs, sections)

2. **Retrieval Optimization:**
   - Retrieve top-K (5-10) candidates
   - Rerank to top-N (3-5) for context
   - Use hybrid search (dense + sparse)

3. **Context Management:**
   - Include document metadata
   - Add source citations
   - Keep total context < 50% of model limit

4. **Evaluation:**
   - Measure retrieval quality separately
   - Test faithfulness to retrieved context
   - Track answer relevancy
   - Monitor hallucination rates

### Agentic Systems

Building autonomous systems with tool use and multi-step workflows.

#### Framework Selection

**LangGraph**
- **Best For:** Complex, cyclic workflows
- **Strengths:** State persistence, streaming, checkpoints
- **Use Case:** Multi-step research, data analysis pipelines
- **Link:** [LangChain LangGraph](https://langchain.com/langgraph)

**CrewAI**
- **Best For:** Team-based AI workflows
- **Strengths:** Role delegation, hierarchical processes
- **Use Case:** Software development teams, content creation
- **Link:** [CrewAI](https://crewai.com)

**AutoGen**
- **Best For:** Multi-agent conversations
- **Strengths:** Code execution, nested chats, AutoGen Studio
- **Use Case:** Code generation, complex problem solving
- **Link:** [Microsoft AutoGen](https://microsoft.github.io/autogen/)

#### Model Context Protocol (MCP)

**Standardized Tool Integration:**
- Anthropic's protocol for LLM-tool connection
- Growing ecosystem of MCP servers
- Supported by Claude Desktop, Semantic Kernel

**Available MCP Servers:**
- filesystem, git, github
- postgres, sqlite
- playwright (web automation)
- web search

**Getting Started:**
```json
// Claude Desktop config
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
    }
  }
}
```

#### Best Model Choices

**Claude 4.5 Sonnet**
- Computer use capabilities
- Strong tool calling
- Excellent coding
- Extended context

**GPT-4o**
- Fast response times
- Strong function calling
- Multimodal support
- Reliable tool use

**Command-R+**
- RAG-optimized
- Tool use
- Multilingual
- Cost-effective

#### Observability for Agents

**LangFuse or LangSmith:**
- Trace multi-step workflows
- Track tool calls
- Monitor costs per agent
- Debug failures

**Key Metrics:**
- Tool call success rate
- Steps to completion
- Cost per task
- User satisfaction

### Multimodal Applications

Vision, image generation, video understanding.

#### Vision-Language Models (VLMs)

**GPT-4o**
- Multi-image reasoning
- Fast inference
- Strong OCR
- Broad capabilities

**Claude 4.5 Sonnet**
- Document analysis
- Chart/graph interpretation
- Long-context vision
- High accuracy

**Gemini 2.0 Pro**
- Video understanding
- Extreme long context
- Native multimodal
- Temporal reasoning

#### Image Generation

**Open Source:**
- **Flux:** High quality, fast, strong community
- **Stable Diffusion 3.5:** Improved composition, text rendering

**Proprietary:**
- **Midjourney v7:** Photorealistic, artistic quality
- **DALL-E 3:** Consistent characters, prompt following
- **Ideogram:** Superior text rendering

#### Video Generation

**Available Platforms:**
- **Sora (OpenAI):** High quality, physics simulation
- **Runway Gen-3:** Camera control, 60+ second videos
- **Pika 2.0:** Accessible, creative control
- **Google Veo:** Long-form, realistic

## Select Deployment Strategy

### Production Cloud

Scalable, managed infrastructure for production workloads.

#### Recommended Stack

**Inference Server:**
- **vLLM 0.6+** with PagedAttention and prefix caching
- 20-30x throughput improvement
- 2-3x latency reduction
- GPU optimization

**Observability:**
- **OpenTelemetry** for distributed tracing
- **LangFuse** for LLM-specific monitoring
- Track cost, latency, quality, errors

**Evaluation:**
- **RAGAS** for RAG evaluation
- **DeepEval** for LLM unit testing
- Continuous quality assessment
- A/B testing framework

**Guardrails:**
- **Guardrails AI** for output validation
- **NeMo Guardrails** for conversation control
- Input/output validation
- Content safety

**Load Balancing:**
- NGINX or cloud-native load balancers
- Multiple model replicas
- Health checks
- Auto-scaling

#### Architecture Pattern

```
User Request
    ↓
[Load Balancer]
    ↓
[API Gateway + Auth]
    ↓
[Rate Limiting + Caching]
    ↓
[Application Logic]
    ↓
[Guardrails (Input)]
    ↓
[LLM Inference (vLLM)]
    ↓
[Guardrails (Output)]
    ↓
[Observability (OpenTelemetry)]
    ↓
Response to User
```

### Local/On-Premise

Self-hosted deployment for privacy, control, or cost optimization.

#### Recommended Stack

**Serving:**
- **Ollama** (simplest setup)
- **llama.cpp** (maximum optimization)
- **vLLM** (production-grade)

**Quantization:**
- **GGUF Q5_K_M** (best quality/size)
- **AWQ 4-bit** (GPU, quality-focused)
- **GPTQ 4-bit** (legacy support)

**Hardware Options:**

**Apple Silicon:**
- M3/M4 Max: 32-36 tokens/sec (7B models)
- M3/M4 Ultra: 70B models possible
- Metal acceleration
- Unified memory advantage

**NVIDIA:**
- RTX 4090: 7-13B models at speed
- A100/H100: 70B+ models
- CUDA acceleration
- TensorRT optimization

**AMD:**
- ROCm support
- MI250/MI300 for large models
- Growing ecosystem

#### Simple Local Setup

```bash
# Option 1: Ollama (easiest)
curl -fsSL https://ollama.ai/install.sh | sh
ollama pull llama3.3:70b-instruct-q5_K_M
ollama serve

# Option 2: llama.cpp (optimized)
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp
make
./server -m models/llama-3.3-70b-q5_K_M.gguf -c 4096

# Option 3: vLLM (production)
pip install vllm
vllm serve meta-llama/Llama-3.3-70B-Instruct --quantization awq
```

#### Monitoring

**Prometheus + Grafana:**
- Request rates
- Latency metrics
- Token throughput
- GPU utilization
- Memory usage

### Research & Experimentation

For research, prototyping, and experimentation.

#### Recommended Stack

**Platform:**
- **Hugging Face Transformers + Accelerate**
- Broad model support
- Research-friendly
- Community resources

**Fine-Tuning:**
- **Axolotl** (configuration-driven)
- **Unsloth** (2x faster, 60% memory savings)
- QLoRA for large models

**Evaluation:**
- **LM Evaluation Harness** (200+ benchmarks)
- **MTEB** (embeddings)
- **Custom metrics**

**Notebooks:**
- Jupyter with HuggingFace integrations
- Google Colab (free GPU)
- Kaggle Notebooks

## Implement Best Practices

### Day One Requirements

✅ **Observability**
- OpenTelemetry traces from start
- Cost tracking per request
- Latency monitoring (P50/P90/P99)
- Error tracking with context
- Dashboard for key metrics

✅ **Evaluation**
- Domain-specific test set
- Automated evaluation pipeline
- Human feedback collection
- Quality baselines
- Regression detection

✅ **Guardrails**
- Input validation (prompt injection, PII)
- Output validation (format, content safety)
- Rate limiting
- Content filtering
- Audit logging

✅ **Fallbacks**
- Multiple model providers
- Automatic failover
- Graceful degradation
- Circuit breakers
- User-facing error messages

✅ **Caching**
- Prefix caching for system prompts
- Semantic caching for similar queries
- Response caching for exact matches
- Cache hit rate monitoring
- TTL management

### Production Checklist

Before deploying to production, ensure:

#### Infrastructure
- [ ] Auto-scaling configured
- [ ] Load balancing in place
- [ ] Database for persistence
- [ ] Secrets management (Vault, AWS Secrets)
- [ ] CI/CD pipeline
- [ ] Rollback mechanism

#### Monitoring
- [ ] Cost tracking within budget
- [ ] P99 latency < SLA threshold
- [ ] Error rate < 1%
- [ ] Uptime monitoring
- [ ] Alert on anomalies
- [ ] Stakeholder dashboard

#### Quality & Safety
- [ ] Hallucination detection
- [ ] Content safety filters
- [ ] PII detection/redaction
- [ ] Prompt injection defense
- [ ] Output format validation
- [ ] Quality baseline established

#### Operations
- [ ] On-call rotation defined
- [ ] Runbooks documented
- [ ] Incident response plan
- [ ] Post-mortem process
- [ ] Status page (if applicable)

### Quick Start Templates

#### 1. Simple Chatbot (5 minutes)

```python
from anthropic import Anthropic

client = Anthropic(api_key="your-api-key")

def chat(message, history=[]):
    history.append({"role": "user", "content": message})
    
    response = client.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        messages=history
    )
    
    assistant_message = response.content[0].text
    history.append({"role": "assistant", "content": assistant_message})
    
    return assistant_message, history

# Usage
history = []
response, history = chat("Hello!", history)
response, history = chat("What is Python?", history)
```

#### 2. RAG System (15 minutes)

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader
from llama_index.embeddings.openai import OpenAIEmbedding
from llama_index.llms.openai import OpenAI

# Load and index documents
documents = SimpleDirectoryReader("./docs").load_data()
index = VectorStoreIndex.from_documents(documents)

# Query
query_engine = index.as_query_engine()
response = query_engine.query("What are the key points?")
print(response)
```

#### 3. Tool-Using Agent (30 minutes)

```python
from langchain.agents import create_openai_functions_agent, AgentExecutor
from langchain_openai import ChatOpenAI
from langchain.tools import Tool
from langchain.prompts import ChatPromptTemplate

# Define tools
def search(query: str) -> str:
    """Search for information"""
    return f"Results for: {query}"

tools = [
    Tool(name="Search", func=search, description="Search for information")
]

# Create agent
llm = ChatOpenAI(model="gpt-4o", temperature=0)
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant with access to tools."),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}")
])

agent = create_openai_functions_agent(llm, tools, prompt)
executor = AgentExecutor(agent=agent, tools=tools)

# Run
result = executor.invoke({"input": "Search for recent AI news"})
print(result)
```

## Next Steps

### Learning Path

1. **Week 1: Fundamentals**
   - Understand prompt engineering basics
   - Test different models via API
   - Build simple chatbot
   - Learn about tokens and costs

2. **Week 2: RAG Systems**
   - Implement basic RAG
   - Experiment with embeddings
   - Test retrieval strategies
   - Evaluate with RAGAS

3. **Week 3: Advanced Patterns**
   - Build tool-using agent
   - Implement guardrails
   - Add observability
   - A/B test improvements

4. **Week 4: Production**
   - Deploy with proper monitoring
   - Implement safety measures
   - Set up evaluation pipeline
   - Optimize costs

### Resources

**Official Documentation:**
- [OpenAI Docs](https://platform.openai.com/docs)
- [Anthropic Docs](https://docs.anthropic.com)
- [LangChain Docs](https://python.langchain.com)
- [LlamaIndex Docs](https://docs.llamaindex.ai)

**Community:**
- [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA) - Local deployment
- [r/LangChain](https://reddit.com/r/LangChain) - Framework discussions
- [Hugging Face Forums](https://discuss.huggingface.co)
- [Discord Communities](https://discord.gg) - Model-specific channels

**Courses:**
- DeepLearning.AI courses on LLMs
- Fast.ai practical deep learning
- Stanford CS324 (Large Language Models)

## Related Resources
- [Text Models](../models/text-models.md) - Model capabilities and selection
- [Agentic Systems](../frameworks/agentic-systems.md) - Building autonomous agents
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Testing and benchmarking
- [Production Checklist](../operations/production-checklist.md) - Deployment requirements
- [Trends & Future Directions](./trends-2026.md) - What's next in LLMs

---

[🏠 Back to Home](../../README.md)
