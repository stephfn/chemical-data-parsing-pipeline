# 🧪 Unstructured Chemical Data Parsing & Entity Resolution Pipeline

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Extraction-150458.svg)](https://pandas.pydata.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-TF--IDF%20%26%20Cosine%20Similarity-F79A3E.svg)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end Python data engineering and NLP pipeline designed to ingest unstructured text from Safety Data Sheets (SDS), technical spec sheets, and multi-vendor chemical catalog feeds, parsing them into standardized datasets and performing automated entity resolution.

---

## 📌 Executive Summary & Architecture

In chemical procurement and inventory platforms, product data frequently arrives trapped in unstandardized text files or multi-vendor catalog feeds. Key specifications like **CAS Registry Numbers**, **GHS Hazard/Precautionary statements**, and **Chemical Purity levels** lack uniform schemas, while different suppliers use varying synonym conventions for the same chemical (e.g., *IPA* vs. *2-Propanol* vs. *Isopropanol*).

This repository provides a two-stage automated solution:
1. **Stage 1 (Regex Extraction):** Ingest raw vendor strings, extract structured entities, and handle domain-specific purity edge cases.
2. **Stage 2 (Entity Resolution & Machine Learning):** Tokenize chemical strings using Character 3-Gram TF-IDF Vectorization and compute Cosine Similarity to resolve vendor items to a canonical Master Chemical Registry.

---

## 📁 Repository Structure

```text
chemical-data-parsing-pipeline/
├── 01_unstructured_sds_parsing.ipynb      # Stage 1: Regex Parsing & Edge-Case Refinement
├── 02_chemical_entity_resolution.ipynb     # Stage 2: TF-IDF & Cosine Similarity Matching Engine
├── parsed_sds_specifications.csv          # Stage 1 Output: Clean parsed SDS attributes
├── resolved_chemical_catalog_map.csv      # Stage 2 Output: Multi-vendor catalog mapping table
├── .gitignore                             # Excludes checkpoints, pycache, and temporary files
└── README.md                              # Project documentation

---

## 🛠️ Pipeline Modules & Technical Highlights

### **1. SDS Field Parsing Engine (`01_unstructured_sds_parsing.ipynb`)**
* **CAS Registry Numbers:** Pattern matching for standard CAS formats (`\b[1-9]\d{1,6}-\d{2}-\d\b`).
* **GHS Codes:** Automatic extraction of `H-Codes` (Hazard) and `P-Codes` (Precautionary).
* **Iterative Regex Refinement (Purity Specs):** Upgraded initial regex (`v1`) to `v2` (`(?:>=|>|≥)?\s*\b\d{2,3}(?:\.\d{1,3})?\s*%`) to accommodate domain edge cases such as `>= 99.5%`, `98.0% min`, and multi-decimal purity assays.

### **2. Entity Resolution & Deduplication (`02_chemical_entity_resolution.ipynb`)**
* **Character 3-Gram TF-IDF Vectorization:** Captures sub-string and morphological similarities without relying on hardcoded synonym dictionaries.
* **Cosine Similarity Scoring:** Pairwise comparison between raw vendor catalog listings and the canonical registry.
* **Automated Confidence Triage:**
  * **Similarity $\ge$ 0.45:** `MATCH_HIGH_CONFIDENCE` (Auto-mapped to Master ID).
  * **Similarity 0.20 – 0.44:** `NEEDS_HUMAN_REVIEW` (Flagged for human-in-the-loop validation).
  * **Similarity < 0.20:** `NO_MATCH_FOUND` (Prevents database corruption from unlisted compounds).

---

## 🚀 Quickstart & Reproduction

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/stephfn/chemical-data-parsing-pipeline.git](https://github.com/stephfn/chemical-data-parsing-pipeline.git)
   cd chemical-data-parsing-pipeline