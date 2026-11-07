# Explainable Machine Learning for Chronic Kidney Disease Prediction

A Data Mining project focused on predicting **Chronic Kidney Disease (CKD) progression** using machine learning and explainable AI techniques.

The project uses longitudinal kidney function data to analyze changes in estimated Glomerular Filtration Rate (eGFR), predict disease progression, and identify factors influencing model predictions.

## Project Overview

Chronic Kidney Disease is a condition in which kidney function gradually decreases over time. Early identification of disease progression can help support clinical research and risk assessment.

This project aims to develop and compare machine learning models for predicting CKD progression using repeated patient measurements.

## Objectives

- Explore and understand longitudinal CKD data.
- Apply data cleaning and preprocessing techniques.
- Analyze kidney function trends using EDA.
- Perform feature engineering and feature selection.
- Train and compare machine learning models.
- Evaluate prediction performance using classification metrics.
- Explain model predictions using SHAP or LIME.

## Dataset

**Dataset:** SMART-C — Longitudinal eGFR Trajectory and Survival Benchmark Dataset

**Source:** [Mendeley Data](https://data.mendeley.com/datasets/xkc9x7v2sr/1)

The dataset contains:

- 5,000 patient records.
- 41,800 longitudinal eGFR observations.
- `baseline.csv` — Baseline patient information.
- `followup.csv` — Repeated kidney function measurements.

### Key Features

| Feature | Description |
|---|---|
| patient_id | Unique patient identifier |
| baseline_egfr | Initial kidney function measurement |
| egfr_value | eGFR measurement during follow-up |
| study_day | Day of follow-up measurement |
| treatment_group | Treatment assignment |
| baseline_glp1 | Baseline GLP-1 therapy indicator |
| egfr_category | Baseline eGFR category |

**Dataset limitation:** Some clinical attributes mentioned in the original proposal, including age, blood pressure, hemoglobin and diabetes status, are unavailable in this dataset. The analysis will focus on the available eGFR-related features.

## Project Workflow

1. **Data Collection:** Load and explore the SMART-C dataset.
2. **Data Preprocessing:** Identify missing values, duplicates, outliers and inconsistent data.
3. **Data Integration:** Combine baseline and follow-up records using patient identifiers.
4. **Data Transformation:** Apply encoding, normalization and standardization where appropriate.
5. **Exploratory Data Analysis:** Visualize eGFR distributions and changes over time.
6. **Feature Engineering:** Construct relevant features from measurements available before prediction.
7. **Model Training:** Train and compare machine learning models.
8. **Model Evaluation:** Evaluate prediction performance.
9. **Explainable AI:** Interpret model predictions using SHAP or LIME.

## Machine Learning Models

The following algorithms are planned:

- Logistic Regression
- Random Forest
- XGBoost

### Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC

## Technologies

- **Python** — Programming language
- **Pandas and NumPy** — Data processing
- **Matplotlib and Seaborn** — Data visualization
- **Scikit-learn** — Machine learning
- **XGBoost** — Gradient boosting
- **SHAP / LIME** — Model explainability
- **Jupyter Notebook / VS Code** — Development environment

## Project Structure

```text
CKD-Progression-Prediction/
│
├── datasets/
│   ├── baseline.csv
│   └── followup.csv
│
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_preprocessing.ipynb
│   ├── 03_exploratory_analysis.ipynb
│   ├── 04_model_training.ipynb
│   └── 05_model_explainability.ipynb
│
├── results/
│
├── README.md
├── requirements.txt
└── .gitignore
```

*This is the planned repository structure. Files will be added as development progresses.*

## Project Status

**In Progress**

Current phase: Data Understanding and Preprocessing.

Future work includes feature engineering, model development, evaluation and explainability.

## Academic Information

**Subject:** Data Mining  
**Department:** Data Science  
**Project Year:** 2026  
**Instructor:** Mr. Muhammad Hussain  
**Student:** Usman Shakir  
**Roll Number:** 24F-DS-122

## Disclaimer

This project is developed for educational and research purposes only. Its predictions are not intended for clinical diagnosis or medical decision-making.
