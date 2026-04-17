# Data Processing & Validation

[Home](../../README.md) > [Development](../) > Data Processing & Validation

> Comprehensive guide to text processing, data validation, and synthetic data generation for LLM applications.

*Last Updated: April 18, 2026*

## Table of Contents
- [Text Processing](#text-processing)
- [Data Validation](#data-validation)
- [Synthetic Data](#synthetic-data)
- [Best Practices](#best-practices)

## Text Processing

### spaCy

| Aspect | Details |
|--------|---------|
| **Version** | 3+ |
| **Type** | Industrial-strength NLP |
| **Languages** | 70+ supported |

**Key Features:**
- Fast, production-ready
- Transformer model support
- Entity recognition (NER)
- Dependency parsing
- Part-of-speech tagging
- Sentence segmentation
- Text classification
- Custom pipeline components

**Common Use Cases:**

**1. Named Entity Recognition:**
```python
import spacy

nlp = spacy.load("en_core_web_trf")
doc = nlp("Apple Inc. was founded by Steve Jobs in Cupertino.")

for ent in doc.ents:
    print(ent.text, ent.label_)
# Output: Apple Inc. (ORG), Steve Jobs (PERSON), Cupertino (GPE)
```

**2. Text Preprocessing:**
```python
# Tokenization, lemmatization, stopword removal
doc = nlp("The quick brown foxes were jumping")
tokens = [token.lemma_ for token in doc if not token.is_stop]
# Output: ['quick', 'brown', 'fox', 'jump']
```

**3. Sentence Segmentation:**
```python
doc = nlp("First sentence. Second sentence. Third sentence.")
sentences = [sent.text for sent in doc.sents]
```

**4. Custom Pipeline Components:**
```python
from spacy.language import Language

@Language.component("custom_component")
def custom_function(doc):
    # Custom processing
    return doc

nlp.add_pipe("custom_component", after="ner")
```

**Best For:**
- Production NLP pipelines
- Multi-language support
- Entity extraction
- Document preprocessing
- Feature engineering

### NLTK (Natural Language Toolkit)

| Aspect | Details |
|--------|---------|
| **Type** | Educational and practical NLP |
| **Strength** | Comprehensive toolkit |
| **Use Case** | Research, education, prototyping |

**Key Features:**
- Tokenization
- Stemming and lemmatization
- POS tagging
- Parsing
- Semantic reasoning
- Corpus access
- Text classification

**Common Use Cases:**

**1. Tokenization:**
```python
from nltk.tokenize import word_tokenize, sent_tokenize

text = "Hello world. This is NLTK."
sentences = sent_tokenize(text)
words = word_tokenize(text)
```

**2. Stemming:**
```python
from nltk.stem import PorterStemmer

stemmer = PorterStemmer()
words = ["running", "runs", "ran"]
stems = [stemmer.stem(word) for word in words]
# Output: ['run', 'run', 'ran']
```

**3. Part-of-Speech Tagging:**
```python
from nltk import pos_tag

text = word_tokenize("The quick brown fox jumps")
tags = pos_tag(text)
# Output: [('The', 'DT'), ('quick', 'JJ'), ...]
```

**Best For:**
- Learning NLP concepts
- Quick prototyping
- Research projects
- Educational purposes
- Linguistic analysis

### Tokenizers (Hugging Face)

| Aspect | Details |
|--------|---------|
| **Focus** | Fast tokenization |
| **Implementation** | Rust-based (Python bindings) |
| **Models** | BPE, WordPiece, Unigram, SentencePiece |

**Key Features:**
- Extremely fast (10-100x faster than pure Python)
- Consistent with model training
- Batched encoding
- Truncation and padding
- Special token handling
- Offset mapping

**Common Use Cases:**

**1. Loading Pre-trained Tokenizers:**
```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("meta-llama/Llama-3-8B")
encoded = tokenizer("Hello world", return_tensors="pt")
```

**2. Custom Tokenizer Training:**
```python
from tokenizers import Tokenizer
from tokenizers.models import BPE
from tokenizers.trainers import BpeTrainer

tokenizer = Tokenizer(BPE())
trainer = BpeTrainer(vocab_size=30000, special_tokens=["[PAD]", "[UNK]"])
tokenizer.train(files=["data.txt"], trainer=trainer)
```

**3. Batch Processing:**
```python
texts = ["Text 1", "Text 2", "Text 3"]
encoded = tokenizer(texts, padding=True, truncation=True, max_length=512)
```

**Best For:**
- LLM application development
- Model fine-tuning
- Production inference
- Consistent tokenization

## Data Validation

### Pydantic

| Aspect | Details |
|--------|---------|
| **Version** | v2 |
| **Performance** | 50x faster than v1 |
| **Type** | Data validation with type hints |

**Key Features:**
- Type validation
- Data parsing
- JSON schema generation
- Custom validators
- Nested models
- Field validation
- Error messages

**Common Use Cases:**

**1. LLM Output Validation:**
```python
from pydantic import BaseModel, Field, validator

class PersonInfo(BaseModel):
    name: str = Field(..., min_length=1, max_length=100)
    age: int = Field(..., ge=0, le=150)
    email: str
    
    @validator('email')
    def validate_email(cls, v):
        if '@' not in v:
            raise ValueError('Invalid email')
        return v

# Validate LLM output
try:
    person = PersonInfo(**llm_output_dict)
except ValidationError as e:
    print(e.json())
```

**2. API Request/Response Schemas:**
```python
class QueryRequest(BaseModel):
    query: str = Field(..., max_length=1000)
    max_results: int = Field(default=10, ge=1, le=100)
    filters: dict[str, str] = Field(default_factory=dict)

class QueryResponse(BaseModel):
    results: list[str]
    total: int
    latency_ms: float
```

**3. Configuration Validation:**
```python
class ModelConfig(BaseModel):
    model_name: str
    temperature: float = Field(default=0.7, ge=0.0, le=2.0)
    max_tokens: int = Field(default=512, ge=1, le=4096)
    top_p: float = Field(default=1.0, ge=0.0, le=1.0)
```

**Best For:**
- LLM output validation
- API schema definition
- Configuration management
- Type safety
- Data quality enforcement

### Pandera

| Aspect | Details |
|--------|---------|
| **Focus** | Statistical data testing |
| **Integration** | pandas DataFrames |
| **Use Case** | Data quality checks |

**Key Features:**
- Schema validation for DataFrames
- Statistical hypothesis testing
- Data profiling
- Custom checks
- Error reporting
- Schema inference

**Common Use Cases:**

**1. DataFrame Schema Validation:**
```python
import pandera as pa
from pandera import Column, DataFrameSchema

schema = DataFrameSchema({
    "user_id": Column(int, checks=pa.Check.greater_than(0)),
    "score": Column(float, checks=pa.Check.in_range(0, 100)),
    "timestamp": Column(pa.DateTime),
    "category": Column(str, checks=pa.Check.isin(["A", "B", "C"]))
})

# Validate
validated_df = schema.validate(df)
```

**2. Statistical Checks:**
```python
schema = DataFrameSchema({
    "revenue": Column(
        float,
        checks=[
            pa.Check.greater_than(0),
            pa.Check(lambda s: s.mean() > 1000, error="Mean too low")
        ]
    )
})
```

**3. Training Data Validation:**
```python
training_schema = DataFrameSchema({
    "text": Column(str, checks=pa.Check(lambda s: s.str.len() > 10)),
    "label": Column(int, checks=pa.Check.isin([0, 1, 2])),
    "split": Column(str, checks=pa.Check.isin(["train", "val", "test"]))
})
```

**Best For:**
- Dataset validation
- Data quality monitoring
- ML pipeline testing
- Training data checks
- Preprocessing validation

### Great Expectations

| Aspect | Details |
|--------|---------|
| **Type** | Data quality framework |
| **Scale** | Enterprise-grade |
| **Features** | Profiling, validation, documentation |

**Key Features:**
- Data profiling
- Expectation suite creation
- Automated validation
- Data documentation
- Integration with data pipelines
- Alert and monitoring

**Common Use Cases:**

**1. Data Profiling:**
```python
from great_expectations.dataset import PandasDataset

ge_df = PandasDataset(df)
expectations = ge_df.profile(profiler=UserConfigurableProfiler)
```

**2. Expectation Suite:**
```python
# Define expectations
ge_df.expect_column_values_to_not_be_null("user_id")
ge_df.expect_column_values_to_be_between("age", min_value=0, max_value=120)
ge_df.expect_column_values_to_match_regex("email", regex=r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$")

# Save expectations
ge_df.save_expectation_suite("user_data_expectations.json")
```

**3. Pipeline Integration:**
```python
import great_expectations as ge

context = ge.DataContext()
batch = context.get_batch("data_asset_name")
results = context.run_validation_operator(
    "action_list_operator",
    assets_to_validate=[batch]
)
```

**Best For:**
- Production data pipelines
- Data quality monitoring
- Team collaboration on data quality
- Automated testing
- Data documentation

## Synthetic Data

### Faker

| Aspect | Details |
|--------|---------|
| **Type** | Fake data generator |
| **Use Case** | Testing and development |
| **Languages** | Multi-language support |

**Key Features:**
- Realistic fake data
- Multiple locales
- Custom providers
- Consistent seeding
- Wide variety of data types

**Common Use Cases:**

**1. Generate Test Data:**
```python
from faker import Faker

fake = Faker()

# Generate various data types
name = fake.name()
email = fake.email()
address = fake.address()
phone = fake.phone_number()
company = fake.company()
text = fake.text(max_nb_chars=200)
```

**2. Create Synthetic Datasets:**
```python
import pandas as pd

fake = Faker()
Faker.seed(42)  # Reproducibility

data = {
    "user_id": [fake.uuid4() for _ in range(1000)],
    "name": [fake.name() for _ in range(1000)],
    "email": [fake.email() for _ in range(1000)],
    "signup_date": [fake.date_this_year() for _ in range(1000)]
}

df = pd.DataFrame(data)
```

**3. Localized Data:**
```python
# Japanese locale
fake_ja = Faker('ja_JP')
japanese_name = fake_ja.name()
japanese_address = fake_ja.address()
```

**Best For:**
- Development and testing
- Demo data generation
- Privacy-preserving examples
- Load testing
- Prototyping

### SDV (Synthetic Data Vault)

| Aspect | Details |
|--------|---------|
| **Type** | ML-based synthetic data |
| **Method** | Generative models |
| **Privacy** | Differential privacy support |

**Key Features:**
- Learn from real data
- Statistical similarity
- Relational data support
- Privacy guarantees
- Quality metrics

**Common Use Cases:**

**1. Single Table Synthesis:**
```python
from sdv.tabular import GaussianCopula

model = GaussianCopula()
model.fit(real_data)
synthetic_data = model.sample(num_rows=1000)
```

**2. Multi-Table (Relational):**
```python
from sdv.relational import HMA1

metadata = {
    'tables': {
        'users': {...},
        'transactions': {...}
    }
}

model = HMA1(metadata=metadata)
model.fit(real_data)
synthetic_data = model.sample()
```

**3. Privacy-Preserving:**
```python
from sdv.tabular import CTGAN

model = CTGAN(
    epochs=300,
    privacy='differential_privacy',
    epsilon=1.0  # Privacy budget
)
model.fit(sensitive_data)
synthetic_data = model.sample(1000)
```

**Best For:**
- Privacy-preserving data sharing
- ML model training
- Data augmentation
- Research datasets
- Compliance (GDPR, HIPAA)

### Gretel

| Aspect | Details |
|--------|---------|
| **Type** | Enterprise synthetic data platform |
| **Deployment** | Cloud and on-premise |
| **Features** | Privacy, quality, compliance |

**Key Features:**
- Production-grade synthetic data
- Differential privacy
- Quality metrics
- API and SDK
- Compliance certifications

**Use Cases:**
- Enterprise data sharing
- Development environments
- ML training with privacy
- Third-party data sharing
- Regulatory compliance

**Best For:**
- Enterprise requirements
- High privacy standards
- Quality guarantees
- Managed service
- Compliance needs

## Best Practices

### Text Processing

**1. Choose Right Tool:**
- **spaCy**: Production pipelines, entity extraction
- **NLTK**: Education, research, prototyping
- **Transformers Tokenizers**: LLM applications

**2. Language Considerations:**
- Test with target languages
- Use language-specific models
- Consider multilingual models
- Validate character encoding

**3. Performance Optimization:**
- Batch processing when possible
- Disable unused pipeline components
- Use GPU acceleration (spaCy transformers)
- Cache processed results

**4. Preprocessing Pipeline:**
```python
def preprocess_text(text):
    # 1. Clean
    text = text.strip()
    text = remove_special_chars(text)
    
    # 2. Normalize
    text = text.lower()  # if case-insensitive
    
    # 3. Tokenize
    doc = nlp(text)
    
    # 4. Extract features
    tokens = [token.lemma_ for token in doc if not token.is_stop]
    
    return tokens
```

### Data Validation

**1. Fail Fast:**
- Validate at ingestion
- Clear error messages
- Log validation failures
- Monitor failure rates

**2. Layered Validation:**
```python
# Layer 1: Type validation (Pydantic)
validated_input = InputSchema(**raw_input)

# Layer 2: Business logic validation
if not is_valid_business_rule(validated_input):
    raise ValueError("Business rule violation")

# Layer 3: Statistical validation (Pandera)
validated_df = schema.validate(dataframe)
```

**3. Schema Evolution:**
- Version schemas
- Backward compatibility
- Migration paths
- Documentation

**4. Monitoring:**
- Track validation failures
- Alert on anomalies
- Data quality dashboards
- Trend analysis

### Synthetic Data

**1. Quality Assessment:**
- Statistical similarity metrics
- Distribution comparison
- ML utility testing
- Human review sampling

**2. Privacy Verification:**
- Membership inference tests
- Attribute disclosure checks
- Identity disclosure tests
- Differential privacy audits

**3. Use Cases:**

**Development:**
- Realistic test data
- No production data exposure
- Unlimited generation

**ML Training:**
- Data augmentation
- Class balance
- Rare event synthesis
- Privacy-preserving training

**Data Sharing:**
- Third-party collaboration
- Open datasets
- Compliance with regulations

**4. Validation:**
```python
from sdv.metrics.tabular import CSTest, KSTest

# Compare distributions
ks_score = KSTest.compute(real_data, synthetic_data)
cs_score = CSTest.compute(real_data, synthetic_data)

# ML utility
from sdv.metrics.tabular import LogisticDetection

detection_score = LogisticDetection.compute(real_data, synthetic_data)
# Score near 0.5 means synthetic data is indistinguishable
```

## Common Pitfalls

**Pitfall 1: Over-Processing**
- Removing too much information
- Aggressive stopword removal
- Excessive normalization

**Solution:** Preserve information needed for task

**Pitfall 2: Ignoring Data Quality**
- No validation in place
- Silent data issues
- Inconsistent formats

**Solution:** Implement validation at ingestion

**Pitfall 3: Poor Synthetic Data Quality**
- Unrealistic distributions
- Missing edge cases
- Privacy leakage

**Solution:** Validate quality and privacy metrics

**Pitfall 4: Inconsistent Processing**
- Different preprocessing for train/test
- Tokenization mismatches
- Encoding issues

**Solution:** Shared preprocessing pipeline, version control

## Related Resources
- [Fine-Tuning](./fine-tuning.md) - Training data preparation
- [Embeddings](../models/embeddings.md) - Text representation
- [Prompt Engineering](./prompt-engineering.md) - Input formatting
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Data quality metrics

---

[🏠 Back to Home](../../README.md)
