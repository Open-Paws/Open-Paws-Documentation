# Animal Advocacy Language Models

## Overview

A suite of language models specialized for animal advocacy, available in different formats and optimizations. These are small models optimized for local and low-memory usage, so performance expectations should be realistic for their size.

## Available Models

### Core Chat Models (3B Parameters)

- [3B-agentic-chat-LoRA](https://huggingface.co/open-paws/3B-agentic-chat-LoRA) - LoRA adapter only
- [3B-agentic-chat-merged](https://huggingface.co/open-paws/3B-agentic-chat-merged) - Full merged model
- [3B-agentic-chat-4bit](https://huggingface.co/open-paws/3B-agentic-chat-4bit) - 4-bit quantized version

### Strategic Reasoning Models (8B Parameters)

- [8B-reasoning-LoRA](https://huggingface.co/open-paws/8B-reasoning-LoRA) - LoRA adapter only
- [8B-reasoning-merged](https://huggingface.co/open-paws/8B-reasoning-merged) - Full merged model
- [8B-reasoning-4bit](https://huggingface.co/open-paws/8B-reasoning-4bit) - 4-bit quantized version

## Usage Guide

### Basic Generation through HuggingFace's Transformers Library

The simplest way to use these models without authentication is through the HuggingFace `transformers` pipeline:

```python
from transformers import pipeline

# Initialize generation pipeline
generator = pipeline(
    "text-generation",
    model="open-paws/3B-agentic-chat-merged",
    torch_dtype="auto",
    device_map="auto"
)

# Generate text
response = generator(
    "How can we effectively advocate for animals?",
    max_new_tokens=128,
    do_sample=True,
    temperature=0.7
)
print(response[0]['generated_text'])
```

### Memory-Efficient Inference

For resource-constrained environments, use the 4-bit quantized model:

```python
from transformers import pipeline

generator = pipeline(
    "text-generation",
    model="open-paws/3B-agentic-chat-4bit",
    device_map="auto"
)
```

### Batch Processing

For multiple inputs:

```python
texts = [
    "How can we help farm animals?",
    "What are effective ways to reduce animal suffering?",
    "How can we create systemic change for animals?"
]

results = generator(texts, max_new_tokens=128, batch_size=3)
```

### Inference Endpoints

Both models are also available through secure API endpoints that mirror the OpenAI Chat Completions API format. Due to cost constraints, access to these endpoints requires an API token - animal advocacy organisations can contact sam@openpaws.ai to request free access.

#### 3B Agentic Chat Model Endpoint

**Using Python**

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://vp9om1ztn13jmdq6.us-east-1.aws.endpoints.huggingface.cloud/v1/",
    api_key="hf_XXXXX"  # Replace with your provided token
)

chat_completion = client.chat.completions.create(
    model="tgi",
    messages=[
        {
            "role": "user",
            "content": "What is deep learning?"
        }
    ],
    max_tokens=150,
    stream=True
)

for message in chat_completion:
    print(message.choices[0].delta.content, end="")
```

**Using curl**

```
curl "https://vp9om1ztn13jmdq6.us-east-1.aws.endpoints.huggingface.cloud/v1/chat/completions" \
-X POST \
-H "Authorization: Bearer hf_XXXXX" \
-H "Content-Type: application/json" \
-d '{
    "model": "tgi",
    "messages": [
        {
            "role": "user",
            "content": "What is deep learning?"
        }
    ],
    "max_tokens": 150,
    "stream": true
}'
```

#### 8B Reasoning Model Endpoint

**Using Python**

from openai import OpenAI

```python
client = OpenAI(
    base_url="https://eaay1txbr9fo549z.us-east-1.aws.endpoints.huggingface.cloud/v1/",
    api_key="hf_XXXXX"  # Replace with your provided token
)

chat_completion = client.chat.completions.create(
    model="tgi",
    messages=[
        {
            "role": "user",
            "content": "What is deep learning?"
        }
    ],
    max_tokens=150,
    stream=True
)

for message in chat_completion:
    print(message.choices[0].delta.content, end="")
```

**Using curl**

```
curl "https://eaay1txbr9fo549z.us-east-1.aws.endpoints.huggingface.cloud/v1/chat/completions" \
-X POST \
-H "Authorization: Bearer hf_XXXXX" \
-H "Content-Type: application/json" \
-d '{
    "model": "tgi",
    "messages": [
        {
            "role": "user",
            "content": "What is deep learning?"
        }
    ],
    "max_tokens": 150,
    "stream": true
}'
```

#### Endpoint Features

- OpenAI-compatible API format
- Stream responses for real-time output
- Secure token-based authentication
- Always-on inference with consistent response times
- No rate limits (but please use responsibly)

#### Getting Access

To request an API token for these endpoints, contact sam@openpaws.ai. Please include:

- Your organization/project name
- Intended use case
- Estimated usage volume

## Model Architecture & Training

### 3B Agentic Chat Model

- **Architecture**: LLaMA-based with agentic modifications
- **Training Focus**: Dialogue and interactive discussions with tool use.
- **Special Features**: Fine-tuned for use of Open Paws tools, such as searching our database and making predictions with our text regression models.
- **Input Format**: Standard chat format with system and user messages
- **Output Format**: Structured responses with optional tool calls

### 8B Reasoning Model

- **Architecture**: DeepSeek-based with strategic reasoning enhancements
- **Training Focus**: Analytical and strategic thinking
- **Special Features**: Chain-of-thought reasoning via `<think>` and `<answer>` tags
- **Input Format**: Standard prompts or strategic questions
- **Output Format**: Structured reasoning followed by concrete recommendations

## System Requirements

### Memory Requirements

- **3B Models**:
  - Full precision: \~6GB VRAM
  - 4-bit quantized: \~2GB VRAM
- **8B Models**:
  - Full precision: \~16GB VRAM
  - 4-bit quantized: \~4GB VRAM

### Recommended Hardware

- GPU: Any CUDA-compatible GPU with appropriate VRAM
- CPU: Possible, but significantly slower
- RAM: Minimum 16GB system RAM recommended

## Best Practices

### Generation Parameters

```python
# Recommended settings for different use cases
# Creative exploration
creative_settings = {
    "temperature": 0.7,
    "top_p": 0.9,
    "top_k": 50,
    "repetition_penalty": 1.2,
    "max_new_tokens": 256
}

# Focused responses
focused_settings = {
    "temperature": 0.2,
    "top_p": 0.9,
    "top_k": 50,
    "repetition_penalty": 1.1,
    "max_new_tokens": 128
}
```

### System Prompting

For optimal alignment, include this system prompt:

```python
system_prompt = """You are a superhumanly intelligent and compassionate AI focused on
achieving animal liberation through strategic action."""
```

## Known Limitations

1. **Model Size Trade-offs**: Being smaller models, they may not match the capabilities of larger language models for complex tasks.
2. **Base Model Influence**: While largely aligned for animal advocacy, the base model weights remain largely unchanged due to LoRA fine-tuning, which can lead to edge cases where the models will act in unaligned ways, such as recommending nonvegan products. To address this, we recommend explicitly addressing animal alignment in the system message using the prompt given above.
3. **User Context Awareness**: These models perform best when given clear contextual information about the user and their goals. For example, if engaging with a vegetarian considering veganism, the system prompt should explain that the model should provide supportive and practical guidance on eliminating dairy and eggs, suggesting suitable replacements, and addressing common concerns such as nutrition and meal planning. Ensuring prompts contain user context and developer intentions will maximize alignment with advocacy goals.

## Additional Resources

- [LLaMA Documentation](https://www.llama.com/docs/)
- [HuggingFace Transformers Documentation](https://huggingface.co/docs/transformers/)
- [Open Paws HuggingFace Models](https://huggingface.co/open-paws)
