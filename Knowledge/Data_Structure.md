# Database Schema

This schema defines the structure of our unified, open-access database designed to support animal advocacy. By integrating data from diverse sources, it supports AI applications such as retrieval-augmented generation (RAG)and model training, as well as general strategic planning and referencing. 

### **Content**

**Purpose**:

The Content class functions as the primary centralized repository for materials related to veganism and animal advocacy, such as articles, reports, blogs, and transcripts. It supports AI applications like semantic search, knowledge graphs, and retrieval-augmented generation (RAG).

**Structure**:

- **summary:** text
- **main_text:** text
- **content_type:** text
- **source_url:** array of texts
- **date**: date
- **scores**: object
    - **good_for_animals:** number
    - **cultural_sensitivity**: number
    - **relevance**: number
    - **insight**: number
    - **trustworthiness**: number
    - **emotional_impact**: number
    - **rationality**: number
    - **influence**: number
    - **alignment**: number
    - **predicted_performance**: number
    - **average_score**: number
- **tags**: array of text
