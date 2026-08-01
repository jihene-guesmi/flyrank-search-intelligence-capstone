# Capstone Report — Structured Content Archetype Clustering

- **Author:** Jihene Guesmi
- **Lane:** Structured Content Archetype Clustering
- **Repo:** https://github.com
- **Date:** August 2026

## 1. Problem framing
This framework serves as a directional, data-driven decision-support utility to guide content resource allocation and metadata rewrite priorities. The unit of analysis is the unique document asset (`content_hash`) evaluated across a fixed logging window. The machine learning pipeline outputs an unsupervised cluster category mapping coupled with a localized vector distance priority score. 

A human editor uses this output to target specific pages for deep structural textual expansion (`REWRITE_CONTENT_EXPANSION`) or positional entity updates, bypassing stable high-performing pages. The operational cost of a wrong call is high human resource hours wasted manually rewriting pages that are either unindexed, highly transactional, or structurally optimal but restricted by external search layout shifts. Machine learning helps resolve this by modeling complex, non-linear traffic friction points that static human thresholds fail to capture.

## 2. Data safety
This analysis utilizes the multi-panel 90-day time-series fact matrices (`fact_content_query_90d.parquet`) from the official FlyRank release, localized tightly to a stable tracking month (`month=2026-03`). To ensure absolute public safety and data compliance, we deliberately excluded all raw search text entries, client brand domains, credentials, and geographic location markers. 

To eliminate severe data leakage risks, we stripped out all future-window tracking loops, post-refresh conversion logs, and target-derived trend indicators (`trend_direction`, `trend_pct`). Pseudonymous keys such as `client_hash` and `query_hash` were utilized strictly for grouping validation constraints and non-overlapping stratification partitions; they were never exposed to the model instance feature arrays. No client-identifying data elements exist anywhere inside the `work/` folder.

## 3. Baseline
Our baseline is a transparent, linear threshold score designed to replicate a human-written business rule:
$$\text{Baseline Score} = (\text{impressions\_90d} \times 0.7) - (\text{clicks\_90d} \times 2.0)$$
An asset is flagged as an intent-mismatch gap if its baseline score falls within the top 15% tier of the test data slice. This represents a fair comparison because it utilizes the exact same feature inputs and operates on identical data splits as the machine learning configurations. Evaluated on the time-aware evaluation future window, this heuristic rule achieves a macro F1-score of 0.825, a target class precision of 0.714, and a target class recall of 0.680.

## 4. Model / analysis
Our methodology implements a dual-model structure consisting of a Supervised Random Forest Classifier control and an Unsupervised Two-Stage K-Means Clustering Distance Engine. Tree-based ensembles fit this lane perfectly because search interaction metrics mirror an aggressive, exponential long-tail distribution skew that breaks standard distance metrics without fragile preprocessing. 

Concurrently, K-Means clustering groups the feature space into 3 latent intent groups without relying on human target definitions. The exact feature list is restricted strictly to non-leaked interaction properties: `impressions_90d` and `avg_position`. The proxy target definition is formulated in one sentence: *A high geometric vector distance between a high-impression content asset and its nearest healthy conversion cluster centroid indicates a high probability of a structural search intent gap.*

## 5. Evaluation
We enforce an honest, chronological **Time-Aware Split Validation Design** to prevent historical data leakage. The dataset is ordered sequentially by its tracking logs; the oldest 80% fraction serves as the training set, while the final, completely unseen future 20% slice serves as the evaluation window. 

### Side-by-Side Evaluation Matrix:
- **Task Base Rate (Majority Class / Normal Rows):** 85.0%
- **W4 Baseline Heuristic Rule:** Macro F1: 0.825 | Precision: 0.714 | Recall: 0.680
- **Model A (Random Forest Control):** Macro F1: 0.977 | Precision: 0.962 | Recall: 0.941
- **Model B (K-Means Vector Distance):** Macro F1: 0.812 | Precision: 0.845 | Recall: 0.812

Our error analysis shows that Model A experiences boundary failures (false negatives) exclusively where impressions hover right at the 2,000 threshold margin due to hard decision-tree cuts. Model B introduces sparse false positives on massive traffic outliers that possess balanced conversions, as their raw dimensional scale naturally pushes them far from dense group centers.

## 6. Interpretation
The unsupervised K-Means engine successfully isolated three functional performance archetypes: a high-density, low-visibility core cluster (Page 2+ terms), a highly optimized core conversion group (Page 1 anchors), and a distinct, high-distance outer fringe tracking massive impressions alongside near-zero clicks (Intent Gaps). 

Feature importance routines confirm that `impressions_90d` holds the primary relative feature weight (0.742), followed by `avg_position` (0.258). A notable negative result observed during testing was that tracking position variations below position 40 displayed nearly zero correlation with click conversions, proving that text optimization has a measurable impact only on assets that have already crossed basic domain indexing thresholds.

## 7. Recommendation
Our output generates a ranked, prioritized action playbook with integrated safety guardrails:
1. **High-Distance Outer Fringe Outliers:** Action: `REWRITE_CONTENT_EXPANSION` | Reason Code: `INTENT_MISALIGNMENT_GAP`. Editors must completely restructure H1/H2 metadata components to map exactly to the dominant query intent.
2. **Stable Page-1 Anchors:** Action: `PROTECT_MONITOR` | Reason Code: `BASELINE_CONVERSION_STABILITY`. Maintain current text blocks; avoid unnecessary edits to prevent algorithmic drift.

A FlyRank editor can run this prioritized pipeline queue tomorrow by sorting assets by descending distance scores. Our operational confidence is limited strictly to stable search indexing periods. To ensure total brand compliance, automated adjustments are blocked via a hardcoded **No-Go List** filter if an asset triggers a safety flag for highly regulated content, checkout pathways, or active A/B tests.

## 8. Reproducibility
To fully reproduce all analytical findings, data density distributions, and multi-model matrix evaluations from a fresh repository clone, execute the following commands in sequence:

```bash
# Clone the verified capstone repository framework
git clone https://github.com.git
cd flyrank-search-intelligence-capstone

# Execute the core trace pipelines cell-by-cell in order
python -m venv env
source env/bin/activate
pip install numpy pandas scikit-learn seaborn matplotlib duckdb

# Run the complete notebooks sequence to re-generate receipts
# w05_model.ipynb -> w06_validation_audit.ipynb -> w07_action_playbook.ipynb
```
- **Global Random State Seed Variable:** `42` (Enforced across all NumPy partitions, Random Forest initializations, and K-Means iterations).
- **Environment Delta Highlights:** `duckdb==1.0.0`, `scikit-learn==1.2.2`, `pandas==2.0.3`. All training metrics receipts and exported analytical charts are written deterministically to `work/outputs/` and `work/figures/`.
