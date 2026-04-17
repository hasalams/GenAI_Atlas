# On-Premise Deployment

[Home](../../README.md) > [Infrastructure](../infrastructure/) > On-Premise Deployment

> Comprehensive guide to deploying LLMs locally and on-premise: inference servers, quantization methods, and model serving platforms.

*Last Updated: April 18, 2026*

## Table of Contents

- [Inference Servers](#inference-servers)
- [Model Serving Platforms](#model-serving-platforms)
- [Quantization Methods](#quantization-methods)
- [Hardware Considerations](#hardware-considerations)
- [Selection Guide](#selection-guide)
- [Related Resources](#related-resources)

## Inference Servers

Production-grade inference engines for optimal LLM performance.

| Server | Version | Optimization | Key Features | Performance |
|--------|---------|-------------|-------------|-------------|
| **vLLM** | 0.6+ | GPU | PagedAttention, prefix caching, speculative decoding, multi-LoRA | 20-30x throughput, 2-3x latency reduction |
| **llama.cpp** | Latest | CPU/GPU/Metal | GGUF quantization, Flash Attention 2, RPC server, M3/M4/ROCm support | Dominates local deployment |
| **TensorRT-LLM** | 0.9+ | NVIDIA GPU | In-flight batching, FP8 inference (H100), INT4/INT8 quantization | 4-8x speedup on H100/A100 |
| **TGI (HuggingFace)** | 2.x | GPU | Continuous batching, Flash Attention 2, grammar-constrained gen, tool calling | Production-ready, broad model support |
| **SGLang** | 0.2+ | GPU | RadixAttention (auto KV cache reuse), constrained decoding, JSON schema | 3-5x faster for structured generation |
| **LMDeploy** | Latest | GPU | Vision-language models, OpenMMLab integration | Strong multimodal support |
| **DeepSpeed-FastGen** | Latest | GPU | Dynamic SplitFuse, prompt/generation batching | Microsoft optimization |

### vLLM 0.6+
**Best for**: High-throughput GPU serving

- **PagedAttention**: Memory-efficient attention, 20-30x throughput vs naive
- **Prefix Caching**: 5-10x speedup for repeated prompts (RAG, agents)
- **Speculative Decoding**: 2-3x latency reduction with draft models
- **Multi-LoRA**: Serve multiple LoRA adapters efficiently
- [GitHub](https://github.com/vllm-project/vllm)

### llama.cpp
**Best for**: Local deployment, CPU inference, Apple Silicon

- **GGUF**: Quantized format (2-8 bits), minimal quality loss
- **Hardware**: M3/M4 Metal, NVIDIA CUDA, AMD ROCm, AVX2/AVX512
- **Flash Attention 2**: Efficient attention mechanism
- **RPC Server**: Distributed inference across machines
- [GitHub](https://github.com/ggerganov/llama.cpp)

### TensorRT-LLM 0.9+
**Best for**: Maximum NVIDIA GPU performance

- **FP8 Inference**: 2x throughput vs FP16 on H100 Hopper
- **In-flight Batching**: Continuous batching for high throughput
- **INT4/INT8**: Weight-only quantization
- **Triton Integration**: Production deployment with Triton Inference Server
- [GitHub](https://github.com/NVIDIA/TensorRT-LLM)

### TGI (Text Generation Inference) 2.x
**Best for**: Production HuggingFace models

- **Continuous Batching**: Efficient request handling
- **Grammar-Constrained**: Force specific output formats (JSON, etc.)
- **Tool Calling**: Native function calling support
- **Broad Support**: Llama, Mistral, Mixtral, Qwen, Phi families
- [GitHub](https://github.com/huggingface/text-generation-inference)

### SGLang 0.2+
**Best for**: Structured generation, agentic workflows

- **RadixAttention**: Automatic KV cache reuse, 3-5x faster
- **Constrained Decoding**: JSON schema adherence, regex-guided
- **Structured Outputs**: Perfect for tool calling, agents
- **Use Cases**: Agent workflows, API responses, structured data extraction
- [GitHub](https://github.com/sgl-project/sglang)

## Model Serving Platforms

User-friendly platforms for running models locally.

### Ollama
- **Focus**: Simple local serving with model library
- **Features**: CLI + API, model management, automatic GPU detection
- **Models**: Pre-quantized library (Llama, Mistral, Qwen, etc.)
- **Best for**: Quick local deployment, development
- [Website](https://ollama.ai/)

### LocalAI
- **Focus**: OpenAI API drop-in replacement
- **Features**: Multi-modal, text-to-speech, image generation
- **Deployment**: Docker, Kubernetes, bare metal
- **Best for**: Replacing OpenAI API locally
- [GitHub](https://github.com/mudler/LocalAI)

### Jan
- **Focus**: Desktop AI assistant
- **Features**: GUI, GPU acceleration, model management
- **Platforms**: Windows, macOS, Linux
- **Best for**: Non-technical users, local ChatGPT alternative
- [Website](https://jan.ai/)

### LM Studio
- **Focus**: GUI for discovering and running local models
- **Features**: Model library, benchmarking, chat interface
- **Platforms**: Windows, macOS
- **Best for**: Exploring models, testing quantizations
- [Website](https://lmstudio.ai/)

### GPT4All
- **Focus**: Privacy-focused local AI
- **Features**: Cross-platform, embedded use, Python bindings
- **Models**: Curated model collection
- **Best for**: Privacy-conscious applications
- [Website](https://gpt4all.io/)

## Quantization Methods

Reduce model size and memory requirements with minimal quality loss.

| Method | Target | Bits | Quality Loss | Best For | Tooling |
|--------|--------|------|--------------|----------|---------|
| **GGUF (k-quant)** | CPU/GPU | 2-8 bit | <2% at Q5_K_M | Local/edge deployment, llama.cpp ecosystem | llama.cpp, Ollama, LM Studio |
| **AWQ** | GPU | 3-4 bit | <1% | Production serving, quality-critical apps | vLLM, TGI, TensorRT-LLM |
| **GPTQ** | GPU | 4 bit | ~2% | Legacy support, experimentation | AutoGPTQ, ExLlama |
| **FP8** | H100 GPU | 8 bit | Minimal | Hopper architecture, 2x throughput vs FP16 | TensorRT-LLM, vLLM |
| **BitsAndBytes** | GPU | 4/8 bit | Variable | HuggingFace fine-tuning, QLoRA | HuggingFace Transformers |
| **QuIP#** | GPU | <2 bit | Experimental | Research, extreme compression | Research implementations |
| **AQLM** | GPU | 2-3 bit | Good | Additive quantization, emerging | Research/production |

### Quantization Recommendations

**Best Quality**:
- No quantization (FP16/BF16)
- FP8 on H100
- AWQ 4-bit

**Best Balance** (recommended for most):
- GGUF Q5_K_M (5-6 bits)
- AWQ 4-bit

**Maximum Compression**:
- GGUF Q2_K or Q3_K_M
- AQLM 2-bit
- QuIP# <2-bit (experimental)

### Quality vs Size Trade-offs

| Quantization | Size | Quality Loss | Use Case |
|--------------|------|--------------|----------|
| No quant (FP16) | 100% | 0% | Reference, production with resources |
| AWQ 4-bit | 25% | <1% | Production, quality-critical |
| GGUF Q5_K_M | 35% | <2% | General purpose, recommended |
| GGUF Q4_K_M | 28% | 2-3% | Resource-constrained |
| GGUF Q3_K_M | 22% | 5-7% | Extreme constraint |
| GGUF Q2_K | 17% | 10%+ | Experimental |

## Hardware Considerations

### GPU Recommendations

**NVIDIA (Best Support)**
- **H100**: FP8 inference, TensorRT-LLM, maximum performance
- **A100 (80GB)**: Most 70B models unquantized, excellent performance
- **A100 (40GB)**: 70B models with quantization
- **4090 (24GB)**: Best consumer GPU, 70B with quantization
- **3090 (24GB)**: Good value, 70B with quantization

**AMD**
- **MI300X**: Competitive with H100, ROCm support improving
- **7900 XTX**: Consumer option, ROCm support for llama.cpp

**Apple Silicon**
- **M3 Max/Ultra**: Good for 70B models with quantization
- **M4 Max/Ultra**: Improved performance, unified memory advantage

### CPU Inference
**Viable with llama.cpp for models up to 13B**
- AVX-512: 2-3x faster than AVX2
- High RAM: Can run larger models (slow but works)

### Memory Requirements (70B Model)

| Quantization | VRAM/RAM Required | Example Hardware |
|--------------|-------------------|------------------|
| FP16 | ~140GB | 2x A100 80GB |
| AWQ 4-bit | ~40GB | 1x A100 40GB, 1x 4090 |
| GGUF Q5_K_M | ~48GB | 1x A100 40GB, 2x 3090 |
| GGUF Q4_K_M | ~40GB | 1x 4090, M3 Max 64GB |
| GGUF Q3_K_M | ~32GB | CPU with 64GB RAM |

## Selection Guide

### By Use Case

**Production API Serving**
→ vLLM 0.6+ (GPU) or TensorRT-LLM (NVIDIA)

**Local Development**
→ Ollama (easy) or llama.cpp (flexible)

**Desktop Application**
→ Jan or LM Studio (GUI)

**Structured Generation / Agents**
→ SGLang (RadixAttention for speed)

**Maximum NVIDIA Performance**
→ TensorRT-LLM with FP8 on H100

**Apple Silicon**
→ llama.cpp with Metal backend

**CPU-Only**
→ llama.cpp with GGUF Q4_K_M

### By Team Size

**Solo Developer / Small Team**
→ Ollama + OpenAI-compatible API

**Medium Team / Startup**
→ vLLM + Ray Serve or TGI

**Enterprise**
→ TensorRT-LLM + Triton Inference Server

## Performance Optimization

### Speed Improvements
1. **Speculative Decoding**: 2-3x latency reduction (vLLM, llama.cpp)
2. **Prefix Caching**: 5-10x speedup for repeated prompts (vLLM, SGLang)
3. **Flash Attention 2**: Memory-efficient, faster (all modern servers)
4. **FP8**: 2x throughput on H100 vs FP16 (TensorRT-LLM)
5. **RadixAttention**: Auto KV cache reuse (SGLang)

### Memory Optimization
1. **PagedAttention**: Efficient memory management (vLLM)
2. **Quantization**: 4x reduction with minimal quality loss
3. **Tensor Parallelism**: Split across multiple GPUs
4. **CPU Offloading**: Offload layers to RAM if needed

## Related Resources

- [Text Models](../models/text-models.md) - Models to deploy
- [Getting Started](../guides/getting-started.md) - Deployment strategy selection
- [Production Checklist](../operations/production-checklist.md) - Best practices
- [Observability](../operations/observability.md) - Monitoring inference

---

[🏠 Back to Home](../../README.md)
