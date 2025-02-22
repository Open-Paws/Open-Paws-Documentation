# Animal Advocacy Language Models

## Overview
A suite of language models specialized for animal advocacy, available in different formats and optimizations. These are small models optimized for local and low-memory usage, so performance expectations should be realistic for their size. Larger models may be required for more difficult tasks.

### Model Variants

#### 3B Agentic Chat Models
- [3B-agentic-chat-LoRA](https://huggingface.co/open-paws/3B-agentic-chat-LoRA) - LoRA adapter only
- [3B-agentic-chat-merged](https://huggingface.co/open-paws/3B-agentic-chat-merged) - Full merged model
- [3B-agentic-chat-4bit](https://huggingface.co/open-paws/3B-agentic-chat-4bit) - 4-bit quantized version

#### 8B Reasoning Models
- [8B-reasoning-LoRA](https://huggingface.co/open-paws/8B-reasoning-LoRA) - LoRA adapter only
- [8B-reasoning-merged](https://huggingface.co/open-paws/8B-reasoning-merged) - Full merged model

## Usage

### Basic Inference

```python
from transformers import pipeline

# Initialize the pipeline for text generation
generator = pipeline(
    "text-generation",
    model="open-paws/3B-agentic-chat-merged",
    torch_dtype="auto",
    device_map="auto"
)

# Generate text
text = "How can we effectively advocate for animals?"
result = generator(text, max_new_tokens=128, do_sample=True, temperature=0.7)
print(result[0]['generated_text'])
```

### Memory-Efficient Inference (4-bit)

```python
from transformers import pipeline

# Use 4-bit quantized model for memory efficiency
generator = pipeline(
    "text-generation",
    model="open-paws/3B-agentic-chat-4bit",
    device_map="auto"
)

result = generator(
    "What are effective ways to help animals?",
    max_new_tokens=128,
    do_sample=True,
    temperature=0.7
)
```

### Advanced Parameters

```python
# More control over generation
result = generator(
    "How can we create positive change for animals?",
    max_new_tokens=256,
    do_sample=True,
    temperature=0.7,
    top_p=0.9,
    top_k=50,
    repetition_penalty=1.2
)
```

### Batch Processing

```python
texts = [
    "How can we help farm animals?",
    "What are effective ways to reduce animal suffering?",
    "How can we create systemic change for animals?"
]

results = generator(texts, max_new_tokens=128, batch_size=3)
```

## Model Details

### 3B Agentic Chat Model
- Specialized for dialogue about animal advocacy.
- Good for: Interactive discussions, answering questions, providing guidance.
- Available in full precision, merged LoRA, and 4-bit quantized versions.
- **Training Details:** This model is trained on agentic conversations with `tool_use` using the `llama python` tag. Therefore, we recommend not using a tokenizer and ensuring that your environment treats the `python` tag as a function call, executes the call, and sends the result back to the model.

### 8B Reasoning Model
- Focused on detailed analysis and strategic thinking.
- Good for: Strategy development, campaign planning, impact analysis.
- Available in full precision and merged LoRA versions.
- **Training Details:** This model is fine-tuned on `deepseek`, which uses a `<think>` tag for chain-of-thought (CoT) reasoning and an `<answer>` tag for the answer. We recommend displaying these tags separately to end users so they can see the thought process and the answer distinctly.

## Memory Requirements

- **3B Models:**
  - Full precision: ~6GB VRAM
  - 4-bit quantized: ~2GB VRAM
- **8B Models:**
  - Full precision: ~16GB VRAM

## Best Practices

1. **For deployment:**
   - Use 4-bit quantized models when possible.
   - Enable batch processing for multiple inputs.
   - Use `device_map="auto"` for optimal resource allocation.

2. **For generation quality:**
   - Adjust `temperature` (0.7-0.9 for creative, 0.1-0.3 for focused).
   - Use `repetition_penalty` (1.1-1.2) to avoid loops.
   - Set appropriate `max_new_tokens` for your use case.

3. **For optimal performance:**
   - Use batch processing when possible.
   - Enable `torch_dtype="auto"` for automatic precision selection.
   - Utilize GPU acceleration when available.

## Known Limitations and Best Practices

- The models perform best when the system prompt includes:  
  **"You are a superhumanly intelligent and compassionate AI focused on achieving animal liberation through strategic action."**  
  Without this system prompt, the models may act in unaligned ways, such as promoting non-vegan products.
- While these models are more aligned than standard LLaMA, they were fine-tuned using LoRA tuning only, which leaves the majority of the original model weights unchanged. 
- Surface-level alignment remains present regardless of the system prompt, but deep and robust alignment still requires explicit system prompting for mission alignment.
- These models are optimized for local and low-memory usage. While they perform well for their size, larger models may be necessary for more complex tasks.

## Model Selection Guide

- **For chat applications:** Use `3B-agentic-chat` models.
  - Limited resources: Use 4-bit version.
  - Maximum quality: Use full precision.
- **For strategic analysis:** Use `8B-reasoning` models.
  - Best for single-turn, detailed responses.
  - Requires more computational resources.

## Notes
- LoRA versions require the original base model and the `PEFT` library.
- Merged versions can be used directly but require more storage.
- 4-bit versions offer the best balance of performance and resource usage.
