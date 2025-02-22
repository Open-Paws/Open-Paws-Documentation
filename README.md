## Overview
This repository contains everything you need to build AI implementations to support animal advocacy using Open Paws models, data and tools. 

Our ecosystem includes prediction models, a comprehensive knowledge graph and vector database, specialized models, and extensive datasets.

## Documentation

### 🗄️ Knowledge Infrastructure
Documentation for our vector-graph database:

   - [Overview & Quick Start](Knowledge/README.md)
   - [Understanding Our Data Structure](Knowledge/Data_Structure.md)

### 📊 Prediction Models
Documentation for our performance and preference prediction models:

- [Overview & Quick Start](Predictions/README.md)

### 🤖 Specialized Generative AI Models
Documentation for our specialized generative AI models, including Large Language Models (LLMs) and Visual Language Models (VLMs):

- [Overview & Quick Start](Generation/README.md)

## Datasets
Use our HuggingFace datasets for fine-tuning your own generative AI models:

1. **Conversational Datasets**
   - Agentic conversations ([small](https://huggingface.co/datasets/open-paws/agentic_conversations_small)/[medium](https://huggingface.co/datasets/open-paws/agentic_conversations_medium)/[large](https://huggingface.co/datasets/open-paws/agentic_conversations_large))
   - Visual QA ([small](https://huggingface.co/datasets/open-paws/visual_qa_small)/[medium](https://huggingface.co/datasets/open-paws/visual_qa_medium)/[large](https://huggingface.co/datasets/open-paws/visual_qa_large))
   - Reasoning conversations ([small](https://huggingface.co/datasets/open-paws/reasoning_conversations_small) only)

2. **Core Datasets**
   - [Animal advocacy facts](https://huggingface.co/datasets/open-paws/animal_advocacy_facts)
   - [Animal alignment feedback](https://huggingface.co/datasets/open-paws/animal_alignment_feedback)
