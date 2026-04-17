# Production Checklist

[Home](../../README.md) > [Operations](../) > Production Checklist

> Essential requirements and best practices for deploying LLM applications to production with confidence.

*Last Updated: April 18, 2026*

## Table of Contents
- [Day One Requirements](#day-one-requirements)
- [Production Checklist](#production-checklist)
- [Deployment Strategies](#deployment-strategies)
- [Best Practices](#best-practices)
- [Common Pitfalls](#common-pitfalls)

## Day One Requirements

Before deploying any LLM application to production, ensure these foundational elements are in place:

### ✅ Observability

**Distributed Tracing:**
- OpenTelemetry integration for request tracing
- End-to-end visibility from user request to LLM response
- Span attributes for model, tokens, cost, latency
- Integration with observability platform (LangFuse, LangSmith, etc.)

**Cost Tracking:**
- Per-request token usage (input + output)
- Cost calculation per request
- Cost attribution by user/session/feature
- Budget alerts and thresholds
- Daily/weekly/monthly reporting

**Latency Monitoring:**
- Time to First Token (TTFT) for streaming
- Total response time
- P50/P90/P99 percentile tracking
- Component-level latency breakdown (retrieval, inference, etc.)
- SLA monitoring and alerts

**Logging:**
- Structured logging with request IDs
- Error tracking with stack traces
- Model inputs/outputs (with PII redaction)
- Tool calls and results (for agentic systems)

### ✅ Evaluation

**Domain-Specific Benchmarks:**
- Custom test sets for your specific use case
- Representative edge cases
- Known failure modes
- Regular regression testing

**Human Feedback Loops:**
- Thumbs up/down mechanism
- Quality ratings
- User corrections
- Session abandonment tracking
- Feedback integration into evaluation

**Automated Quality Metrics:**
- LLM-as-judge scoring
- Task-specific accuracy metrics
- Hallucination detection
- Relevance scoring (for RAG)
- Consistency checks

### ✅ Guardrails

**Input Validation:**
- Prompt injection detection
- Malicious input filtering
- Input length limits
- Rate limiting per user
- Abuse pattern detection

**Output Validation:**
- Content safety filters
- PII detection and redaction
- Toxicity screening
- Format validation (JSON, structured outputs)
- Hallucination checks

**Content Safety:**
- Multi-category safety classification
- Age-appropriate content filtering
- Brand safety checks
- Legal compliance validation

### ✅ Fallbacks

**Multiple Model Providers:**
- Primary and secondary providers configured
- Automatic failover on errors
- Provider health monitoring
- Cost-aware routing

**Graceful Degradation:**
- Fallback to simpler models on failure
- Cached responses for common queries
- Default responses for critical failures
- User-facing error messages

**Circuit Breakers:**
- Automatic provider cutoff on repeated failures
- Exponential backoff for retries
- Rate limit handling
- Timeout management

### ✅ Caching

**Prefix Caching:**
- Cache common prompt prefixes
- System messages and instructions
- Few-shot examples
- RAG context (when stable)

**Semantic Caching:**
- Cache responses for similar queries
- Embedding-based similarity matching
- TTL (time-to-live) management
- Cache invalidation strategy

**Response Caching:**
- Exact match caching for repeated queries
- User-specific cache keys
- Cache hit rate monitoring
- Cost savings tracking

## Production Checklist

Use this comprehensive checklist before deploying to production:

### Infrastructure & Deployment

- [ ] **Scalability**: Can handle 10x current traffic without degradation
- [ ] **Load Balancing**: Traffic distributed across multiple instances
- [ ] **Auto-Scaling**: Automatic scaling based on demand
- [ ] **Container Orchestration**: Kubernetes or equivalent for management
- [ ] **Database**: Production-grade database for state/history
- [ ] **Secrets Management**: Secure API key storage (Vault, AWS Secrets Manager)
- [ ] **CI/CD Pipeline**: Automated testing and deployment
- [ ] **Blue-Green Deployment**: Zero-downtime deployment strategy
- [ ] **Rollback Plan**: Quick rollback mechanism in place

### Monitoring & Observability

- [ ] **Cost per query/user tracked and within budget**
- [ ] **P99 latency < 2 seconds for interactive use** (or defined SLA)
- [ ] **Error rate < 1%** with alerting
- [ ] **Uptime monitoring** with SLA targets (99.9%+)
- [ ] **Dashboard for stakeholders** (cost, quality, usage)
- [ ] **On-call rotation** defined and documented
- [ ] **Runbooks** for common incidents
- [ ] **Alert fatigue management** (meaningful alerts only)

### Quality & Safety

- [ ] **Hallucination detection and scoring in place**
- [ ] **Content safety filters active** (toxicity, bias, etc.)
- [ ] **PII detection and redaction** implemented
- [ ] **Prompt injection defense** tested
- [ ] **Output validation** for format and content
- [ ] **Quality score above baseline** (defined threshold)
- [ ] **Regular evaluation on holdout datasets**
- [ ] **A/B testing framework** for improvements
- [ ] **Safety guardrails tested against adversarial inputs**

### Development & Iteration

- [ ] **Prompt versioning** system in place
- [ ] **A/B testing framework** for prompts and models
- [ ] **Feature flags** for gradual rollout
- [ ] **Dataset management** for train/test/validation
- [ ] **Model version tracking** in production
- [ ] **Evaluation pipeline** for new versions
- [ ] **Feedback collection mechanism** (user ratings, corrections)

### Security & Compliance

- [ ] **API authentication** implemented (API keys, OAuth)
- [ ] **Rate limiting** per user/API key
- [ ] **Audit logging** for compliance
- [ ] **Data retention policy** defined and implemented
- [ ] **GDPR/CCPA compliance** (if applicable)
- [ ] **PII handling procedures** documented
- [ ] **Security review** completed
- [ ] **Penetration testing** for prompt injection and jailbreaks
- [ ] **Terms of Service** and acceptable use policy

### Cost Management

- [ ] **Budget alerts** at 50%, 75%, 90% thresholds
- [ ] **Per-user cost limits** to prevent abuse
- [ ] **Cost attribution** by feature/endpoint
- [ ] **Optimization opportunities** identified (caching, model selection)
- [ ] **ROI tracking** for business justification
- [ ] **Cost forecasting** based on growth projections

### Incident Response

- [ ] **Incident response plan** documented
- [ ] **Contact list** for escalations
- [ ] **Provider status monitoring** (OpenAI, Anthropic, etc.)
- [ ] **Communication templates** for outages
- [ ] **Post-mortem process** defined
- [ ] **Regular fire drills** conducted
- [ ] **Status page** for users (if applicable)

## Deployment Strategies

### Production Cloud

**Recommended Stack:**
- **Inference**: vLLM 0.6+ with PagedAttention and prefix caching
- **Observability**: OpenTelemetry + LangFuse for comprehensive monitoring
- **Evaluation**: RAGAS + DeepEval for continuous quality assessment
- **Guardrails**: Guardrails AI or NeMo Guardrails for safety
- **Load Balancing**: NGINX or cloud-native load balancers
- **Orchestration**: Kubernetes for container management

**Architecture:**
- Multiple availability zones for redundancy
- CDN for static assets and caching
- Message queues for async processing
- Distributed tracing across services
- Centralized logging and monitoring

### Local/On-Premise

**Recommended Stack:**
- **Serving**: Ollama (simple) or llama.cpp (optimized)
- **Quantization**: GGUF Q5_K_M for quality, AWQ 4-bit for speed
- **Hardware**: Apple Silicon (Metal), NVIDIA (CUDA), AMD (ROCm)
- **Models**: Llama 3.3 70B, Qwen 2.5 72B, Phi-4 14B
- **Monitoring**: Prometheus + Grafana

**Considerations:**
- Hardware capacity planning
- Model update procedures
- Local fallback strategies
- Offline operation requirements

### Hybrid Deployment

**Strategy:**
- On-premise for sensitive data
- Cloud for scale and redundancy
- Edge for low-latency requirements
- Consistent API across environments

## Best Practices

### Performance Optimization

1. **Caching Strategy**
   - Implement semantic caching for similar queries
   - Use prefix caching for repeated prompts
   - Cache embeddings for RAG systems
   - Monitor cache hit rates

2. **Latency Reduction**
   - Enable streaming for better perceived performance
   - Use speculative decoding where available
   - Optimize prompt length
   - Parallel tool calls when possible

3. **Cost Optimization**
   - Use smaller models for simple tasks
   - Implement prompt compression
   - Cache aggressively
   - Monitor and optimize token usage

### Quality Assurance

1. **Continuous Evaluation**
   - Run automated evaluations daily
   - Track quality metrics over time
   - A/B test improvements
   - Regular human review sampling

2. **Regression Prevention**
   - Golden dataset for critical paths
   - Automated regression tests in CI/CD
   - Performance benchmarks
   - Quality thresholds in deployment pipeline

3. **User Feedback Integration**
   - Collect feedback systematically
   - Analyze negative feedback patterns
   - Update test sets with failure cases
   - Close feedback loop with improvements

### Safety & Compliance

1. **Defense in Depth**
   - Multiple layers of safety checks
   - Input and output validation
   - Content filtering
   - Rate limiting and abuse prevention

2. **Privacy Protection**
   - PII detection and redaction
   - Data retention policies
   - User data deletion procedures
   - Compliance with regulations

3. **Adversarial Testing**
   - Regular red-team exercises
   - Prompt injection testing
   - Jailbreak attempt detection
   - Edge case exploration

## Common Pitfalls

### Pitfall 1: Insufficient Observability

**Problem:** Deploying without proper monitoring leads to blind spots.

**Solution:** 
- Implement OpenTelemetry from day one
- Track cost, latency, quality, and errors
- Set up alerts before launch

### Pitfall 2: No Fallback Strategy

**Problem:** Single provider dependency causes complete outages.

**Solution:**
- Configure multiple providers
- Implement automatic failover
- Test fallback paths regularly

### Pitfall 3: Ignoring Cost Management

**Problem:** Costs spiral out of control in production.

**Solution:**
- Set budget alerts at multiple thresholds
- Implement per-user cost limits
- Monitor token usage trends
- Optimize regularly

### Pitfall 4: Inadequate Safety Testing

**Problem:** Adversarial inputs bypass safety measures.

**Solution:**
- Conduct red-team exercises
- Test prompt injection defenses
- Implement layered safety checks
- Regular security audits

### Pitfall 5: No Quality Baseline

**Problem:** Unable to detect quality degradation.

**Solution:**
- Establish quality metrics before launch
- Create golden evaluation datasets
- Track quality over time
- Set quality thresholds

### Pitfall 6: Prompt Drift

**Problem:** Prompts change without versioning, causing regressions.

**Solution:**
- Version control all prompts
- A/B test changes
- Track prompt performance
- Document prompt changes

### Pitfall 7: Over-Engineering Day One

**Problem:** Trying to solve every problem before launch.

**Solution:**
- Focus on core day-one requirements
- Iterate based on real usage
- Start simple, add complexity as needed
- Monitor and optimize post-launch

## Incident Response Framework

### Detection

- Automated alerting on SLA violations
- User-reported issues
- Monitoring dashboard anomalies
- Provider status changes

### Response

1. **Acknowledge**: Confirm incident and start timer
2. **Assess**: Determine severity and impact
3. **Mitigate**: Implement temporary fix (rollback, fallback)
4. **Communicate**: Update stakeholders and users
5. **Resolve**: Implement permanent fix
6. **Document**: Post-mortem and lessons learned

### Post-Mortem

- What happened?
- Root cause analysis
- What went well?
- What could be improved?
- Action items with owners
- Prevention measures

## Related Resources
- [Observability](./observability.md) - Monitoring and tracing implementation
- [Guardrails](../development/guardrails.md) - Safety and validation frameworks
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Quality assessment
- [Getting Started Guide](../guides/getting-started.md) - Initial implementation guidance
- [On-Premise Deployment](../infrastructure/on-premise-deployment.md) - Infrastructure setup

---

[🏠 Back to Home](../../README.md)
