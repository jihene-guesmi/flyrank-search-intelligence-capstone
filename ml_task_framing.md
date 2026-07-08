# Machine Learning Task Framing: Semantic Intent Mapping

## 1. Machine Learning Task Type
This problem is formulated as a two-stage unsupervised and scoring task:
* **Stage 1 (Unsupervised Clustering):** Grouping high-dimensional query vector embeddings to discover latent user intent categories without manual labeling.
* **Stage 2 (Similarity Scoring):** Calculating cosine similarity scores between the centroids of these query clusters and the vector embeddings of corresponding client URLs to quantify document relevance gaps.

## 2. Target Variable or Proxy
Because explicit human-labeled relevance scores do not exist in the raw search data, the model utilizes a quantitative proxy target: **Semantic Vector Distance**. Specifically, a low cosine similarity score between a high-impression search query cluster and a landing page URL indicates a high probability of a structural content gap.

## 3. Success Metrics
* **Technical Metric:** Silhouette Coefficient (to evaluate the cohesion and separation of the query clusters) and Cosine Similarity variance.
* **Operational Metric:** Precision@Top-K recommendations (verifying if the top-ranked content gap recommendations are manually validated by domain experts as missing relevant text).

## 4. Operational Action Support
The output of this scoring pipeline directly populates an editorial workflow. It provides content managers with a prioritized list of specific URLs that require optimization, along with a list of semantically related search terms that the page currently fails to address structurally.

## 5. Why Machine Learning Beats Fixed Rules
A fixed rule (such as basic SQL keyword matching) completely fails to capture context, synonyms, or latent search intent. For example, a hardcoded rule cannot recognize that the query "how to fix slow loading speed" and the document title "Optimizing Core Web Vitals" share identical underlying intent. 

Machine learning handles this by projecting language into a geometric vector space where context determines proximity. This allows the system to identify non-obvious semantic gaps across millions of keyword variations that a manual rule engine would entirely miss.
