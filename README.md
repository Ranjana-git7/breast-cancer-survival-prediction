# Breast Cancer Survival Prediction using Multi-Omics Survival Analysis

A multi-omics survival modeling framework for breast cancer prognosis using 
clinical and transcriptomic features from the METABRIC cohort. Directly models 
censored time-to-event data — not binary classification.

## Results

| Model | C-index | IBS | 5-Year AUC |
|-------|---------|-----|------------|
| Cox Proportional Hazards | 0.6630 | 0.1315 | **0.6905** |
| Random Survival Forest | 0.6841 | **0.1235** | 0.6573 |
| XGBoost Survival | **0.6847** (95% CI: 0.6267–0.7366) | — | 0.6269 |

- XGBoost Survival achieved the best C-index (0.6847)
- RSF achieved the lowest Integrated Brier Score (0.1235)
- Risk stratification confirmed statistically significant (log-rank p < 0.05)

## Dataset

- **Training:** METABRIC cohort (n=1,903 patients)
- **Features:** Clinical variables, molecular subtypes, somatic mutations, 
  top 200 transcriptomic gene expression features (variance-filtered)
- **Target:** Overall survival time (T) + event indicator (E) — right-censored

## Models

- **Cox Proportional Hazards** — semi-parametric baseline with hazard ratio 
  interpretability
- **Random Survival Forest** — non-parametric ensemble for nonlinear 
  multi-omics interactions
- **XGBoost Survival** — gradient boosted survival with Cox partial likelihood 
  objective

## Methods

- Bayesian hyperparameter optimization (Optuna) with C-index as objective
- Stratified 3-fold cross-validation on training set
- 80/20 train-test split with stratified random seed
- Evaluation: C-index, Integrated Brier Score, time-dependent AUC, 
  calibration curves, Kaplan-Meier risk stratification

## Key SHAP Features (RSF)

Top predictors identified via SHAP explainability:
- **Tumor size** — highest mean SHAP value; larger tumors → higher risk
- **Mutation count** — genomic instability predictor
- **SF3B1** — splicing factor frequently altered in breast cancer
- **MYC** — oncogene
- **JAK1, MAPK14** — immune and stress response pathways
- **NOTCH3, CASP8, TNK2, CXCR1** — developmental and signaling pathways

## Publication

Ranjana L, Jothi Lakshmi S L — *"A Digital Twin Enhanced Wearable Biosignal 
and AI Imaging System for Early Breast Cancer Detection"*  
ICSRF 2025 (UNESCO-supported), Amrita Vishwa Vidyapeetham  
**SSRN Preprint:** https://ssrn.com/abstract=6119426

## Tech Stack

Python · scikit-survival · lifelines · XGBoost · Optuna · SHAP · 
pandas · numpy · matplotlib · Jupyter
