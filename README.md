# Explainable Machine Learning for Chronic Kidney Disease Prediction

This is my Data Mining semester project, where I'm exploring how machine learning can help predict the progression of **Chronic Kidney Disease (CKD)**.

I'm using repeated kidney-function measurements to understand how **estimated glomerular filtration rate (eGFR)** changes over time. My goal is to build and compare prediction models, then use explainable AI to understand which available features influence their predictions.

> **Project status:** In progress. Data exploration, integration, and preprocessing demonstrations are underway/completed. Prediction models and explanations have not been built yet.

## What I'm trying to do

CKD can progress at different rates for different people. By studying eGFR measurements taken over time, I want to investigate whether machine learning can identify patients who may experience further kidney-function decline.

For this project, I plan to:
- Explore the data and check its quality.
- Handle missing and inconsistent information carefully.
- Combine baseline and follow-up measurements.
- Examine eGFR trends and create features using information available at prediction time.
- Define a future CKD progression outcome.
- Compare Logistic Regression, Random Forest, and XGBoost.
- Evaluate the models and explain their predictions using SHAP or LIME.

## Dataset

I'm using the **SMART-C Longitudinal eGFR Trajectory and Survival Benchmark Dataset** from [Mendeley Data](https://data.mendeley.com/datasets/xkc9x7v2sr/1).

| File | What it contains |
| --- | --- |
| `baseline.csv` | One baseline record for each of 5,000 patients |
| `followup.csv` | 41,800 records of kidney-function measurements over time |

Some of the fields used in the project are `patient_id`, `baseline_egfr`, `egfr_value`, `study_day`, `treatment_group`, and `egfr_category`.

**Dataset limitation:** The files don't include several clinical factors mentioned in my original proposal, such as age, blood pressure, hemoglobin, and diabetes status. My implementation will focus on the variables that are actually available. The dataset's benchmark provenance and limitations will also be documented; results should not be treated as validated clinical predictions.

## What I've worked on so far

- Loaded and explored both CSV files using Pandas.
- Renamed columns to make them easier to understand.
- Checked missing values, duplicates, repeated patient visits, and unusual eGFR measurements.
- Used the IQR method and box plots to investigate potential outliers without automatically deleting them.
- Joined the baseline and follow-up tables using patient IDs, and checked that the follow-up rows were preserved.
- Compared repeated columns and prepared a merged dataset.
- Demonstrated Min-Max normalization and Z-score standardization.

The scaling exercises are for understanding preprocessing. When I train models, I'll split patients first and fit preprocessing steps using only the training data to avoid data leakage.

## What's next

1. Define a clear CKD progression target and prediction time window.
2. Create a patient-level dataset with features available before the outcome.
3. Explore trends and relationships in the prepared data.
4. Train and compare machine learning models.
5. Evaluate performance using accuracy, precision, recall, F1-score, and ROC-AUC.
6. Use SHAP or LIME to interpret model predictions.

## Tools and libraries

**Currently used:** Python, Pandas, Matplotlib, scikit-learn, Jupyter Notebook.

**Planned for later stages:** NumPy, Seaborn, XGBoost, SHAP or LIME.

## Repository structure

```text
├── datasets/
│   ├── raw/
│   │   ├── baseline.csv
│   │   └── followup.csv
│   └── processed/
│       └── smart_c_merged.csv
├── notebooks/
│   ├── 1_data_understanding.ipynb
│   └── 2_data_preprocessing.ipynb
└── README.md
```

I'll add feature-engineering, modeling, and explainability notebooks as the project progresses.

## Academic details

- **Subject:** Data Mining
- **Department:** Data Science
- **Year:** 2026
- **Instructor:** Mr. Muhammad Hussain
- **Student:** Usman Shakir
- **Roll number:** 24F-DS-122

## Note

This is a university learning and research project. It is **not a medical diagnosis tool** and should not be used to make clinical decisions.
