# Database Schema

This schema defines the structure of our unified, open-access database designed to support animal advocacy. By integrating data from diverse sources, it supports AI applications such as retrieval-augmented generation (RAG)and model training, as well as general strategic planning and referencing. 

### **Content**

**Purpose**:

The Content class functions as the primary centralized repository for materials related to veganism and animal advocacy, such as articles, reports, blogs, and transcripts. It supports AI applications like semantic search, knowledge graphs, and retrieval-augmented generation (RAG).

**How to Use**:

Users can query this class to access content and its associated metadata. For example, they might retrieve all blog posts about a specific species, filter scientific studies by publication date or sort social media posts by their alignment with animal rights.

- **summary:** text
- **main_text:** text
- **content_type:** text
- **source_url:** array of texts
- **individual_authors**: ref to `Individual`
- **group_authors**: ref to `Group`
- **language**: ref to `Language`
- **date**: date
- **related_individuals**: ref to `Individual`
- **related_groups**: ref to `Group`
- **related_locations**: ref to `Location`
- **related_events:** ref to `Event`
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

### **Language**

**Purpose**:

The Language class standardizes metadata about languages used in advocacy materials. It ensures global inclusivity and supports multilingual applications in content tagging, filtering, and analysis.

**How to Use**:

Organizations can use this class to filter content by language or to identify language-specific materials for regional campaigns or localization. For example, it allows users to retrieve all advocacy content written in a target language or all groups that produce content in that language.

- **native_name**: text
- **iso_code**: text
- **related_individuals**: ref to `Individual`
- **related_groups**: ref to `Group`
- **related_locations**: ref to `Location`
- **related_events:** ref to `Event`
- **content_written_in_this_language**: ref to `Content`
- **tags**: array of text

### **Location**

**Purpose**:

The Location class provides a consistent framework for linking data to geographic contexts, from regions and countries to specific sites.

**How to Use**:

Users can query this class to retrieve geospatial context for content, events, groups, individuals, events or species. For instance, users could retrieve all events conducted in a specific city or list all factory farms within a specified region.

- **name**: text
- **type**: text
- **description**: text
- **coordinates**: geoCoordinates
- **miles_radius:** number
- **related_individuals**: ref to `Individual`
- **related_groups**: ref to `Group`
- **related_events:** ref to `Event`
- **related_content**: ref to `Content`
- **tags**: array of text

### **Event**

**Purpose**:

The Event class tracks data about advocacy-related activities, including protests, conferences, and campaigns.

**How to Use**:

Users can retrieve detailed event records, including participants, locations, and dates. For instance, they might examine the history of protests in a given region or analyze connections between events and individuals or groups.

- **name**: text
- **type**: text
- **description**: text
- **status**: text
- **start_date**: date
- **end_date**: date
- **participant_count**: integer
- **participating_individuals**: ref to `Individual`
- **participating_groups**: ref to `Group`
- **location**: ref to `Location`
- **related_content**: ref to `Content`
- **tags**: array of text

### **Group**

**Purpose**:

The Group class represents organizations, coalitions, businesses and other entities related to animal advocacy or animal exploitation, whether allies, adversaries, or neutral stakeholders.

**How to Use**:

Organizations can query this class to analyze a group’s role, strategies, and affiliations. For example, users might retrieve data on groups advocating for animal rights or lobbying groups opposing regulations on factory farming.

- **name**: text
- **type**: text
- **description**: text
- **status**: text
- **location**: ref to `Location`
- **language**: ref to `Language`
- **members**: ref to `Individual`
- **membership_count**: integer
- **alignment_score**: number
- **advocacy_approach**: object
    - **incrementalist_vs_abolitionist**: number
    - **individual_vs_institutional**: number
    - **solely_animal_vs_intersectional**: number
    - **welfare_vs_rights**: number
    - **diplomatic_vs_confrontational**: number
    - **intuitive_vs_empirical**: number
- **adversarial_approach**: object
    - **values_vs_profit**: number
    - **short_term_vs_long_term**: number
    - **innovation_vs_tradition**: number
    - **pro_regulation_vs_anti_regulation**: number
    - **transparency_vs_misinformation**: number
    - **passive_vs_active**: number
- **contact_details**: array of objects
    - **type**: text
    - **value**: text
    - **verified**: boolean
- **social_media**: array of objects
    - **platform**: text
    - **link**: text
    - **followers**: integer
    - **verified**: boolean
- **related_locations**: ref to `Location`
- **related_events:** ref to `Event`
- **related_content**: ref to `Content`
- **tags**: array of text

### **Individual**

**Purpose**:

The Individual class captures data on people participating in animal advocacy or engaged in animal exploitation, including activists, policymakers, corporate executives, politicians and industry stakeholders.

**How to Use**:

Users can search for individuals by affiliations, roles, or activities. For example, an organization might analyze an influential policymaker to anticipate their potential impact on campaigns and the best approaches for reaching out to them.

- **first_name**: text
- **last_name**: text
- **description**: text
- **affiliated_groups**: ref to `Group`
- **alignment_score**: number
- **advocacy_approach**: object
    - **incrementalist_vs_abolitionist**: number
    - **individual_vs_institutional**: number
    - **solely_animal_vs_intersectional**: number
    - **welfare_vs_rights**: number
    - **diplomatic_vs_confrontational**: number
    - **intuitive_vs_empirical**: number
- **adversarial_approach**: object
    - **values_vs_profit**: number
    - **short_term_vs_long_term**: number
    - **innovation_vs_tradition**: number
    - **pro_regulation_vs_anti_regulation**: number
    - **transparency_vs_misinformation**: number
    - **passive_vs_active**: number
- **demographics**: array of objects
    - **type**: text
    - **value**: text
    - **verified**: boolean
- **language**: ref to `Language`
- **location**: ref to `Location`
- **contact_details**: array of objects
    - **type**: text
    - **value**: text
    - **verified**: boolean
- **social_media**: array of objects
    - **platform**: text
    - **link**: text
    - **followers**: integer
    - **verified**: boolean
- **related_content**: ref to `Content`
- **tags**: array of text
