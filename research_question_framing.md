# Capstone Research Question Framing: Semantic Intent Mapping & Document Relevance

## 1. Selected Lane & Provisional Research Question
* **Provisional Lane:** Semantic Intent Mapping & Document Relevance
* **Research Question:** To what extent can vector embeddings and high-dimensional semantic clustering identify structural topic gaps between a client's existing document library and shifting user search query intent distributions?

## 2. Operational Definitions & Variables
* **Unit of Analysis:** The individual URL (Document) paired with its associated cluster of driving Search Queries.
* **Model Inputs (Features):** Multi-dimensional text embeddings (derived from search phrases and page metadata), historical CTR trends, and impressions.
* **Model Output:** A structural relevance score ranking text gaps, identifying pages that require structural expansion or new content creation.

## 3. Business Decision, Action, and Risk Mitigation
* **The Core Decision:** Determining which low-performing or stagnating URLs possess actual market demand but fail to convert due to a semantic misalignment with user intent.
* **Downstream Action:** Content teams will execute targeted, data-driven editorial rewrites based on the specific semantic gaps identified.
* **Risk / Cost of a Wrong Recommendation:** If the model suggests a rewrite based on a false correlation, the client incurs a double penalty: wasted editorial labor costs and potential loss of stable, existing legacy rankings due to unnecessary text disruption.

## 4. Why This Requires Machine Learning (Beyond Simple Modeling)
This problem cannot be solved using basic SQL filters or simple keyword matching. Human search intent is highly fluid and linguistically diverse (synonyms, phrasing variations, and latent questions). 

Applying unsupervised semantic clustering allows us to map the geometric distances between what users *actually mean* and what a document *currently covers*. Machine learning provides the necessary multi-dimensional analysis to discover these non-obvious thematic overlaps at scale across millions of rows of search data, transforming raw numbers into reproducible, structural content playbooks.
