# Credit Risk — End-to-End Data Engineering & Machine Learning Pipeline

This project implements a complete end-to-end pipeline for credit risk assessment using PySpark, Delta Lake, Spark ML, and MLflow on Databricks.  
The solution follows a Medallion Architecture (Bronze → Silver → Gold) and includes modular feature engineering, model training, experiment tracking, and deploy-ready output.

---

## 1. Project Structure

The solution is organized into independent notebooks reflecting each stage of the pipeline:


notebooks/
│
├── 01_ingestion_and_bronze.py         # Raw ingestion, schema validation, Bronze table
├── 02_feature_engineering.py          # Cleaning, encoding, scaling, Silver/Gold tables
└── 03_model_training.py               # ML training, MLflow tracking, model selection

docs/      # Architecture diagrams and documentation
src/       # (Optional) production pipeline scripts


---

## 2. Objectives

- Build a reproducible data engineering and ML workflow
- Clean and standardize credit application data
- Engineer categorical and numerical features using Spark ML
- Train and evaluate multiple classification models
- Track experiments using MLflow
- Produce a deploy-ready model for inference

---

## 3. Pipeline Overview

**Stage 1 — Ingestion & Bronze (Notebook 01)**
- Load raw CSV into Databricks Workspace Volume
- Standardize column names and schema
- Handle initial inconsistencies
- Persist Bronze table in Delta format

**Stage 2 — Cleaning, Encoding & Feature Engineering (Notebook 02)**
- Identify and categorize feature types programmatically
- Correct invalid category tokens
- Apply StringIndexer and OneHotEncoder
- Normalize numerical features
- Build unified feature vector
- Generate Silver and Gold Delta tables

**Stage 3 — Model Training & MLflow (Notebook 03)**
- Train/test split
- Train three ML models: Logistic Regression, Random Forest, Gradient-Boosted Trees
- Evaluate metrics (F1-score, precision, recall)
- Log models and metrics with MLflow
- Select best-performing model
- Save final model for downstream deployment

---

## 4. Architecture

This project follows a Medallion Architecture:


Raw Data
   ↓
Bronze Layer         # Cleaned schema, minimal transformations
   ↓
Silver Layer         # Categorical fixes, indexing
   ↓
Gold Layer           # Encoded & scaled features, ready for ML
   ↓
ML Training          # F1-based model selection via MLflow
   ↓
Best Model Artifact  # Saved for deployment/inference


---

## 5. Technology Stack

- PySpark (Spark 3.x)
- Delta Lake
- Spark ML (StringIndexer, OneHotEncoder, MinMaxScaler, VectorAssembler)
- MLflow (experiment tracking + model registry)
- Databricks (Community Edition)
- Python 3.10+

---


