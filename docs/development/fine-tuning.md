# Fine-Tuning & Training

[Home](../../README.md) > [Development](../) > Fine-Tuning & Training

> Comprehensive guide to fine-tuning LLMs, training frameworks, parameter-efficient methods, and distributed training for specialized model adaptation.

*Last Updated: April 18, 2026*

## Table of Contents
- [Training Frameworks](#training-frameworks)
- [Parameter-Efficient Fine-Tuning (PEFT)](#parameter-efficient-fine-tuning-peft)
- [Distributed Training](#distributed-training)
- [Best Practices](#best-practices)

## Training Frameworks

### Hugging Face Transformers

| Aspect | Details |
|--------|---------|
| **Type** | Foundation ML framework |
| **Models** | Thousands of pre-trained models |
| **License** | Apache 2.0 |

**Key Features:**
- Comprehensive model library
- Unified API across architectures
- Training utilities (Trainer API)
- Integration with PyTorch and TensorFlow
- Active community and ecosystem

**Components:**
- **Transformers**: Model architectures
- **Datasets**: Data loading and processing
- **Tokenizers**: Fast tokenization
- **Accelerate**: Distributed training abstraction
- **Evaluate**: Metrics and evaluation

**Use Cases:**
- Full fine-tuning
- Research and experimentation
- Custom model development
- Inference optimization

**Training Example:**
```python
from transformers import AutoModelForCausalLM, Trainer, TrainingArguments

model = AutoModelForCausalLM.from_pretrained("base-model")
training_args = TrainingArguments(
    output_dir="./results",
    num_train_epochs=3,
    per_device_train_batch_size=4,
    gradient_accumulation_steps=4,
)
trainer = Trainer(model=model, args=training_args, train_dataset=dataset)
trainer.train()
```

**Best For:**
- Standard fine-tuning workflows
- Researchers and developers
- Custom architectures
- Broad model support

### Axolotl

| Aspect | Details |
|--------|---------|
| **Focus** | Easy fine-tuning configuration |
| **Methods** | QLoRA, LoRA, full fine-tuning |
| **License** | Apache 2.0 |

**Key Features:**
- YAML configuration for training
- Pre-built recipes for popular models
- Support for multiple PEFT methods
- Flash Attention integration
- Multi-GPU support

**Configuration-Driven:**
```yaml
base_model: meta-llama/Llama-3-8B
model_type: LlamaForCausalLM
tokenizer_type: LlamaTokenizer

adapter: lora  # or qlora
lora_r: 16
lora_alpha: 32

datasets:
  - path: custom_dataset.jsonl
    type: alpaca

num_epochs: 3
micro_batch_size: 2
gradient_accumulation_steps: 4
```

**Strengths:**
- Simple configuration
- Quick setup
- Proven recipes
- Good documentation

**Best For:**
- Quick fine-tuning experiments
- Standard use cases
- Teams preferring configuration over code
- Reproducible training runs

### Unsloth

| Aspect | Details |
|--------|---------|
| **Focus** | Fast, memory-efficient fine-tuning |
| **Performance** | 2x faster training, 60% memory reduction |
| **Methods** | LoRA, QLoRA |

**Key Features:**
- Optimized kernels for speed
- Memory-efficient implementations
- Easy API (wrapper around Transformers)
- Support for major model families
- Free and Pro versions

**Performance Benefits:**
- 2x faster training
- 60% less memory usage
- Larger batch sizes possible
- Cost savings on cloud GPUs

**Quick Start:**
```python
from unsloth import FastLanguageModel

model, tokenizer = FastLanguageModel.from_pretrained(
    model_name="llama-3-8b",
    max_seq_length=2048,
    load_in_4bit=True,
)

model = FastLanguageModel.get_peft_model(
    model,
    r=16,
    lora_alpha=32,
    target_modules=["q_proj", "k_proj", "v_proj"],
)
```

**Best For:**
- Speed-critical training
- Limited GPU memory
- Cost optimization
- LoRA/QLoRA fine-tuning

### LLaMA Factory

| Aspect | Details |
|--------|---------|
| **Interface** | Web UI + configuration |
| **Models** | Diverse model support |
| **Focus** | User-friendly fine-tuning |

**Key Features:**
- Web-based interface
- No-code fine-tuning
- Built-in dataset templates
- Experiment tracking
- Model evaluation

**Supported Methods:**
- Full fine-tuning
- LoRA
- QLoRA
- Freeze tuning
- P-tuning

**Built-in Features:**
- Dataset management
- Training monitoring
- Model evaluation
- Export and deployment

**Best For:**
- Teams without ML expertise
- Rapid prototyping
- Non-technical users
- Education and learning

## Parameter-Efficient Fine-Tuning (PEFT)

### LoRA (Low-Rank Adaptation)

**Concept:** Add trainable low-rank matrices to existing weights.

**How It Works:**
```
W_new = W_frozen + B × A
```
Where:
- W_frozen: Original frozen weights
- A, B: Small trainable matrices (rank r << model dimension)

**Advantages:**
- 10-100x fewer trainable parameters
- Minimal memory overhead
- Fast training
- Easy to swap adapters
- No inference latency with merged weights

**Typical Configuration:**
- Rank (r): 8-64 (higher = more capacity, slower)
- Alpha: 16-32 (scaling factor, often 2×rank)
- Target modules: attention layers (q_proj, v_proj, k_proj)

**Best For:**
- Limited GPU memory
- Multiple task-specific adapters
- Fast iteration
- Cost-effective training

### QLoRA (Quantized LoRA)

**Concept:** Combine LoRA with 4-bit quantization of base model.

**Memory Savings:**
- Base model: 4-bit quantized (NormalFloat 4)
- LoRA adapters: 16-bit
- Gradients: Computed efficiently

**Enables:**
- Fine-tune 65B model on single 48GB GPU
- 70B on 2× consumer GPUs
- Minimal quality degradation

**Configuration:**
```python
from transformers import BitsAndBytesConfig

bnb_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_quant_type="nf4",
    bnb_4bit_compute_dtype=torch.bfloat16,
    bnb_4bit_use_double_quant=True,
)

model = AutoModelForCausalLM.from_pretrained(
    "model_name",
    quantization_config=bnb_config
)
```

**Best For:**
- Large model fine-tuning on limited hardware
- Cost optimization
- Experimental work
- Consumer GPU fine-tuning

### Adapter Methods

**Prefix Tuning:**
- Add trainable prefix tokens to each layer
- Model learns task-specific prefixes
- No modification to base model

**Prompt Tuning:**
- Train continuous prompt embeddings
- Extremely parameter-efficient
- Best for simple task adaptation

**IA³ (Infused Adapter by Inhibiting and Amplifying Inner Activations):**
- Scale activations with learned vectors
- Even fewer parameters than LoRA
- Competitive performance

### PEFT Library (Hugging Face)

**Unified Interface:**
```python
from peft import LoraConfig, get_peft_model

config = LoraConfig(
    r=16,
    lora_alpha=32,
    target_modules=["q_proj", "v_proj"],
    lora_dropout=0.05,
    bias="none",
    task_type="CAUSAL_LM"
)

model = get_peft_model(base_model, config)
```

**Supported Methods:**
- LoRA / QLoRA
- Prefix Tuning
- P-Tuning
- Prompt Tuning
- IA³
- AdaLoRA

**Features:**
- Easy switching between methods
- Adapter management
- Merge and save utilities
- Inference optimization

## Distributed Training

### DeepSpeed

| Aspect | Details |
|--------|---------|
| **Provider** | Microsoft |
| **Focus** | Large-scale distributed training |
| **License** | Apache 2.0 |

**Key Technologies:**

**ZeRO (Zero Redundancy Optimizer):**
- **Stage 1**: Optimizer state partitioning (4x memory reduction)
- **Stage 2**: + Gradient partitioning (8x reduction)
- **Stage 3**: + Parameter partitioning (memory proportional to # GPUs)

**ZeRO-Infinity:**
- Offload to CPU and NVMe
- Train trillion-parameter models
- Efficient memory management

**Features:**
- 3D parallelism (data + pipeline + tensor)
- Gradient accumulation
- Mixed precision training
- Custom CUDA kernels
- Communication optimization

**Configuration:**
```json
{
  "zero_optimization": {
    "stage": 3,
    "offload_optimizer": {"device": "cpu"},
    "offload_param": {"device": "cpu"}
  },
  "train_micro_batch_size_per_gpu": 1,
  "gradient_accumulation_steps": 16,
  "fp16": {"enabled": true}
}
```

**Best For:**
- Very large models (>10B parameters)
- Multi-node training
- Limited GPU memory
- Production training pipelines

### Megatron-LM

| Aspect | Details |
|--------|---------|
| **Provider** | NVIDIA |
| **Focus** | Billion-scale model training |
| **Models** | GPT, BERT, T5 families |

**Key Features:**
- Tensor parallelism
- Pipeline parallelism
- Sequence parallelism
- Optimized for NVIDIA hardware
- Proven at massive scale

**Parallelism Strategies:**

**Tensor Parallelism:**
- Split individual layers across GPUs
- Low-latency communication
- Ideal for fast interconnects (NVLink)

**Pipeline Parallelism:**
- Split model layers across GPUs
- Process micro-batches in pipeline
- Good for slower interconnects

**Sequence Parallelism:**
- Split sequence dimension
- For very long sequences
- Reduces memory per GPU

**Best For:**
- Training from scratch
- Billion+ parameter models
- NVIDIA DGX systems
- Research labs

### FSDP (Fully Sharded Data Parallel)

| Aspect | Details |
|--------|---------|
| **Provider** | Meta / PyTorch |
| **Type** | Built into PyTorch |
| **Inspired by** | DeepSpeed ZeRO |

**Features:**
- Native PyTorch integration
- Automatic sharding
- Mixed precision support
- CPU offloading
- Gradient checkpointing

**Simple Setup:**
```python
from torch.distributed.fsdp import FullyShardedDataParallel as FSDP

model = FSDP(
    model,
    auto_wrap_policy=transformer_auto_wrap_policy,
    mixed_precision=bf16_policy,
)
```

**Best For:**
- PyTorch-native workflows
- Moderate to large models
- Simpler than DeepSpeed
- Research and production

## Best Practices

### Data Preparation

**Dataset Quality:**
1. **Clean Data**: Remove duplicates, errors, irrelevant content
2. **Diverse Examples**: Cover full range of use cases
3. **Balanced Distribution**: Avoid class imbalance
4. **Representative**: Match production distribution

**Dataset Size Guidelines:**
- **Full fine-tuning**: 10K-1M+ examples
- **LoRA**: 1K-100K examples
- **Few-shot learning**: 10-1K examples
- **Domain adaptation**: 5K-50K examples

**Format Standardization:**
```json
{
  "instruction": "Task description",
  "input": "Optional context",
  "output": "Expected response"
}
```

Or conversational:
```json
{
  "messages": [
    {"role": "user", "content": "Question"},
    {"role": "assistant", "content": "Answer"}
  ]
}
```

### Hyperparameter Tuning

**Critical Parameters:**

**Learning Rate:**
- Full fine-tuning: 1e-5 to 5e-5
- LoRA: 1e-4 to 3e-4
- Start higher, use warmup and decay

**Batch Size:**
- Effective batch size: 32-256
- Use gradient accumulation if needed
- Larger = more stable, slower convergence

**Epochs:**
- Usually 1-5 epochs
- Monitor validation loss
- Early stopping to prevent overfitting

**LoRA Rank:**
- r=8: Simple tasks
- r=16: Most use cases
- r=32-64: Complex tasks, more capacity

**Sequence Length:**
- Match your use case
- Longer = more memory
- Use packing for efficiency

### Training Monitoring

**Key Metrics:**
1. **Training Loss**: Should decrease smoothly
2. **Validation Loss**: Prevent overfitting
3. **Perplexity**: Language modeling quality
4. **Custom Metrics**: Task-specific accuracy

**Red Flags:**
- Loss not decreasing
- Training/validation divergence (overfitting)
- Loss spikes or instability
- Gradient explosion (check gradient norms)

**Tools:**
- Weights & Biases
- TensorBoard
- MLflow
- Built-in logging

### Evaluation Strategy

**During Training:**
- Validation set evaluation every N steps
- Save checkpoints regularly
- Track multiple metrics
- Early stopping on validation loss

**Post-Training:**
- Hold-out test set evaluation
- Human evaluation sampling
- Comparison to baseline
- Domain-specific benchmarks
- A/B test in production

### Common Pitfalls

**Pitfall 1: Overfitting**
- Training loss very low, validation loss high
- Model memorizes training data
- Poor generalization

**Solution:**
- More data
- Fewer epochs
- Early stopping
- Data augmentation
- Regularization (dropout, weight decay)

**Pitfall 2: Catastrophic Forgetting**
- Model loses general capabilities
- Too much specialization

**Solution:**
- Mix in general data (10-20%)
- Shorter training
- Lower learning rate
- LoRA instead of full fine-tuning

**Pitfall 3: Poor Data Quality**
- Noisy labels
- Irrelevant examples
- Format inconsistencies

**Solution:**
- Data cleaning and validation
- Manual review of samples
- Consistency checks
- Gradual data expansion

**Pitfall 4: Wrong Hyperparameters**
- Learning rate too high (instability)
- Learning rate too low (no learning)
- Batch size mismatched

**Solution:**
- Start with proven baselines
- Learning rate finder
- Systematic hyperparameter search
- Monitor training curves

**Pitfall 5: Ignoring Licenses**
- Using model against license terms
- Data compliance issues

**Solution:**
- Check model licenses (commercial use?)
- Verify data usage rights
- Document provenance

## Training Recipes

### Recipe 1: LoRA Fine-tuning (70B Model on Single GPU)

**Requirements:** 1× A100 80GB or equivalent

**Configuration:**
```yaml
base_model: meta-llama/Llama-3-70B
method: qlora
r: 32
lora_alpha: 64
target_modules: [q_proj, k_proj, v_proj, o_proj]

load_in_4bit: true
bnb_4bit_compute_dtype: bfloat16

batch_size: 1
gradient_accumulation_steps: 16
learning_rate: 2e-4
epochs: 3
```

**Expected:** 24-36 hours for 10K examples

### Recipe 2: Full Fine-tuning (7B Model)

**Requirements:** 4× A100 40GB or equivalent

**Configuration:**
```yaml
base_model: meta-llama/Llama-3-8B
method: full

per_device_batch_size: 4
gradient_accumulation_steps: 4
learning_rate: 1e-5
warmup_steps: 100
epochs: 2

deepspeed_stage: 2
```

**Expected:** 8-16 hours for 50K examples

### Recipe 3: Instruction Tuning

**Dataset Format:**
```json
{
  "instruction": "Summarize the following text in 2 sentences.",
  "input": "Long text here...",
  "output": "Concise summary."
}
```

**Best Practices:**
- 5K-50K diverse instructions
- Mix of task types
- Quality over quantity
- Test on out-of-distribution instructions

## Related Resources
- [Text Models](../models/text-models.md) - Base models for fine-tuning
- [Evaluation Frameworks](../evaluation/evaluation-frameworks.md) - Testing fine-tuned models
- [On-Premise Deployment](../infrastructure/on-premise-deployment.md) - Inference servers
- [Data Processing](./data-processing.md) - Dataset preparation tools

---

[🏠 Back to Home](../../README.md)
