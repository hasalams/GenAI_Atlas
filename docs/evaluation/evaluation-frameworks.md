# Evaluation & Testing Frameworks

[Home](../../README.md) > [Evaluation](../) > Evaluation Frameworks

> Comprehensive guide to evaluation frameworks, LLM-as-judge patterns, specialized testing tools, and benchmarking suites for assessing LLM application quality.

*Last Updated: April 18, 2026*

## Table of Contents
- [Evaluation Frameworks](#evaluation-frameworks)
- [LLM-as-Judge Patterns](#llm-as-judge-patterns)
- [Specialized Testing](#specialized-testing)
- [Benchmarking Suites](#benchmarking-suites)
- [Best Practices](#best-practices)

## Evaluation Frameworks

### RAGAS (Retrieval Augmented Generation Assessment)

| Aspect | Details |
|--------|---------|
| **Version** | 0.2+ |
| **Focus** | RAG evaluation |
| **Integration** | LangChain, LlamaIndex, custom pipelines |

**Key Metrics:**
- **Faithfulness**: How grounded is the answer in retrieved context?
- **Answer Relevancy**: How relevant is the answer to the question?
- **Context Precision**: What proportion of retrieved context is relevant?
- **Context Recall**: Is all necessary information retrieved?
- **Context Relevancy**: Overall context quality assessment

**Unique Features:**
- Synthetic test data generation
- Reference-free evaluation (LLM-as-judge)
- Component-level RAG assessment
- Automated test set creation

**Best For:**
- RAG system optimization
- Retrieval quality assessment
- End-to-end RAG evaluation
- Identifying retrieval vs. generation issues

### DeepEval

| Aspect | Details |
|--------|---------|
| **Version** | 1.x+ |
| **Focus** | LLM unit testing |
| **Integration** | pytest, CI/CD pipelines |

**14+ Built-in Metrics:**
- Hallucination detection
- Toxicity scoring
- Bias measurement
- Answer relevancy
- Faithfulness
- Contextual precision/recall
- Coherence
- G-Eval (custom criteria)
- Summarization quality
- JSON correctness

**Key Features:**
- pytest integration for unit testing
- CI/CD friendly
- Custom metric creation
- Batch evaluation
- LLM-as-judge implementation

**Best For:**
- Development workflow testing
- Continuous integration
- Unit testing LLM outputs
- Regression detection

### TruLens

| Aspect | Details |
|--------|---------|
| **Version** | 1.x+ |
| **Focus** | Evaluation + observability |
| **Strength** | Real-time feedback and monitoring |

**Core Capabilities:**
- Real-time feedback collection
- Retrieval quality evaluation
- Groundedness scoring
- Custom feedback functions
- Dashboard visualization

**Evaluation Types:**
- **Groundedness**: Is output supported by context?
- **Answer Relevance**: Does output address the query?
- **Context Relevance**: Is retrieved context useful?
- **Custom Feedback**: User-defined evaluation functions

**Best For:**
- Production monitoring
- Real-time quality assessment
- RAG system observability
- Iterative improvement workflows

### PromptFoo

| Aspect | Details |
|--------|---------|
| **Type** | CLI evaluation tool |
| **Focus** | Prompt testing and optimization |

**Key Features:**
- CLI-based evaluation
- Regression testing for prompts
- Red-teaming capabilities
- A/B testing support
- Multiple provider support

**Evaluation Modes:**
- Deterministic assertions
- LLM-as-judge scoring
- Semantic similarity
- Exact match testing
- Custom JavaScript evaluators

**Best For:**
- Prompt engineering workflows
- Version control for prompts
- Adversarial testing
- Development iteration

### LangChain Evaluators

| Evaluator Type | Purpose |
|----------------|---------|
| **String Evaluators** | Exact match, regex, embedding distance |
| **Trajectory Evaluators** | Agent action sequences |
| **Comparison Evaluators** | Pairwise output comparison |
| **Custom Evaluators** | User-defined evaluation logic |

**Integration Strengths:**
- Native LangChain compatibility
- Dataset management via LangSmith
- Prompt versioning
- Automated evaluation runs

### OpenAI Evals

| Aspect | Details |
|--------|---------|
| **Type** | Benchmark framework |
| **Community** | Growing contribution base |
| **Use Cases** | Research, model development |

**Features:**
- Template-based eval creation
- Model comparison framework
- Community-contributed benchmarks
- Reproducible evaluation

## LLM-as-Judge Patterns

### Overview

LLM-as-judge uses powerful language models to evaluate the quality of outputs from other LLMs, providing scalable evaluation for subjective tasks.

### Pattern 1: GPT-4 / Claude as Judge

**Use Cases:**
- Open-ended generation quality
- Creative writing assessment
- Subjective task evaluation
- Nuanced quality scoring

**Implementation:**
```markdown
Evaluation Prompt Structure:
1. Task description and criteria
2. Original input/question
3. Model output to evaluate
4. Scoring rubric (1-5 or 1-10)
5. Request for reasoning + score
```

**Best Practices:**
- Provide clear evaluation criteria
- Use consistent scoring rubrics
- Include reasoning requirement
- Validate against human judgments

### Pattern 2: Pairwise Comparison

**Methodology:**
- Present two outputs side-by-side
- Ask judge to select better output
- Aggregate across many comparisons
- Compute win rates or ELO scores

**Advantages:**
- Easier than absolute scoring
- More consistent judgments
- Less score inflation
- Aligns with human preferences

### Pattern 3: Rubric-Based Scoring

**Components:**
- Clear criteria (e.g., accuracy, helpfulness, conciseness)
- Point scales for each criterion
- Weighted aggregation
- Detailed reasoning requirement

**Example Criteria:**
- Factual Accuracy (0-10)
- Relevance to Query (0-10)
- Clarity of Explanation (0-10)
- Completeness (0-10)

### Pattern 4: Chain-of-Thought Evaluation

**Process:**
1. Ask judge to think step-by-step
2. Analyze each evaluation criterion
3. Provide reasoning for each score
4. Give final aggregated score

**Benefits:**
- More explainable judgments
- Catches subtle issues
- Reduces evaluation errors
- Provides actionable feedback

### Pattern 5: Synthetic Data Generation

**Applications:**
- Creating test datasets
- Generating edge cases
- Producing golden answer sets
- Building evaluation benchmarks

**RAGAS Approach:**
- Generate questions from documents
- Create ground truth answers
- Produce distractor context
- Build comprehensive test sets

## Specialized Testing

### Giskard

| Aspect | Details |
|--------|---------|
| **Focus** | ML testing and vulnerability scanning |
| **Capabilities** | Adversarial testing, model debugging |

**Features:**
- Automated vulnerability detection
- Adversarial test generation
- Performance profiling
- Bias detection
- Model debugging tools

### LLM Guard

| Aspect | Details |
|--------|---------|
| **Focus** | Security testing |
| **Open Source** | Yes |

**Detection Capabilities:**
- Prompt injection attempts
- PII leakage
- Jailbreak attempts
- Malicious outputs
- Toxicity scanning

### Rebuff

| Aspect | Details |
|--------|---------|
| **Type** | Prompt injection defense API |
| **Deployment** | Cloud service |

**Features:**
- Real-time injection detection
- Heuristic + ML detection
- API-based integration
- Low latency checks

### Inspect AI

| Aspect | Details |
|--------|---------|
| **Provider** | Anthropic |
| **Focus** | Safety and capability evaluation |

**Evaluation Areas:**
- Safety red-teaming
- Capability assessment
- Alignment testing
- Robustness evaluation

## Benchmarking Suites

### LM Evaluation Harness

| Aspect | Details |
|--------|---------|
| **Benchmarks** | 200+ standardized tasks |
| **Provider** | EleutherAI |
| **Use** | Research and development |

**Coverage:**
- Language understanding
- Reasoning
- Knowledge
- Math
- Code generation
- Common sense

**Strengths:**
- Standardized evaluation
- Reproducible results
- Wide model support
- Active maintenance

### BigBench

| Aspect | Details |
|--------|---------|
| **Tasks** | 200+ diverse tasks |
| **Provider** | Google |
| **Focus** | Challenging, diverse capabilities |

**Task Categories:**
- Linguistic understanding
- Logical reasoning
- Mathematics
- Common sense
- Social intelligence
- Multimodal reasoning

### HELM (Holistic Evaluation of Language Models)

| Dimension | Metrics |
|-----------|---------|
| **Accuracy** | Task-specific performance |
| **Calibration** | Confidence-accuracy alignment |
| **Robustness** | Performance under perturbations |
| **Fairness** | Demographic representation and bias |
| **Efficiency** | Compute and cost metrics |

**Stanford Framework:**
- Multi-dimensional assessment
- Transparency in evaluation
- Reproducible methodology
- Comprehensive reporting

### MTEB (Massive Text Embedding Benchmark)

| Aspect | Details |
|--------|---------|
| **Focus** | Embedding model evaluation |
| **Tasks** | 8 task types, 56 datasets |

**Task Types:**
- Classification
- Clustering
- Pair classification
- Reranking
- Retrieval
- Semantic textual similarity
- Summarization
- BitextMining

**Leaderboard:**
- Standardized scoring
- Model comparison
- Regular updates
- Community contributions

## Best Practices

### Evaluation Strategy

1. **Multi-Level Evaluation**
   - Unit tests for components
   - Integration tests for workflows
   - End-to-end system tests
   - User acceptance testing

2. **Continuous Evaluation**
   - CI/CD integration
   - Regression detection
   - Performance tracking over time
   - A/B testing in production

3. **Domain-Specific Metrics**
   - Define custom evaluation criteria
   - Collect domain expert feedback
   - Build custom test sets
   - Validate against business KPIs

4. **Balance Automation & Human Review**
   - Automated screening for basic quality
   - Human evaluation for edge cases
   - Regular calibration with human judgments
   - Periodic gold standard updates

### Metric Selection

**For RAG Systems:**
- RAGAS metrics (faithfulness, relevancy)
- Retrieval precision/recall
- Context quality scores
- End-to-end answer quality

**For Generative Tasks:**
- LLM-as-judge scoring
- Human preference ratings
- Pairwise comparisons
- Task-specific accuracy

**For Safety:**
- Toxicity detection
- Bias measurement
- PII leakage checks
- Jailbreak resistance

### Cost Management

- Use smaller judge models for simple tasks
- Cache evaluation results
- Batch evaluations
- Sample strategically rather than exhaustive testing
- Use deterministic checks before expensive LLM evaluation

## Related Resources
- [Leaderboards](./leaderboards.md) - Public benchmarks and model rankings
- [Observability](../operations/observability.md) - Production monitoring and tracing
- [Guardrails](../development/guardrails.md) - Safety and validation frameworks
- [Production Checklist](../operations/production-checklist.md) - Deployment best practices

---

[🏠 Back to Home](../../README.md)
