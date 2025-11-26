# Credit Risk Pipeline — Databricks, Spark, Delta Lake & MLflow

This project implements a full end-to-end **Credit Risk Assessment Pipeline** using:

- PySpark (Spark 3.x)
- Delta Lake (Bronze → Silver → Gold)
- Spark ML / MLlib
- MLflow (tracking + model artifacts)
- Databricks (Community Edition)
- Unity Catalog Volumes (for model storage)

The pipeline includes raw data ingestion, feature engineering, model training, experiment tracking, batch inference, and scoring outputs — following a **production-oriented Medallion Architecture**.

---

## 1. Project Structure

The solution is organized into independent notebooks reflecting each stage of the pipeline:


notebooks/
│
├── 01_ingestion_and_cleaning.py # Raw → Bronze
├── 02_feature_engineering.py # Silver & Gold preprocessing
├── 03_model_training.py # ML training + MLflow tracking
└── 04_batch_pipeline.py # Batch inference + Scoring layer


docs/ # Architecture diagram (PNG)
src/ # Optional production scripts
README.md



---

## 2. Objectives

- Build a reproducible data engineering and ML workflow
- Clean and standardize credit application data
- Engineer categorical and numerical features using Spark ML
- Train and evaluate multiple classification models
- Track experiments using MLflow
- Produce a deploy-ready model for inference

---

## 2. Objectives

- Build a reproducible Data Engineering + ML pipeline in Databricks  
- Clean and standardize credit application data  
- Encode categorical & scale numerical features  
- Train multiple Spark ML models  
- Evaluate using F1-score  
- Track experiments and artifacts with MLflow  
- Save the best model to a UC Volume  
- Run batch inference and generate a scoring Delta table  

---

## 3. Pipeline Overview

### **Stage 1 — Bronze Layer (Notebook 01)**
- Load raw CSV from Databricks Volumes  
- Standardize column names  
- Remove invalid fields / `_c0`  
- Persist as Delta Lake Bronze  

### **Stage 2 — Silver & Gold (Notebook 02)**
- Fix categorical tokens ("NA" → "unknown")  
- Detect categorical vs numerical columns programmatically  
- Apply:
  - `StringIndexer`
  - `OneHotEncoder`
  - `MinMaxScaler`
- Assemble final `features` vector  
- Save Silver and Gold Delta tables  

### **Stage 3 — Model Training (Notebook 03)**
- Train Logistic Regression, Random Forest, and GBT  
- Evaluate using **F1-score**  
- Track runs, metrics, and artifacts with MLflow  
- Select best-performing model  
- Save artifact to **Unity Catalog Volume**  

### **Stage 4 — Batch Scoring (Notebook 04)**
- Load Gold data  
- Load best model from UC Volume  
- Generate:
  - `prediction`
  - `probability`
- Save scoring results in Delta Lake  

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

- **PySpark (Spark 3.x)**  
- **Delta Lake** for Bronze/Silver/Gold  
- **Spark MLlib** for modeling  
- **MLflow** for experiment tracking + model artifacts  
- **Databricks Community Edition**  
- **Unity Catalog Volumes** for durable model storage  

---

## 6. Results

- Full Medallion pipeline implemented  
- End-to-end ML lifecycle operational  
- Best model saved and reusable  
- Scoring pipeline producing predictions and probability vectors  
- Ready for BI / dashboards / REST APIs  

---

## 7. Next Improvements (Roadmap)

- Hyperparameter tuning (CrossValidator)
- Model explainability (SHAP)
- Databricks Jobs for scheduling
- Streaming inference simulation
- Real-time serving endpoint (Databricks Model Serving)

---

## 8. License

MIT License.