# Beta Bank Customer Churn Prediction

## Overview

Beta Bank is losing customers month over month. The bank's leadership has determined
that retaining existing customers is significantly more cost-effective than acquiring
new ones — making early identification of at-risk customers a critical business need.

This project develops a binary classification model to predict whether a customer
will leave the bank in the near future, using historical behavioral data and contract
information. The primary objective is to maximize the **F1 score** (minimum
threshold: **0.59** on the test set). The **AUC-ROC** metric is also measured and
compared against F1 to provide a fuller picture of model performance.

---

## Business Problem

Customer churn is a direct threat to revenue stability. By predicting which customers
are likely to leave, the bank can proactively intervene — offering retention incentives
before a customer decides to terminate their contract. The cost of inaction outweighs
the cost of a targeted retention campaign, making a reliable churn prediction model
a high-value business asset.

---

## Dataset

**Source:** `/datasets/Churn.csv`

| Column | Description |
|---|---|
| `RowNumber` | Data string index |
| `CustomerId` | Unique customer identifier |
| `Surname` | Customer surname |
| `CreditScore` | Credit score |
| `Geography` | Country of residence |
| `Gender` | Gender |
| `Age` | Age |
| `Tenure` | Number of years as a bank customer |
| `Balance` | Account balance |
| `NumOfProducts` | Number of banking products used |
| `HasCrCard` | Holds a credit card (1 = Yes, 0 = No) |
| `IsActiveMember` | Active member status (1 = Yes, 0 = No) |
| `EstimatedSalary` | Estimated annual salary |
| `Exited` | **Target** — Customer has left (1 = Yes, 0 = No) |

---

## Project Workflow

### Step 1 — Data Preparation
- Load and inspect the dataset for missing values, duplicates, and data types
- Drop features that carry no predictive value: `RowNumber`, `CustomerId`, `Surname`
- Encode categorical variables: `Geography` (one-hot encoding), `Gender` (label encoding)
- Scale numerical features to normalize ranges across the feature space
- Document and justify every preparation decision

### Step 2 — Class Imbalance Analysis
- Examine the distribution of the target variable `Exited`
- Train an initial model **without** addressing class imbalance
- Evaluate performance using F1 score and AUC-ROC
- Summarize findings: how does imbalance affect the model's ability to detect churners?

### Step 3 — Model Improvement with Imbalance Correction
Apply and compare at least two approaches to handling class imbalance:

- **Class weighting** — penalize misclassification of the minority class via
  `class_weight='balanced'`
- **Upsampling** — increase minority class representation in the training set
  by resampling with replacement
- **Downsampling** — reduce majority class representation to balance the
  training set

Use a dedicated **validation set** to compare models and tune hyperparameters.
Select the best-performing model and configuration before touching the test set.

### Step 4 — Final Testing
- Apply the best model to the **held-out test set**
- Report the final **F1 score** and **AUC-ROC**
- Interpret and compare both metrics:
  - F1 balances precision and recall — critical when false negatives are costly
  - AUC-ROC measures the model's ability to rank positive cases above negative
    ones across all classification thresholds

---

## Performance Target

| Metric | Target |
|---|---|
| F1 Score (test set) | ≥ 0.59 |
| AUC-ROC | Reported for comparison |

---
