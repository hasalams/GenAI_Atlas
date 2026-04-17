# Guardrails & Safety

[Home](../../README.md) > [Development](../) > Guardrails & Safety

> Comprehensive guide to safety frameworks, content moderation, and guardrails for protecting LLM applications from harmful outputs and adversarial inputs.

*Last Updated: April 18, 2026*

## Table of Contents
- [Safety Frameworks](#safety-frameworks)
- [Use Cases](#use-cases)
- [Implementation Patterns](#implementation-patterns)
- [Best Practices](#best-practices)

## Safety Frameworks

### Guardrails AI

| Aspect | Details |
|--------|---------|
| **Version** | 0.5+ |
| **Type** | Output validation and self-healing |
| **License** | Open source (Apache 2.0) |

**Key Features:**
- **50+ Validators**: Pre-built validators for common safety checks
- **Self-Healing**: Automatic re-prompting when validation fails
- **Streaming Validation**: Real-time validation during streaming
- **Custom Validators**: Easy to create domain-specific checks
- **Schema Enforcement**: Pydantic-based output structure validation

**Built-in Validators:**
- PII detection (SSN, credit cards, emails, etc.)
- Toxicity detection
- Bias detection
- Factual consistency
- Relevance scoring
- Competitor mentions
- Reading level
- URL validation
- SQL injection prevention

**Use Cases:**
- Output format enforcement (JSON, structured data)
- Content safety filters
- PII redaction
- Factual accuracy checks
- Business logic validation

**Example:**
```python
from guardrails import Guard
from guardrails.validators import DetectPII, ToxicLanguage

guard = Guard().use_many(
    DetectPII(pii_entities=["EMAIL", "SSN"]),
    ToxicLanguage(threshold=0.8)
)

validated_output = guard(
    llm_output=response,
    on_fail="reask"  # or "fix", "filter", "exception"
)
```

**Best For:**
- Output validation
- Structured data extraction
- PII protection
- Self-healing workflows

### NeMo Guardrails

| Aspect | Details |
|--------|---------|
| **Version** | 0.9+ |
| **Provider** | NVIDIA |
| **Focus** | Conversation control and flow management |

**Key Features:**
- **Colang 2.0 DSL**: Domain-specific language for conversation flows
- **Topical Rails**: Restrict conversations to allowed topics
- **Jailbreak Prevention**: Block adversarial prompts
- **Fact-Checking**: Verify outputs against knowledge base
- **Input/Output Rails**: Multi-layer protection
- **Dialog Management**: Control conversation flow

**Rail Types:**

1. **Input Rails**
   - Prompt injection detection
   - Topic filtering
   - Jailbreak prevention
   - Inappropriate content blocking

2. **Output Rails**
   - Factual accuracy checks
   - Toxicity filtering
   - Bias detection
   - Relevance validation

3. **Dialog Rails**
   - Conversation flow control
   - Topic boundaries
   - Turn management
   - Context maintenance

**Colang Example:**
```colang
define user ask about competitor
  "tell me about [competitor name]"
  "how does [competitor] compare"

define flow
  user ask about competitor
  bot inform cannot discuss competitors
```

**Best For:**
- Conversational AI applications
- Topic-restricted chatbots
- Enterprise applications with strict policies
- Complex dialog management

### LLM Guard

| Aspect | Details |
|--------|---------|
| **Type** | Security toolkit |
| **License** | Open source |
| **Focus** | Input/output security scanning |

**Detection Capabilities:**

**Input Scanners:**
- Prompt injection detection
- Jailbreak attempt identification
- Malicious input patterns
- Code injection
- SQL injection
- Toxicity pre-screening

**Output Scanners:**
- PII leakage detection
- Sensitive data exposure
- Toxicity in responses
- Bias detection
- Malicious code generation

**Features:**
- Modular scanner architecture
- Configurable thresholds
- Fast scanning (< 50ms)
- Framework agnostic
- Easy integration

**Best For:**
- Security-first applications
- Pre/post-processing pipelines
- Multi-layer defense
- Rapid security scanning

### LlamaGuard

| Aspect | Details |
|--------|---------|
| **Version** | v2+ |
| **Provider** | Meta |
| **Type** | Content safety classifier |

**Safety Categories:**
1. Violence and hate
2. Sexual content
3. Criminal planning
4. Guns and illegal weapons
5. Regulated or controlled substances
6. Self-harm
7. Misinformation (hallucinations)

**Features:**
- Multi-category risk detection
- Fine-tuned Llama model
- Fast inference
- Open weights
- Customizable categories

**Integration:**
- Pre-processing input validation
- Post-processing output filtering
- Real-time safety classification

**Best For:**
- Content moderation
- Multi-category safety
- Open-source safety solution
- Fine-tunable safety model

### Rebuff

| Aspect | Details |
|--------|---------|
| **Type** | Prompt injection defense API |
| **Deployment** | Cloud service |

**Features:**
- Real-time prompt injection detection
- Heuristic + ML detection
- Low latency (< 100ms)
- Simple API integration
- Continuously updated detection

**Detection Methods:**
1. Heuristic analysis
2. Machine learning models
3. Pattern matching
4. Anomaly detection

**Best For:**
- Production API protection
- Low-latency requirements
- Managed service preference
- Prompt injection focus

### Azure AI Content Safety

| Aspect | Details |
|--------|---------|
| **Provider** | Microsoft Azure |
| **Type** | Commercial moderation API |

**Capabilities:**
- Multi-language support
- Image and text moderation
- Custom blocklists
- Category-specific thresholds
- Real-time analysis

**Safety Categories:**
- Hate speech
- Violence
- Self-harm
- Sexual content

**Enterprise Features:**
- SLA guarantees
- Compliance certifications
- Global availability
- Azure integration

**Best For:**
- Enterprise deployments
- Azure ecosystem
- Commercial support needs
- Multi-modal moderation

### Lakera Guard

| Aspect | Details |
|--------|---------|
| **Type** | Enterprise security platform |
| **Focus** | Production-grade prompt injection defense |

**Features:**
- Advanced prompt injection detection
- Real-time threat intelligence
- Analytics dashboard
- Custom rule creation
- Incident response

**Enterprise Capabilities:**
- SOC 2 compliance
- 99.9% uptime SLA
- Dedicated support
- Custom integrations

**Best For:**
- Enterprise production systems
- High-security requirements
- Compliance needs
- Managed security solution

## Use Cases

### Use Case 1: PII Protection

**Requirement:** Prevent sensitive personal information from appearing in outputs.

**Solution Stack:**
- **Input**: LLM Guard for PII detection in user queries
- **Output**: Guardrails AI with DetectPII validator
- **Fallback**: Automatic redaction or request rejection

**Implementation:**
```python
# Input validation
if llm_guard.detect_pii(user_input):
    return "Cannot process requests containing personal information"

# Output validation
guard = Guard().use(DetectPII(pii_entities="all", on_fail="fix"))
safe_output = guard(llm_response)
```

### Use Case 2: Content Safety

**Requirement:** Filter toxic, biased, or inappropriate content.

**Solution Stack:**
- **Primary**: LlamaGuard for multi-category classification
- **Secondary**: Guardrails AI for toxicity scoring
- **Tertiary**: Azure Content Safety for compliance

**Implementation:**
1. Classify input with LlamaGuard
2. Block high-risk categories
3. Validate output with Guardrails AI
4. Log incidents for review

### Use Case 3: Topic Restriction

**Requirement:** Chatbot should only discuss specific topics (e.g., company products).

**Solution Stack:**
- **Primary**: NeMo Guardrails with Colang topic definitions
- **Secondary**: Semantic similarity checks
- **Fallback**: Polite rejection messages

**Implementation:**
```colang
define user ask off topic
  # semantic patterns for off-topic queries

define flow
  user ask off topic
  bot inform topic restriction
  bot suggest valid topics
```

### Use Case 4: Prompt Injection Defense

**Requirement:** Protect against adversarial inputs attempting to override instructions.

**Solution Stack:**
- **Real-time**: Rebuff API for fast detection
- **Deep scan**: LLM Guard for pattern analysis
- **Logging**: Track and analyze attack patterns

**Defense Layers:**
1. Input sanitization
2. Prompt injection detection
3. Instruction hierarchy (critical rules first)
4. Output validation
5. Incident logging

### Use Case 5: Structured Output Validation

**Requirement:** Ensure LLM outputs valid JSON matching a schema.

**Solution Stack:**
- **Primary**: Guardrails AI with Pydantic schema
- **Self-healing**: Automatic re-prompting on failure
- **Fallback**: Default structured response

**Implementation:**
```python
from pydantic import BaseModel
from guardrails import Guard

class OutputSchema(BaseModel):
    name: str
    age: int
    email: str

guard = Guard.from_pydantic(OutputSchema)
validated = guard(llm_output, reask_on_fail=True, max_reasks=3)
```

## Implementation Patterns

### Pattern 1: Defense in Depth

**Approach:** Multiple layers of validation at different stages.

**Layers:**
1. **Input validation**: Sanitize and validate user input
2. **Prompt engineering**: Use delimiters and instruction hierarchy
3. **Runtime monitoring**: Track for anomalies
4. **Output validation**: Check response before returning
5. **Logging**: Audit trail for incidents

**Benefits:**
- No single point of failure
- Catches different types of issues
- More robust against novel attacks

### Pattern 2: Fail-Safe Defaults

**Approach:** When validation fails, default to safe behavior.

**Strategies:**
- Return generic safe response
- Ask clarifying question
- Apologize and offer alternatives
- Log for human review

**Never:**
- Return potentially unsafe content
- Expose error details to users
- Fail silently without logging

### Pattern 3: Self-Healing

**Approach:** Automatically correct issues rather than failing.

**Techniques:**
1. **Reask**: Re-prompt LLM with validation feedback
2. **Fix**: Automatically correct minor issues (PII redaction)
3. **Filter**: Remove offending portions
4. **Fallback**: Use cached safe response

**Guardrails AI Example:**
```python
guard = Guard().use(
    validators=[ToxicLanguage(), DetectPII()],
    on_fail="reask",  # self-healing
    max_reasks=3
)
```

### Pattern 4: Progressive Validation

**Approach:** Validate incrementally during generation (streaming).

**Benefits:**
- Catch issues early
- Lower latency to first safe token
- Better user experience
- Cost savings (stop early)

**Implementation:**
- Chunk-based validation
- Real-time filtering
- Early termination on violations

### Pattern 5: Context-Aware Guardrails

**Approach:** Different validation rules based on context.

**Dimensions:**
- User role (admin vs. regular user)
- Content sensitivity (public vs. internal)
- Domain (legal, medical, general)
- Compliance requirements (HIPAA, GDPR)

**Implementation:**
```python
def get_guardrails(user_role, domain):
    if domain == "medical":
        return strict_medical_guardrails
    elif user_role == "admin":
        return relaxed_guardrails
    else:
        return standard_guardrails
```

## Best Practices

### Selection Criteria

**Choose Guardrails AI when:**
- Output validation is primary concern
- Need structured data extraction
- Self-healing is important
- Many custom validators needed

**Choose NeMo Guardrails when:**
- Building conversational AI
- Need dialog flow control
- Topic restriction is critical
- Complex conversation management

**Choose LLM Guard when:**
- Security is paramount
- Need fast input/output scanning
- Want modular, flexible system
- Open-source preference

**Choose Enterprise Solutions when:**
- Compliance requirements (SOC 2, HIPAA)
- Need SLA guarantees
- Want managed service
- Require dedicated support

### Integration Strategy

1. **Start Simple**
   - Begin with basic validation
   - Add complexity as needed
   - Test incrementally

2. **Measure Performance Impact**
   - Latency addition
   - Cost per request
   - False positive rate
   - User experience impact

3. **Monitor and Tune**
   - Track validation failures
   - Adjust thresholds
   - Update rules based on patterns
   - A/B test configurations

4. **Balance Security and Usability**
   - Avoid over-blocking
   - Provide helpful feedback
   - Allow appeals process
   - User education

### Testing Guardrails

**Red Team Testing:**
- Adversarial prompt attempts
- Jailbreak techniques
- PII leakage tests
- Toxicity probing
- Edge cases

**Regression Testing:**
- Validate against known safe inputs
- Check false positive rate
- Performance benchmarks
- User experience testing

**Continuous Monitoring:**
- Track validation failure rates
- Analyze blocked content patterns
- Monitor performance metrics
- Review false positives

### Performance Optimization

**Latency Reduction:**
1. **Parallel Validation**: Run independent validators concurrently
2. **Early Termination**: Stop on first critical failure
3. **Caching**: Cache validation results for repeated content
4. **Selective Validation**: Context-aware validator selection

**Cost Optimization:**
1. **Tiered Validation**: Fast checks first, expensive checks if needed
2. **Sampling**: Validate subset in non-critical scenarios
3. **Batch Processing**: Amortize overhead across multiple items

### Compliance Considerations

**GDPR:**
- PII detection and redaction
- Data minimization
- User consent tracking
- Right to erasure

**HIPAA:**
- PHI detection
- Encryption
- Audit logging
- Access controls

**Industry-Specific:**
- Financial services (PCI DSS)
- Legal (attorney-client privilege)
- Education (FERPA)
- Government (FedRAMP)

## Common Pitfalls

**Pitfall 1: Over-Blocking**
- Too strict thresholds
- High false positive rate
- Poor user experience

**Solution:** Tune thresholds with real data, provide feedback mechanisms

**Pitfall 2: Single Layer Defense**
- Relying on one guardrail
- No fallback
- Vulnerable to novel attacks

**Solution:** Implement defense in depth, multiple layers

**Pitfall 3: Ignoring Performance**
- Excessive latency
- Poor user experience
- Timeout issues

**Solution:** Measure impact, optimize critical paths, use async processing

**Pitfall 4: Inadequate Testing**
- Not testing adversarial inputs
- Missing edge cases
- No red team exercises

**Solution:** Regular security testing, adversarial probing, continuous monitoring

**Pitfall 5: Static Rules**
- Not updating detection patterns
- Missing new attack vectors
- Stale threat intelligence

**Solution:** Regular updates, threat monitoring, feedback loops

## Related Resources
- [Prompt Engineering](./prompt-engineering.md) - Defensive prompting techniques
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Testing guardrails
- [Production Checklist](../operations/production-checklist.md) - Deployment requirements
- [Observability](../operations/observability.md) - Monitoring validation failures

---

[🏠 Back to Home](../../README.md)
