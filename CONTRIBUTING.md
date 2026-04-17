# Contributing to GenAI_Atlas

Thank you for your interest in contributing to GenAI_Atlas! This repository serves as a comprehensive resource hub for the LLM and Generative AI community.

## How to Contribute

### 1. Types of Contributions

We welcome contributions in the following areas:

- **New Tools & Frameworks**: Add newly released tools to relevant categories
- **Version Updates**: Update model versions, framework releases, benchmark scores
- **Performance Data**: Add benchmark results, performance comparisons
- **Implementation Examples**: Share practical examples and use cases
- **Documentation Improvements**: Fix typos, clarify explanations, improve formatting
- **New Guides**: Create new how-to guides for common patterns
- **Cross-References**: Improve links between related topics

### 2. Finding the Right File

The repository is organized into modular documentation files:

```
docs/
├── models/              # LLMs, vision models, embeddings
├── infrastructure/      # Databases, deployment
├── frameworks/          # Agentic systems, LLM frameworks
├── evaluation/          # Benchmarks, testing
├── operations/          # Observability, monitoring
├── development/         # Dev tools, guardrails, fine-tuning
└── guides/              # How-to guides
```

Use GitHub search or `grep` to find where to add your content:
```bash
grep -r "vLLM" docs/  # Find files mentioning vLLM
```

### 3. Contribution Process

#### For Small Updates (typos, links, version bumps)
1. Edit the file directly on GitHub (click the pencil icon)
2. Describe your change in the commit message
3. Create a pull request

#### For Larger Contributions (new tools, sections)
1. Fork the repository
2. Create a branch: `git checkout -b add-tool-name`
3. Make your changes following the formatting guidelines below
4. Test that all links work
5. Update the "Last Updated" date in the file
6. Commit with a clear message: `git commit -m "Add ToolName to agentic systems"`
7. Push and create a pull request

### 4. Formatting Guidelines

#### Adding a New Tool/Framework

Follow the existing table format:

```markdown
| Tool | Version | Key Features | Link |
|------|---------|-------------|------|
| **New Tool** | 1.0+ | Feature 1, Feature 2, Feature 3 | [Website](https://example.com) |
```

**Include**:
- **Version**: Current stable version (use `+` for "and above")
- **Key Features**: 3-5 most important capabilities
- **Link**: Official website or GitHub (prefer official docs)

#### Updating Model Information

For model tables, include:

```markdown
| Model | Provider | Parameters | Context | Key Features |
|-------|----------|------------|---------|-------------|
| **Model Name** | Company | 70B | 128K | Feature 1, Feature 2 |
```

#### Adding Benchmark Results

Always include:
- Benchmark name and version
- Score/metric
- Date or model version tested
- Link to source

```markdown
| Model | MMMU | GPQA | Date |
|-------|------|------|------|
| **GPT-4o** | 69.1 | 53.6 | Apr 2026 |
```

#### Cross-References

When adding cross-references to related pages:

```markdown
## Related Resources

- [Related Page](../category/file.md) - Brief description of why it's relevant
- [Another Page](../other/file.md) - What users will find there
```

### 5. Quality Standards

#### Required for All Contributions
- ✅ Accurate information with sources
- ✅ Proper markdown formatting
- ✅ Working links (test before submitting)
- ✅ Consistent with existing style
- ✅ Update "Last Updated" date

#### Preferred
- ✅ Include version numbers
- ✅ Add performance/benchmark data when available
- ✅ Provide context (why is this tool useful?)
- ✅ Cross-reference related sections

#### Avoid
- ❌ Marketing language ("revolutionary", "game-changing")
- ❌ Unverified claims without sources
- ❌ Duplicate information already in other files
- ❌ Breaking existing links
- ❌ Subjective opinions without data

### 6. Documentation File Structure

Each documentation file should maintain:

```markdown
# Title

[Home](../../README.md) > [Category](../) > Title

> Brief description of what this page covers

*Last Updated: Month Day, Year*

## Table of Contents
- [Section 1](#section-1)
- [Section 2](#section-2)

## Content sections...

## Related Resources
- [Related Page](path/to/file.md) - Description

---

[🏠 Back to Home](../../README.md)
```

### 7. Examples of Good Contributions

#### Example 1: Adding a New Model
```markdown
| **Llama 4 405B** | Meta | 405B | 128K | Open weights, improved reasoning, multilingual |
```

#### Example 2: Updating Benchmark Results
```markdown
**Latest Results (May 2026)**:
- Model X: 71.2 MTEB score (was 68.5)
- Model Y: 89.3% on MATH benchmark
```

#### Example 3: Adding a New Tool
```markdown
### NewTool v2.0

**Best for**: Specific use case

- **Key Feature 1**: Explanation
- **Key Feature 2**: Explanation
- **Performance**: 2x faster than alternative
- [GitHub](https://github.com/org/newtool)
```

### 8. Reviewing Process

Pull requests will be reviewed for:
1. **Accuracy**: Is the information correct and sourced?
2. **Relevance**: Does it belong in this repository?
3. **Quality**: Is it well-formatted and clear?
4. **Completeness**: Are links, versions, and context provided?

Typical review time: 1-3 days for small updates, 1 week for larger contributions.

### 9. Questions or Issues?

- **Question about where to add something?** Open an issue first
- **Found outdated information?** Submit a PR or open an issue
- **Want to propose a new section?** Open an issue for discussion

## Code of Conduct

- Be respectful and constructive
- Assume good intentions
- Focus on facts and data over opinions
- Credit sources appropriately
- Help maintain a welcoming community

## Recognition

Contributors are recognized through:
- GitHub contribution history
- Acknowledgment in pull request discussions
- Community appreciation for keeping the resource up-to-date

---

Thank you for helping make GenAI_Atlas a valuable resource for the LLM community! 🚀
