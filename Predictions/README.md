# Animal Advocacy Prediction Models

## Overview
A suite of prediction models designed to evaluate animal advocacy content through two complementary approaches:

1. **Performance Prediction** – Evaluates content based on real-world advocacy metrics.
2. **Preference Prediction** – Assesses content using human and synthetic feedback.

## Using the Models 

These models are text regression models that predict various metrics for animal advocacy content. You can easily use them through the Hugging Face `transformers` library pipeline or our dedicated inference endpoints.

### Using Public Inference Endpoints

These models are available through free public endpoints, requiring no authentication. The endpoints are always-on CPU instances for reliable, consistent response times.

#### Advocate Preference Prediction Endpoint

This endpoint predicts how well content will resonate with animal advocates.

**Python Usage**
```python
import requests

def get_preference_prediction(text):
    API_URL = "https://kev0bv9q0wc83rua.us-east-1.aws.endpoints.huggingface.cloud"
    headers = {
        "Accept": "application/json",
        "Content-Type": "application/json"
    }
    
    response = requests.post(API_URL, headers=headers, json={
        "inputs": text,
        "parameters": {}
    })
    return response.json()

# Example usage
text = "Animals deserve to live free from exploitation and suffering."
preference_score = get_preference_prediction(text)
print(f"Preference Score: {preference_score}")
```
**curl Usage**

```
curl "https://kev0bv9q0wc83rua.us-east-1.aws.endpoints.huggingface.cloud" \
-X POST \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "inputs": "Animals deserve to live free from exploitation and suffering.",
    "parameters": {}
}'
```

#### Text Performance Prediction Endpoint

This endpoint predicts the likely real-world performance of advocacy content.

**Python Usage**
```python
import requests

def get_performance_prediction(text):
    API_URL = "https://yu85a393fhiqe5hl.us-east-1.aws.endpoints.huggingface.cloud"
    headers = {
        "Accept": "application/json",
        "Content-Type": "application/json"
    }
    
    response = requests.post(API_URL, headers=headers, json={
        "inputs": text,
        "parameters": {}
    })
    return response.json()

# Example usage
text = "Animals deserve to live free from exploitation and suffering."
performance_score = get_performance_prediction(text)
print(f"Performance Score: {performance_score}")
```

**curl Usage**

```
curl "https://yu85a393fhiqe5hl.us-east-1.aws.endpoints.huggingface.cloud" \
-X POST \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{
    "inputs": "Animals deserve to live free from exploitation and suffering.",
    "parameters": {}
}'
```

#### Usage Notes

- Both endpoints are always-on CPU instances, ensuring consistent response times
- No authentication required
- No rate limits, but please use responsibly
- Ideal for real-time content evaluation and feedback

### Using HuggingFace's Transformers Library

```python
from transformers import pipeline

# Initialize the pipeline for text regression
predictor = pipeline(
    "text-classification",
    model="open-paws/perceived_trustworthiness_prediction",
    return_all_scores=True
)

# Make predictions
text = "Animals deserve to live free from exploitation and suffering."
result = predictor(text)

# Results will be a score between 0 and 1
print(result[0][0]['score'])  # Example output: 0.856
```

### Batch Processing

For processing multiple texts efficiently:

```python
texts = [
    "Animals deserve to live free from exploitation.",
    "Factory farming causes immense suffering.",
    "We must take action to protect animals."
]

# Process multiple texts at once
results = predictor(texts)

# Access scores
for text, result in zip(texts, results):
    score = result[0]['score']
    print(f"Text: {text}\nScore: {score}\n")
```

## Known Limitations and Best Practices

### Handling Out-of-Range Predictions

These models are regression-based and can occasionally predict scores outside the intended 0-1 range. This occurs when the model encounters content that it predicts should score more extremely than examples from its training data. To handle this gracefully, we recommend clipping the values to the valid range:

```python
from transformers import pipeline
import numpy as np

predictor = pipeline(
    "text-classification",
    model="open-paws/perceived_trustworthiness_prediction",
    return_all_scores=True
)

def clip_score(score):
    """Clips the score to be between 0 and 1."""
    return np.clip(score, 0, 1)

text = "Animals deserve to live free from exploitation and suffering."
result = predictor(text)
score = result[0][0]['score']
clipped_score = clip_score(score)

# For batch processing
texts = [
    "Animals deserve to live free from exploitation.",
    "Factory farming causes immense suffering.",
    "We must take action to protect animals."
]

results = predictor(texts)
for text, result in zip(texts, results):
    score = clip_score(result[0]['score'])
    print(f"Text: {text}\nClipped Score: {score}\n")
```

## Available Models on Hugging Face

### Core Models
- [Animal Advocate Preference Prediction](https://huggingface.co/open-paws/animal_advocate_preference_prediction)
- [Text Performance Prediction](https://huggingface.co/open-paws/text_performance_prediction)

### Specific Metric Models
- [Potential Influence Prediction](https://huggingface.co/open-paws/potential_influence_prediction)
- [Level of Rationality Prediction](https://huggingface.co/open-paws/level_of_rationality_prediction)
- [Emotional Impact Prediction](https://huggingface.co/open-paws/emotional_impact_prediction)
- [Perceived Trustworthiness Prediction](https://huggingface.co/open-paws/perceived_trustworthiness_prediction)
- [Perceived Insightfulness Prediction](https://huggingface.co/open-paws/perceived_insightfulness_prediction)
- [Perceived Insightfulness Prediction](https://huggingface.co/open-paws/perceived_insightfulness_prediction)
- [Cultural Sensitivity Prediction](https://huggingface.co/open-paws/cultural_sensitivity_prediction)
- [Effect on Animals Prediction](https://huggingface.co/open-paws/effect_on_animals_prediction)
