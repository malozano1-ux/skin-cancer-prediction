# Skin Cancer Risk Prediction

Binary classification of skin lesions (Benign vs. Malignant) using a large tabular dataset of 50,000 observations with demographic, behavioral, environmental, and lesion-related predictors.

## Overview

- **Course:** Stats 101C — Statistical Machine Learning, UCLA
- **Authors:** Manuela Lozano, Gwen Sanders, Christopher Kusmana, Mizuki Shitomi, Shaina Dulles, Naman Satija
- **Tools:** R (`glmnet`, `caret`, `MASS`, `tidyverse`)
- **Dataset:** 50,000 training / 20,000 test observations, 49 predictors (20 numerical + 29 categorical)
- **Date:** December 2025

## Problem

Classify skin lesions as benign or malignant from structured clinical and lifestyle survey data. The dataset was approximately balanced (47.7% Benign, 52.3% Malignant) but presented two key challenges: ~8% missingness across all predictors and a mix of informative and noise variables (e.g., favorite color, phone brand, music genre).

## Methods

**Missing data:** Median imputation for numerical variables, mode imputation for categorical variables. Listwise deletion was infeasible — it would have reduced 50,000 training observations to just 334.

**Variable selection (4 methods):**
- Density plots for numerical predictors
- Stacked bar charts for categorical predictors
- Chi-square tests — identified 9 significant categorical predictors (α = 0.01)
- Cross-validation decision tree for importance ranking

9 uninformative predictors dropped: favorite color, favorite cuisine, phone brand, preferred shoe type, music genre, pets, smartwatch use, desk height, zip code.

**Models evaluated:** Ridge logistic regression, LDA, XGBoost, GLM, SVM, random forests, decision trees, KNN

## Key Results

| Model | Kaggle Accuracy |
|---|---|
| Ridge logistic regression (glmnet, α=0, 10-fold CV) | 0.60465 |
| **LDA — final model** | **0.60480** |
| XGBoost, SVM, random forest, KNN | < LDA |

**LDA was selected as the final model** — no nonlinear method consistently outperformed it, suggesting the relationship between predictors and cancer status is largely linear.

## Key Findings

- **Most predictive features:** age, UV exposure, number of lesions, family history, skin tone, immunosuppression, sunscreen frequency
- **Malignant cases vs. benign:** older on average (52.5 vs. 48.0 years), higher UV exposure (3.63 vs. 3.41), larger lesion sizes
- **Chi-square significant categorical predictors:** skin tone, occupation, sunscreen frequency, hat use, clothing protection, tanning bed use, family history, immunosuppressed, skin photosensitivity
- **Simple imputation beat complex imputation:** median/mode outperformed missRanger (random forest-based) due to the large sample size and weak inter-predictor correlation
- Predictive signal is distributed across many variables with small individual effects — accuracy of ~0.60 reflects the inherent limits of survey-style data without imaging features

## Files

| File | Description |
|---|---|
| `FinalProject_Mizuki.Rmd` | Classification models: LDA and ridge logistic regression with 10-fold CV |
| `skin_cancer_report.pdf` | Full written report: EDA, variable selection, model comparison, discussion |

## Full Report

[View on portfolio →](https://manuela-lozano.netlify.app/projects/skin-cancer.html)
