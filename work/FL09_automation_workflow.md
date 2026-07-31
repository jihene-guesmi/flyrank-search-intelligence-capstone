# Assignment: Ship an Automation Workflow v2 (FL-04)

## 1. Pipeline Architectural Blueprint

We automate the transition from raw data warehouse schemas to validated, public-safe data contracts. This pipeline utilizes a highly structured **Claude Project** containing dedicated operational prompt handoffs to isolate, critique, and format technical specifications.

### Step-by-Step System Flow Diagram:
```text
[Raw Parquet Schema Input] 
           │
           ▼
┌─────────────────────────────────────────────────────────┐
│ STEP 1: GATHER & SCHEMA EXTRACTOR (Parsing Engine)      │
└──────────────────────────┬──────────────────────────────┘
                           │ (Schema Map Markdown)
                           ▼
┌─────────────────────────────────────────────────────────┐
│ STEP 2: ANOMALY CRITIQUE & RISK ASSESSMENT (Guardrail)  │
└──────────────────────────┬──────────────────────────────┘
                           │ (Vulnerability Assessment Log)
                           ▼
┌─────────────────────────────────────────────────────────┐
│ STEP 3: DRAFT COMPLIANT CONTRACT (Synthesis Engine)     │
└──────────────────────────┬──────────────────────────────┘
                           │ (Draft Contract Manuscript)
                           ▼
┌─────────────────────────────────────────────────────────┐
│ STEP 4: DEFENSIVE LANGUAGE REVISER (Format Specialist)  │
└──────────────────────────┬──────────────────────────────┘
                           │
                           ▼
[Final Validated Publication-Safe Data Contract]
```

---

## 2. Programmatic Prompt Configurations & Orchestration

The pipeline is hardcoded into our Claude Project instructions using three strict, sequential operational blocks:

### Block 1: The Schema Parser (Step 1 to Step 2 Handoff)
```text
[SYSTEM ROLE: Data Architect Parse Engine]
INPUT: Raw Parquet directory path string or text log schema.
TASK: Strip out system-specific path noise. Isolate all active columns, metrics, and data types.
OUTPUT: A clean Markdown table mapping out the physical structure of the dataset. Stop and output the table. Do not add conversational text.
```

### Block 2: The Compliance Critique Engine (Step 2 to Step 3 Handoff)
```text
[SYSTEM ROLE: Senior Data Privacy Auditor]
INPUT: The Markdown table output from Block 1.
TASK: Audit the schema columns for compliance vulnerabilities against the FlyRank public safety rule. 
CONSTRAINTS: Explicitly flag the presence of: client_domain, user_ip, unmasked_query_string, or raw_credentials. 
OUTPUT: Generate an Anomaly Vulnerability Assessment Log listing required data transformations or exclusions.
```

### Block 3: The Contract Synthesis & Defensive Reviser (Step 3 to Final Handoff)
```text
[SYSTEM ROLE: Defensive Engineering Technical Writer]
INPUT: The Vulnerability Assessment Log from Block 2.
TASK: Synthesize the final Data Contract manuscript. 
CONSTRAINTS: You must purge all flagged vulnerabilities. Every claim regarding data limits must strictly use defensive, non-causal engineering vocabulary: "observed", "measured", "directional", "decision-support".
OUTPUT: Final Markdown specification file matching the strict repository template code contract.
```

---

## 3. Production Pipeline Runs Log

The automated workflow was executed over 5 distinct, real search intelligence tracking files to prove end-to-end stability.

### Run 1: Core Interaction Fact Table (`fact_content_query_90d.parquet`)
- **Input Parsed:** `client_hash (text), content_hash (text), query_hash (text), impressions_90d (int), clicks_90d (int), avg_position (float), month (text)`.
- **Critique Action:** Dropped absolute date-stamps; enforced token tracking masking over hashes.
- **Output Generated:** Verified clean. Baseline F1 comparison matrices properly mapped.

### Run 2: Content Dimension Profile (`dim_content_assets.parquet`)
- **Input Parsed:** `content_hash (text), publication_epoch (int), crawling_status_code (int), raw_url_string (text)`.
- **Critique Action:** CRITICAL ALERT: `raw_url_string` violates public domain privacy rules. Pipeline triggered structural exclusion, replacing column with dynamic cryptographic `url_obfuscated_id`.
- **Output Generated:** Validated clean asset dimensions sheet.

### Run 3: Search Query Cluster Metadata (`dim_query_clusters.parquet`)
- **Input Parsed:** `query_hash (text), latent_cluster_id (int), silhouette_score (float), sample_clear_text_query (text)`.
- **Critique Action:** CRITICAL ALERT: `sample_clear_text_query` contains private proprietary customer searches. Purged feature completely; forced model evaluation to rely solely on abstract vector indexes.
- **Output Generated:** Compliant cluster schema map.

### Run 4: Historical Ranking Shift Stream (`fact_rank_history_30d.parquet`)
- **Input Parsed:** `content_hash (text), daily_rank_position (int), device_type (text), search_vertical (text)`.
- **Critique Action:** Verified safe. Device categorization grouped into static binary indices (`desktop` / `mobile`).
- **Output Generated:** Logged historical rank monitoring framework.

### Run 5: Click-Through Rate Anomalies Log (`fact_ctr_mismatch_slice.parquet`)
- **Input Parsed:** `content_hash (text), baseline_expected_ctr (float), measured_ctr (float), performance_delta (float)`.
- **Critique Action:** Masked percentage deltas to prevent calculations from leaking direct search scale volumes.
- **Output Generated:** Publication-safe opportunity contract tracking log.

---

## 4. Financial & Operational Time Accounting

To prove systemic utility, pipeline implementation cost metrics were calculated against an expert human designer performing the identical sequence manually:

- **Initial Automated System Setup Cost:** 45 Minutes (Writing instructions, debugging block handoffs).
- **Automated Execution Time Per Dataset:** 45 Seconds (Parsing, auditing, drafting, revising).
- **Total Time Spent across 5 Runs (System):** 48.75 Minutes (Setup + Execution loop).
- **Manual Human Execution Time Per Dataset:** 30 Minutes (Manual inspection, text drafting, careful compliance scrubbing).
- **Total Time Spent across 5 Runs (Manual):** 150 Minutes.
- **Measured Net Time Saved:** **101.25 Minutes Saved** on the first 5 runs alone. System breaks even on Run 2.

---

## 5. Known Failure Modes & The Human Verification Layer

Despite 100% operational pass metrics across the initial dataset runs, the pipeline possesses specific structural blindspots that require hard human engineering reviews:

1. **Complex Semantic Edge-Cases:** If a malicious or highly complex query string passes through an anonymized hash but gets logged inside adjacent meta-description strings, the Critique Engine can pass it over. A human must manually review sample text blocks before final compilation.
2. **Context-Insensitive Word Swapping:** The Defensive Language Reviser operates on explicit token matching rules. If a dataset requires a true causal analysis (such as testing an internal server error impact), the model may falsely flag the word "impact" or "caused" as a safety violation and corrupt the sentence meaning. 
3. **Hallucinated Columns under Noise:** If an input log schema suffers from erratic syntax formatting or truncated text truncation errors, the parsing stage can hallucinate columns that do not exist or miss critical ones.
