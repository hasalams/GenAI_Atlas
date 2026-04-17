# Observability & Monitoring

[Home](../../README.md) > [Operations](../) > Observability & Monitoring

> Comprehensive guide to observability platforms, monitoring tools, and key metrics for production LLM applications.

*Last Updated: April 18, 2026*

## Table of Contents
- [LLM Observability Platforms](#llm-observability-platforms)
- [Production Monitoring Tools](#production-monitoring-tools)
- [Key Metrics to Track](#key-metrics-to-track)
- [Implementation Best Practices](#implementation-best-practices)

## LLM Observability Platforms

### OpenTelemetry

| Aspect | Details |
|--------|---------|
| **Type** | Industry standard |
| **Status** | Production-ready |
| **Key Feature** | Vendor-neutral observability |

**Semantic Conventions:**
- `gen_ai.*` namespace for LLM operations
- Standardized span attributes
- Token usage tracking
- Model identification
- Provider attribution

**Integration Benefits:**
- Framework-agnostic
- Cross-platform compatibility
- Unified tracing across services
- Vendor-neutral data collection
- Rich ecosystem support

**Best For:**
- Multi-vendor LLM deployments
- Microservices architectures
- Enterprise observability standards
- Integration with existing APM tools

### LangFuse

| Aspect | Details |
|--------|---------|
| **Version** | v3 |
| **Type** | Comprehensive LLM observability platform |
| **Deployment** | Cloud or self-hosted |

**Core Capabilities:**
- **Trace Analysis**: Complete request lifecycle tracking
- **Prompt Versioning**: Track and compare prompt variations
- **A/B Testing**: Compare model and prompt performance
- **Cost Tracking**: Token usage and cost per request/user
- **Feedback Loops**: Collect and analyze user feedback
- **Datasets**: Curate test sets from production data

**Advanced Features:**
- Prompt playground for experimentation
- Automated prompt optimization suggestions
- User session tracking
- Quality score aggregation
- Export to CSV/JSON for analysis

**Best For:**
- Comprehensive LLM observability
- Prompt engineering workflows
- Cost optimization
- Quality monitoring
- Production debugging

### LangSmith

| Aspect | Details |
|--------|---------|
| **Provider** | LangChain |
| **Type** | End-to-end LLM platform |
| **Integration** | Native LangChain support |

**Key Features:**
- **End-to-End Tracing**: Complete chain execution visibility
- **Dataset Curation**: Build test sets from production
- **Playground**: Interactive prompt testing
- **Automated Optimization**: Prompt improvement suggestions
- **Production Guardrails**: Safety and quality gates

**Evaluation Capabilities:**
- Online and offline evaluation
- Custom evaluator support
- Automated regression testing
- Comparison views

**Best For:**
- LangChain applications
- Development to production workflows
- Dataset management
- Prompt optimization

### Weights & Biases (W&B)

| Aspect | Details |
|--------|---------|
| **Focus** | ML lifecycle + LLM features |
| **Strength** | Experiment tracking |

**LLM Features:**
- Prompt diff visualization
- Fine-tuning experiment tracking
- Model registry
- Chain execution logging
- Token usage tracking

**ML Platform Features:**
- Experiment comparison
- Hyperparameter tracking
- Model versioning
- Artifact management
- Team collaboration

**Best For:**
- ML teams with existing W&B usage
- Fine-tuning workflows
- Experiment tracking
- Model versioning
- Research to production

### Arize AI

| Aspect | Details |
|--------|---------|
| **Type** | ML monitoring + RAG evaluation |
| **Strength** | Drift detection and embeddings |

**Core Capabilities:**
- **Drift Detection**: Model performance degradation
- **Embedding Visualization**: UMAP/t-SNE for vector analysis
- **Retrieval Analysis**: RAG system evaluation
- **Hallucination Detection**: Groundedness scoring
- **Root Cause Analysis**: Automated issue detection

**RAG-Specific Features:**
- Retrieval quality metrics
- Context relevance scoring
- Retrieved document analysis
- Reranking performance

**Best For:**
- RAG system monitoring
- Embedding quality analysis
- Production ML monitoring
- Drift detection

### Phoenix (Arize OSS)

| Aspect | Details |
|--------|---------|
| **Type** | Open-source observability |
| **Deployment** | Local-first |

**Features:**
- Local trace visualization
- Embedding analysis
- LLM trace inspection
- Zero-config setup
- OpenTelemetry compatible

**Best For:**
- Development environments
- Open-source preference
- Local-first workflows
- Cost-sensitive projects

## Production Monitoring Tools

### Prometheus + Grafana

**Use Case:** Time series monitoring with custom dashboards

**Key Metrics:**
- Request rate and throughput
- Error rates by type
- Token usage over time
- Cost per endpoint
- P50/P90/P99 latency
- Cache hit rates

**Dashboard Components:**
- Real-time request monitoring
- Cost tracking
- Error analysis
- Performance trends
- Capacity planning

### Datadog

**Features:**
- Cloud monitoring with LLM integrations
- APM (Application Performance Monitoring)
- Log aggregation and analysis
- Custom metrics and dashboards
- Alerting and incident management

**LLM Integration:**
- Token usage tracking
- Model performance metrics
- Cost attribution
- Distributed tracing

### New Relic

**Features:**
- Application performance monitoring
- Distributed tracing
- Error tracking
- Custom dashboards
- Alert management

**LLM Capabilities:**
- Request tracing
- Performance analysis
- Error rate monitoring
- Custom event tracking

### Elastic Stack (ELK)

**Components:**
- Elasticsearch: Log storage and search
- Logstash: Log processing
- Kibana: Visualization and dashboards

**Use Cases:**
- Log aggregation
- Full-text search
- Pattern detection
- Alerting
- Audit trails

## Key Metrics to Track

### Cost Metrics

**Per-Request Metrics:**
- Tokens used (input + output)
- Cost per request
- Model used
- Provider costs
- Cache savings

**Aggregated Metrics:**
- Cost per user
- Cost per session
- Cost per feature
- Daily/weekly/monthly spend
- Cost trends over time

**Optimization Indicators:**
- Cache hit rate
- Token efficiency
- Model selection effectiveness
- Prompt length trends

### Latency Metrics

**Core Latency Metrics:**
- **TTFT (Time to First Token)**: Critical for streaming
- **Token Throughput**: Tokens per second
- **Total Latency**: End-to-end response time
- **P50/P90/P99**: Percentile latencies

**Component Latency:**
- Retrieval time (RAG systems)
- Reranking latency
- Tool execution time
- Model inference time
- Network overhead

**User Experience:**
- Interactive response threshold (< 2s)
- Streaming perception (fast TTFT)
- Batch processing efficiency

### Quality Metrics

**Automated Metrics:**
- LLM-as-judge scores
- Faithfulness scores (RAG)
- Answer relevancy
- Context precision/recall
- Hallucination rate estimates

**User Feedback:**
- Thumbs up/down rates
- Explicit quality ratings
- User corrections
- Session abandonment
- Retry patterns

**A/B Testing:**
- Preference win rate
- Task completion rate
- User satisfaction scores
- Engagement metrics

### Reliability Metrics

**Error Tracking:**
- Error rate by type
- Rate limit hits
- Timeout frequency
- Provider downtime
- Fallback activation rate

**Retry Patterns:**
- Retry attempts per request
- Retry success rate
- Exponential backoff effectiveness
- Circuit breaker activations

**Availability:**
- System uptime
- Provider availability
- Service degradation events
- Graceful degradation success

### Retrieval Metrics (RAG Systems)

**Retrieval Quality:**
- Precision@K
- Recall@K
- MRR (Mean Reciprocal Rank)
- NDCG (Normalized Discounted Cumulative Gain)

**Performance:**
- Retrieval latency
- Index size
- Query throughput
- Reranking latency

**Context Quality:**
- Relevance scores
- Context length used
- Documents retrieved
- Reranking impact

## Implementation Best Practices

### Day One Observability

**Essential Setup:**
1. **Distributed Tracing**: OpenTelemetry or LangFuse from start
2. **Cost Tracking**: Token usage per request with attribution
3. **Latency Monitoring**: P99 latency alerts
4. **Error Tracking**: Structured error logging
5. **Basic Dashboards**: Request volume, cost, latency, errors

### Instrumentation Patterns

**Trace Structure:**
```
User Request
├─ Prompt Construction
├─ Context Retrieval (RAG)
│  ├─ Embedding Generation
│  ├─ Vector Search
│  └─ Reranking
├─ LLM Call
│  ├─ Token Count
│  ├─ Cost Calculation
│  └─ Latency Measurement
└─ Response Processing
```

**Span Attributes:**
- User ID / Session ID
- Model used
- Token counts (input/output)
- Cost
- Latency
- Quality scores
- Error information

### Alerting Strategy

**Critical Alerts:**
- P99 latency > SLA threshold
- Error rate > 5%
- Cost spike > 50% increase
- Provider downtime
- Quality score drop > 20%

**Warning Alerts:**
- P90 latency trending up
- Cache hit rate declining
- Token usage increasing
- Specific error patterns

### Dashboard Design

**Executive Dashboard:**
- Daily cost trends
- User growth
- Quality score averages
- System uptime

**Engineering Dashboard:**
- Request throughput
- Error rates by type
- Latency distributions
- Cache performance

**Operations Dashboard:**
- Current error rate
- Active incidents
- Provider health
- Resource utilization

### Privacy Considerations

**PII Protection:**
- Redact user inputs in traces
- Hash user identifiers
- Comply with GDPR/CCPA
- Implement data retention policies

**Security:**
- Encrypted storage
- Access controls
- Audit logging
- Compliance reporting

## Integration Examples

### OpenTelemetry + LangChain

- Automatic span creation for chains
- Token tracking
- Cost attribution
- Error propagation

### LangFuse + CrewAI

- Multi-agent trace visualization
- Agent-level cost tracking
- Conversation flow analysis
- Performance per agent

### W&B + Fine-Tuning

- Training metrics
- Validation loss
- Model checkpoints
- Hyperparameter tracking

## Related Resources
- [Production Checklist](./production-checklist.md) - Deployment requirements
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Quality assessment tools
- [Agentic Systems](../frameworks/agentic-systems.md) - Multi-agent observability
- [Getting Started Guide](../guides/getting-started.md) - Implementation guidance

---

[🏠 Back to Home](../../README.md)
