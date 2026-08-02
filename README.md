# 🧪 Unstructured Chemical Data & SDS Parsing Pipeline

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Extraction-150458.svg)](https://pandas.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A robust Python data engineering pipeline designed to ingest unstructured text from Safety Data Sheets (SDS), technical spec sheets, and chemical supplier feeds, parsing them into standardized, audit-ready structured datasets.

---

## 📌 Executive Summary & Business Impact

In chemical procurement and inventory platforms, product data frequently arrives trapped in multi-line raw text files or unstructured vendor catalogs. Key specifications like **CAS Registry Numbers**, **GHS Hazard/Precautionary statements**, and **Chemical Purity levels** lack standard schemas across suppliers.

This repository demonstrates an end-to-end extraction pipeline using Python regular expressions (Regex) and Pandas to:
* **Normalize multi-source raw text** into structured tables.
* **Handle domain-specific edge cases** (e.g., non-standard purity representations like `>= 99.5%`, `98.0% min`, or `99.99%`).
* **Export clean, validated datasets** ready for downstream SQL databases or chemical entity resolution.

---

## 📁 Repository Structure

```text
chemical-data-parsing-pipeline/
├── 01_unstructured_sds_parsing.ipynb   # Main Jupyter Notebook (Regex Pipeline & Edge-Case Refinement)
├── parsed_sds_specifications.csv       # Final clean structured output
├── .gitignore                          # Excludes checkpoints, pycache, and temporary files
└── README.md                           # Project documentation