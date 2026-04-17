# Prompt Engineering

[Home](../../README.md) > [Development](../) > Prompt Engineering

> Comprehensive guide to prompt engineering techniques, patterns, tools, and best practices for optimizing LLM performance.

*Last Updated: April 18, 2026*

## Table of Contents
- [Core Techniques](#core-techniques)
- [Advanced Patterns](#advanced-patterns)
- [Tools & Libraries](#tools--libraries)
- [Best Practices](#best-practices)

## Core Techniques

### Few-Shot Learning

**Concept:** Provide examples within the prompt to guide the model's behavior.

**When to Use:**
- Task specification without fine-tuning
- Demonstrating output format
- Establishing tone and style
- Complex reasoning patterns

**Example Structure:**
```
Task: Classify sentiment

Example 1:
Input: "I love this product!"
Output: Positive

Example 2:
Input: "This is terrible."
Output: Negative

Example 3:
Input: "It's okay, nothing special."
Output: Neutral

Now classify:
Input: "Best purchase ever!"
Output: ?
```

**Best Practices:**
- Use 3-5 diverse examples
- Include edge cases
- Maintain consistent formatting
- Order examples strategically (last example often most influential)

### Zero-Shot Prompting

**Concept:** Direct instruction without examples, relying on model's pre-trained knowledge.

**When to Use:**
- Simple, well-defined tasks
- Minimizing token usage
- Tasks the model already understands well
- Quick prototyping

**Example:**
```
Summarize the following text in 2-3 sentences:
[text]
```

**Strengths:**
- Token efficient
- Fast to implement
- Works well for common tasks

**Limitations:**
- Less control over output format
- May require iteration on instruction clarity

### Chain-of-Thought (CoT)

**Concept:** Encourage step-by-step reasoning before providing the final answer.

**Key Phrase:** "Let's think step by step"

**When to Use:**
- Mathematical problems
- Logical reasoning tasks
- Multi-step planning
- Complex decision-making

**Example:**
```
Question: If a train travels 60 miles per hour for 2.5 hours, how far does it travel?

Let's think step by step:
1. Speed = 60 miles per hour
2. Time = 2.5 hours
3. Distance = Speed × Time
4. Distance = 60 × 2.5 = 150 miles

Answer: 150 miles
```

**Effectiveness:**
- Significant improvement on reasoning tasks
- More interpretable outputs
- Better error detection
- Enhanced accuracy on complex problems

### Self-Consistency

**Concept:** Generate multiple reasoning paths and select the most consistent answer.

**Implementation:**
1. Generate N different reasoning chains (e.g., 5-10)
2. Extract final answers from each
3. Select the majority vote answer

**When to Use:**
- High-stakes decisions
- Uncertainty quantification
- Robustness to reasoning errors
- Tasks with single correct answer

**Benefits:**
- Improved accuracy (5-20% on reasoning tasks)
- Confidence estimation
- Error mitigation

**Trade-offs:**
- Higher computational cost (N× tokens)
- Increased latency

## Advanced Patterns

### ReAct (Reasoning and Acting)

**Concept:** Interleave reasoning traces with actions and observations.

**Pattern:**
```
Thought: I need to find information about X
Action: search("X")
Observation: [search results]
Thought: Based on the results, I should...
Action: calculate(...)
Observation: [calculation result]
Thought: Now I can conclude...
Answer: [final answer]
```

**Use Cases:**
- Agentic systems
- Tool-using applications
- Multi-step workflows
- Research and analysis tasks

**Implementation:**
- Frameworks: LangGraph, AutoGen, CrewAI
- Requires function calling or tool use
- Iterative thought-action-observation loops

### Tree of Thoughts (ToT)

**Concept:** Explore multiple reasoning paths in a tree structure, backtracking when needed.

**Process:**
1. Generate multiple next thoughts
2. Evaluate each thought
3. Select most promising paths
4. Explore further or backtrack
5. Aggregate or select best solution

**When to Use:**
- Optimization problems
- Game playing
- Creative tasks requiring exploration
- Problems with multiple valid approaches

**Trade-offs:**
- Very high computational cost
- Complex implementation
- Best for high-value decisions

### Reflexion

**Concept:** Self-reflection and iterative improvement based on feedback.

**Process:**
1. Generate initial output
2. Evaluate output against criteria
3. Reflect on shortcomings
4. Generate improved output
5. Repeat until satisfactory

**Applications:**
- Code generation with testing
- Writing with quality checks
- Problem-solving with validation
- Iterative refinement workflows

**Example:**
```
Attempt 1: [initial code]
Test Result: Failed on edge case X
Reflection: Need to handle empty input
Attempt 2: [improved code with edge case handling]
Test Result: Success
```

### Prompt Compression

**Concept:** Reduce token usage while maintaining quality and meaning.

**Techniques:**

1. **Remove Redundancy**
   - Eliminate repeated instructions
   - Consolidate similar examples
   - Use concise language

2. **Use Abstractions**
   - Reference learned concepts
   - Leverage model's prior knowledge
   - Minimize example verbosity

3. **Structured Formats**
   - Use bullet points over prose
   - Employ abbreviations consistently
   - Leverage formatting (bold, headers)

**Tools:**
- LLMLingua: Automated prompt compression
- Manual optimization through testing

**Benefits:**
- Lower costs (fewer input tokens)
- Faster response times
- Can fit more context within limits

### Instruction Hierarchy

**Concept:** Structure prompts with clear priority levels.

**Pattern:**
```
# Primary Objective
[Core task]

## Critical Constraints
- Must adhere to X
- Never do Y

## Preferences
- Prefer format A
- Aim for style B

## Context
[Background information]
```

**Benefits:**
- Clear priority for the model
- Reduced instruction conflicts
- Better adherence to critical requirements

## Tools & Libraries

### LangChain Prompts

**Features:**
- Template system with variable substitution
- Example selectors (similarity-based, length-based)
- Prompt composition and chaining
- Versioning and tracking

**Use Cases:**
- Rapid prototyping
- Dynamic prompt generation
- Complex prompt logic

**Example:**
```python
from langchain.prompts import PromptTemplate

template = "Translate {text} from {source_lang} to {target_lang}"
prompt = PromptTemplate(template=template, 
                       input_variables=["text", "source_lang", "target_lang"])
```

### DSPy

**Concept:** Programming framework for prompting and fine-tuning.

**Key Features:**
- Declarative prompt specification
- Automatic optimization
- Compile-time prompt tuning
- Metric-driven optimization

**Philosophy:**
- Prompts as programs
- Automatic prompt engineering
- Data-driven optimization

**When to Use:**
- Systematic prompt optimization
- Multi-stage pipelines
- Research and experimentation

### Guidance

**Provider:** Microsoft

**Features:**
- Constrained generation
- Structured outputs (JSON, XML)
- Control flow in prompts
- Guaranteed format compliance

**Use Cases:**
- Structured data extraction
- API response generation
- Format-critical applications

**Example:**
```python
from guidance import models, gen

model = models.OpenAI("gpt-4")
result = model + "Generate JSON: " + gen("output", regex=r'\{.*\}')
```

### LMQL

**Concept:** Query language for LLM interaction.

**Features:**
- SQL-like syntax for LLM queries
- Constraints on generation
- Type safety
- Composable queries

**Example:**
```
"Classify sentiment: {text}
Sentiment:[CHOICE(['positive', 'negative', 'neutral'])]"
```

**Benefits:**
- Declarative specification
- Guaranteed output constraints
- Easy composition

## Best Practices

### Prompt Design Principles

1. **Be Specific and Clear**
   - Avoid ambiguity
   - Define terms if necessary
   - Specify output format explicitly

2. **Use Delimiters**
   - Separate instructions from content
   - Use triple quotes, XML tags, or markers
   - Prevents prompt injection

3. **Specify Output Format**
   - JSON schema
   - Example output
   - Step-by-step structure

4. **Provide Context**
   - Relevant background information
   - Role or persona
   - Constraints and requirements

5. **Test Iteratively**
   - Start simple, add complexity
   - Test edge cases
   - A/B test variations

### Prompt Iteration Workflow

1. **Initial Draft**
   - Write clear instructions
   - Minimal example if needed

2. **Test on Examples**
   - Run on diverse inputs
   - Identify failure modes

3. **Refine Instructions**
   - Add clarifications for failures
   - Provide edge case examples
   - Adjust tone or style

4. **Optimize for Cost/Quality**
   - Remove unnecessary tokens
   - Balance example count
   - Test compression techniques

5. **Version Control**
   - Track prompt changes
   - Document performance impact
   - A/B test in production

### Common Pitfalls

**Pitfall 1: Over-Prompting**
- Including unnecessary detail
- Too many examples
- Redundant instructions

**Solution:** Start minimal, add only what improves results

**Pitfall 2: Ambiguous Instructions**
- Vague requirements
- Undefined terms
- Multiple interpretations

**Solution:** Be explicit, use examples, test with others

**Pitfall 3: Ignoring Model Limitations**
- Asking for real-time data
- Assuming specific knowledge cutoff
- Expecting perfect factual accuracy

**Solution:** Understand model capabilities, use tools/retrieval when needed

**Pitfall 4: Poor Example Selection**
- Examples not representative
- Too similar to each other
- Wrong difficulty level

**Solution:** Diverse, representative examples covering edge cases

**Pitfall 5: No Prompt Versioning**
- Ad-hoc changes without tracking
- No A/B testing
- Cannot reproduce previous behavior

**Solution:** Version control, systematic testing, performance tracking

### Evaluation Strategy

1. **Define Success Metrics**
   - Task-specific accuracy
   - Output format compliance
   - Response quality scores

2. **Create Test Sets**
   - Representative examples
   - Edge cases
   - Known failure modes

3. **Automate Testing**
   - CI/CD integration
   - Regression detection
   - Performance benchmarks

4. **A/B Test Changes**
   - Compare prompt variations
   - Measure impact on metrics
   - Statistical significance testing

### Model-Specific Considerations

**Claude (Anthropic):**
- Prefers XML tags for structure
- Strong at following complex instructions
- Excellent at long-context tasks
- Use clear section headers

**GPT-4 (OpenAI):**
- Good at following detailed instructions
- Strong tool use and function calling
- Benefits from system messages
- JSON mode for structured outputs

**Gemini (Google):**
- Native multimodal understanding
- Extreme long context (1M-2M tokens)
- Good at video understanding
- Clear visual references

**Open Source Models:**
- May require more explicit instructions
- Chat templates vary by model
- Test system message effectiveness
- Some benefit from specific prompt formats

## Advanced Topics

### Prompt Injection Prevention

**Techniques:**
1. Use delimiters to separate instructions from user input
2. Validate and sanitize inputs
3. Use instruction hierarchy (critical rules first)
4. Implement output validation
5. Monitor for adversarial patterns

### Multilingual Prompting

**Best Practices:**
- Specify language explicitly
- Provide examples in target language
- Be aware of translation quality
- Test across languages
- Consider language-specific models (Qwen, Cohere)

### Prompt Optimization at Scale

**Approaches:**
1. **Manual Iteration**: Human-in-the-loop refinement
2. **DSPy Optimization**: Automated prompt tuning
3. **Reinforcement Learning**: RLHF-style prompt optimization
4. **Ensemble Methods**: Combine multiple prompt strategies
5. **Meta-Prompting**: Use LLMs to improve prompts

## Related Resources
- [Text Models](../models/text-models.md) - Model capabilities and selection
- [Agentic Systems](../frameworks/agentic-systems.md) - ReAct and tool use patterns
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Testing prompt performance
- [Observability](../operations/observability.md) - Monitoring prompt performance
- [Guardrails](./guardrails.md) - Safety and validation

---

[🏠 Back to Home](../../README.md)
