# Thyroid Disease Classification using R and XGBoost

This repository presents a full pipeline for binary classification of thyroid disease using clinical and biological data. The model is trained on the `thyroid.disease` dataset from the `MLDataR` package in R, and uses XGBoost to predict whether a patient is likely to have a thyroid disorder.

This project was completed as part of a supervised machine learning assignment under the Master's program in Web Intelligence and Data Science.

---

## Contents

- Dataset Overview
- Preprocessing Workflow
- Modeling Strategy
- Evaluation Metrics
- How to Use This Repository
- Future Work and Improvements

---

## Dataset Description

The dataset comes from the `MLDataR::thyroid.disease` dataset and contains 3,772 observations (patients), with 27 features describing medical conditions, hormone levels, and treatment history. 

**Target variable**:
- `ThyroidClass`: Categorical (binary) – either `"positive"` (has thyroid disease) or `"negative"` (no thyroid disease)

**Key features**:
- Demographics: Age, Gender
- Medical Treatments: Thyroxine, Antithyroid meds, Surgery
- Hormone Levels: TSH, T3, T4, FTI
- Diagnostic Indicators: Pregnant, Sick, Tumor, Goitre, Psych condition
- Binary categorical variables indicating symptoms, treatment history, and hormone testing results

---

## Data Preprocessing Steps

### 1. Missing Value Treatment

- **Numeric columns**: Imputed using the **median** value of each variable.
- **Categorical columns**: Imputed using the **mode** (most frequent value).
  
### 2. Outlier Detection and Removal

- Outliers in key variables (like `TSH reading`) were visualized using **boxplots**.
- Removed using **IQR filtering** (lower and upper bounds computed from quartiles).

### 3. Encoding and Scaling

- All categorical features (e.g. `ThyroidClass`) were converted to **factors**.
- **Standardization** (zero mean, unit variance) was applied to numerical features using `scale()`.

### 4. Train-Test Split

- The cleaned dataset was split into **training and testing sets** using `caret::createDataPartition()` to maintain class distribution.

---

## Model: XGBoost

XGBoost was selected for its ability to:

- Handle missing values internally
- Capture nonlinear feature interactions
- Avoid overfitting through tree regularization and early stopping

### Key Hyperparameters:

- `eta = 0.1` (learning rate)
- `max_depth = 5`
- `nrounds = 100`
- `objective = "binary:logistic"`

### Training Process:

1. Data converted to XGBoost's `DMatrix` format.
2. Encoded all categorical variables appropriately.
3. Trained on the training set with defined parameters.
4. Model predictions made on test set.

---

## Evaluation Metrics

- **Accuracy**: Proportion of correct predictions out of all predictions.
- **AUC-ROC**: Area under the Receiver Operating Characteristic Curve to evaluate classification quality.
- **Confusion Matrix**: Assesses class-wise performance (especially under class imbalance).

Evaluation scripts and plots are provided in the `notebooks` folder.

---

## How to Use This Repository

### 1. Clone the repository

```bash
git clone https://github.com/your-username/thyroid-classification.git
cd thyroid-classification
