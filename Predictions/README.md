# Animal Advocacy Prediction Models

## Overview
A suite of prediction models designed to evaluate animal advocacy content through two complementary approaches:
1. Performance prediction based on real-world advocacy metrics
2. Preference prediction based on human and synthetic feedback

### Preference Prediction Models

#### Generic Models
Single input, single output models that predict general consensus:
- Input: Text content
- Output: 0-1 score for each rating dimension
- Use case: Quick evaluation of content's general reception

Available models:
- `alignment_prediction_generic`
- `cultural_sensitivity_prediction_generic`
- `emotional_impact_prediction_generic`
- `effect_on_animals_prediction_generic`
- `influence_prediction_generic`
- `relevance_prediction_generic`
- `rationality_prediction_generic`
- `trustworthiness_prediction_generic`
- `insight_prediction_generic`

#### Personalized Models
Detailed models considering comprehensive persona characteristics:
- Input includes:
  - Content text
  - Advocacy approach metrics (0-1 scales):
    - Diplomacy level
    - Empiricism preference
    - Focus type
    - Intersectionality
    - Rights vs welfare
  - Personal characteristics:
    - Advocate status (yes/no)
    - Age
    - Personality traits (0-1 scales):
      - Agreeableness
      - Conscientiousness
      - Extraversion
      - Neuroticism
      - Openness
  - Demographics:
    - Country
    - Current lifestyle
    - Education level
    - Ethnicity
    - Gender
    - Income level
    - Political affiliation
    - Religious affiliation
    - Role in movement
    - Species (for non-human perspectives)

Available models:
- `alignment_prediction_personalized`
- `cultural_sensitivity_prediction_personalized`
- `emotional_impact_prediction_personalized`
- `effect_on_animals_prediction_personalized`
- `influence_prediction_personalized`
- `relevance_prediction_personalized`
- `rationality_prediction_personalized`
- `trustworthiness_prediction_personalized`
- `insight_prediction_personalized`

### Performance Prediction Models

#### Text Performance Models

**Basic Text Model**
- Input: 768-dimension text embedding vector only
- Output: Performance score (0-1)
- Use case: Quick performance estimation

Available models:
- `performance_prediction_input_text_only`

**Full Details Text Model**
- Input:
  - 768-dimension text embedding vector
  - Advocacy approach metrics (0-1):
    - Alignment
    - Cultural sensitivity
    - Diplomatic vs confrontational
    - Incrementalist vs abolitionist
    - Individual vs institutional
    - Intuitive vs empirical
    - Single issue vs intersectional
    - Welfare vs rights
  - Content metrics (0-1):
    - Emotional impact
    - Influence
    - Insight
    - Rationality
    - Relevance
    - Trustworthiness
  - Contextual information:
    - Intervention type (ACE menu)
    - Outcome type (ACE menu)
    - Language
    - Content type
    - Timestamp

Available models:
- `performance_prediction_input_text_full_details`

#### Image Performance Models

**Basic Image Model**
- Input: 512-dimension image embedding vector only
- Output: Performance score (0-1)
- Use case: Quick visual content evaluation

Available models:
- `performance_prediction_image_input_embedding_only`

**Full Details Image Model**
- Input:
  - 512-dimension image embedding vector (numbers between -1 and 1)
  - Text description of image
  - Advocacy approach metrics (0-1 scales):
    - Alignment
    - Cultural sensitivity
    - Diplomatic vs confrontational
    - Incrementalist vs abolitionist
    - Individual vs institutional
    - Intuitive vs empirical
    - Single issue vs intersectional
    - Welfare vs rights
  - Content quality metrics (0-1 scales):
    - Emotional impact
    - Influence potential
    - Strategic insight
    - Rational argumentation
    - Topic relevance
    - Trustworthiness
  - Contextual information:
    - Intervention type (from ACE menu)
    - Outcome type (from ACE menu)
    - Language
    - Content type
    - Timestamp (posting date/time)

Available models:
- `performance_prediction_input_image_full_details`
