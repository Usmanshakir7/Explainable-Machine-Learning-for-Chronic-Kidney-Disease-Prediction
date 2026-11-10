# Explainable Machine Learning for Chronic Kidney Disease Prediction

This is my **Data Mining semester project**, where I explore whether machine learning can predict a decline in kidney function using baseline information. I worked with the SMART-C longitudinal eGFR dataset, compared three classification models, and used **SHAP** to understand how the models make predictions.

The project was completed as an academic machine-learning exercise, not as a clinical prediction system.

## Project overview

The goal is to predict whether a patient's **estimated glomerular filtration rate (eGFR) will decrease by at least 40% from baseline at the Week 52 visit**.

- **Target = 0:** Less than 40% eGFR decline at Week 52
- **Target = 1:** At least 40% eGFR decline at Week 52
- **Inputs:** Baseline eGFR, treatment group, baseline GLP-1 indicator, and screening eGFR categories

This is a **one-year eGFR-decline classification task**. It does not establish sustained CKD progression, diagnose CKD, or demonstrate treatment effects.

## Dataset

I used the **SMART-C Longitudinal eGFR Trajectory and Survival Benchmark Dataset**, available on [Mendeley Data](https://data.mendeley.com/datasets/xkc9x7v2sr/1).

| Dataset file | Description |
| --- | --- |
| `datasets/raw/baseline.csv` | Baseline information for 5,000 patients |
| `datasets/raw/followup.csv` | 41,800 longitudinal kidney-function records |
| `datasets/processed/smart_c_merged.csv` | Combined baseline and follow-up data |
| `datasets/processed/ckd_model_ready.csv` | Patient-level dataset for model training |

For the final prediction task, I kept patients with baseline eGFR **≥30** and an analysis-flagged measurement at **Week 52**. This gave me **4,362 patients**, one row per patient:

| Week 52 outcome | Patients |
| --- | ---: |
| Less than 40% decline (class 0) | 3,892 |
| At least 40% decline (class 1) | 470 |

Patients without a usable Week 52 measurement were not labeled as healthy; they were excluded from this fixed-visit analysis.

## What I implemented

### 1. Data understanding

I explored the baseline and follow-up files using Pandas, inspected their columns, checked basic statistics, and examined repeated patient visits.

### 2. Data preprocessing

I investigated missing values, duplicates, potential outliers, and redundant columns. I used the IQR method and box plots to explore unusual values rather than deleting them automatically, and I integrated the baseline and follow-up files using patient IDs.

I also demonstrated **Min-Max normalization** and **Z-score standardization**, following the concepts covered in our Data Mining lectures.

### 3. Feature engineering

I created a binary Week 52 outcome using the percentage change from baseline eGFR, encoded categorical baseline features, checked for missing values and repeated patient IDs, and exported the model-ready dataset.

Only baseline information is used as model input. **Week 52 eGFR and the calculated decline percentage are excluded from the predictors** to avoid future-information leakage.

### 4. Machine learning

I trained and compared **Logistic Regression, Random Forest, and XGBoost** using an **80/20 stratified train-test split**. Scaling was fitted on the training set only for Logistic Regression. I used class weighting to help account for the smaller positive class.

I evaluated the models with accuracy, precision, recall, F1-score, ROC-AUC, confusion matrices, and performance curves.

### 5. Model explainability

I used **Random Forest feature importance** and **SHAP** to explain which baseline features influenced predictions. The explainability notebook includes a global importance chart, a SHAP beeswarm plot, an individual waterfall plot, and an importance comparison table.

## Model results

Results below come from the held-out test set of **873 patients**, including **94 positive cases**.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
| --- | ---: | ---: | ---: | ---: | ---: |
| Logistic Regression | 84.88% | 40.87% | 90.43% | 56.29% | 0.9436 |
| Random Forest | **86.03%** | **42.93%** | 90.43% | **58.22%** | 0.9320 |
| XGBoost | 82.82% | 37.93% | **93.62%** | 53.99% | **0.9459** |

**What I learned:** Random Forest achieved the highest F1-score at the tested decision threshold, while XGBoost had the highest recall and ROC-AUC. These are results from one train-test split, so I do not treat the small differences as proof that one model will always perform better.

### Explainability finding

In Random Forest's built-in feature importance, **baseline eGFR** ranked first (importance approximately **0.734**). Screening eGFR categories also contributed, but they overlap with baseline kidney-function information. Feature importance and SHAP describe **model behavior**, not medical causes.

## Repository structure

```text
├── datasets/
│   ├── raw/
│   │   ├── baseline.csv
│   │   └── followup.csv
│   └── processed/
│       ├── smart_c_merged.csv
│       └── ckd_model_ready.csv
├── notebooks/
│   ├── 1_data_understanding.ipynb
│   ├── 2_data_preprocessing.ipynb
│   ├── 3_feature_engineering.ipynb
│   ├── 4_machine_learning.ipynb
│   └── 5_model_explainability.ipynb
└── README.md
```

## Tools and libraries

Python, Jupyter Notebook, Pandas, NumPy, Matplotlib, Seaborn, scikit-learn, XGBoost, and SHAP.

## How to run

1. Download or clone this repository.
2. Open the project folder in VS Code or Jupyter.
3. Install the required Python libraries in your notebook's Python environment:

   ```python
   %pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap
   ```

4. Run the notebooks in numerical order, starting with **01 — Data Understanding**.
5. If needed, change the `project_dir` / local Windows path in the notebooks to match your computer.
6. Notebook 03 saves `ckd_model_ready.csv`, which is used by Notebooks 04 and 05.

The notebooks contain saved outputs, but running them requires access to the dataset files and the appropriate Python environment.

## Limitations

- The prediction target is **a single Week 52 eGFR decline**, not confirmed sustained CKD progression.
- The dataset has **few baseline predictors** and lacks several clinical variables proposed initially, such as age, blood pressure, hemoglobin, and diabetes status.
- Excluding patients without selected Week 52 measurements may introduce **selection bias**.
- The outcome classes are **imbalanced**, and results are based on a **single train-test split**, without external clinical validation.
- Screening eGFR category and baseline eGFR may overlap in information.
- The dataset's benchmark provenance and suitability for real-world clinical prediction have not been independently established.
- The explainability results do not establish causation.

## Academic details

- **Subject:** Data Mining
- **Department:** Data Science
- **Year:** 2026
- **Instructor:** Mr. Muhammad Hussain
- **Student:** Usman Shakir
- **Roll number:** 24F-DS-122

---

**Academic-use disclaimer:** This is a university learning and research project. It is **not a medical diagnosis or decision-support tool**, and its predictions should not be used to make clinical decisions.
