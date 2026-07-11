# Churn Prediction — Telco Customer Churn

## Project overview
Predicting customer churn is a high-value application for subscription businesses. This repository contains an end-to-end churn prediction workflow using the Telco Customer Churn dataset. The pipeline covers data ingestion, cleaning, feature engineering, exploratory analysis, model training, evaluation, and explainability. Models trained and compared include:

- Logistic Regression (baseline)
- Balanced Logistic Regression (class-weighted)
- Random Forest
- XGBoost (gradient boosting)

SHAP (SHapley Additive exPlanations) is used to provide model explainability and surface actionable business insights.

Notebook (analysis): [Telco_Customer_Churn_ML.ipynb](https://github.com/rashidjibrin12/Churn-Prediction-Project/blob/main/Telco_Customer_Churn_ML.ipynb)

---

## Quick facts
- Repo: `rashidjibrin12/Churn-Prediction-Project`
- Notebook: `Telco_Customer_Churn_ML.ipynb`
- Dataset source (notebook): mustafaoz158/telco-customer-churn (Kaggle)
- Observations: 7,043
- Original columns: 21 (including target `Churn`)
- Processed features after encoding: 39

---

## Senior-level highlights (what makes this production-ready)
This section summarizes design choices and engineering practices that demonstrate senior-level ML work and make the project easier to evaluate by hiring managers or integrate into production.

- Reproducible preprocessing pipeline: all data cleansing and feature transformations are performed deterministically in the notebook (convert + impute TotalCharges, map yes/no → binary, bin tenure/monthly charges, engineer TotalChargesPerMonth). These steps are easily extracted to a `scikit-learn` ColumnTransformer / pipeline for production.

- Stratified validation and evaluation: all train/test splits and cross-validation are stratified on the `Churn` label to ensure stable, representative evaluation for an imbalanced target.

- Class imbalance handling: demonstrated both model-side (class_weight='balanced' for Logistic Regression) and notes on resampling (SMOTE, ADASYN) and sample-weighting for tree models—appropriate for deployment trade-offs.

- Explainability by design: SHAP analysis is integrated to provide both global and local explanations. Use TreeExplainer with tree models and Linear/KernelExplainer for linear baselines to support business interpretability and auditing.

- Feature engineering with business meaning: tenure bins, per-month charges, and explicit handling of `SeniorCitizen` show domain-driven features rather than blind transformations.

- Clear next steps for production: probability calibration, threshold optimization tied to business ROI, monitoring (data drift & performance), and model retraining cadence.

---

## Architecture & pipeline (recommended extraction from notebook)
A production-ready flow derived from the notebook should include:
1. Data ingestion (raw CSV) → validation (schema checks, nulls, datatypes)
2. Deterministic preprocessing pipeline (imputation, mapping, binning, feature creation, encoding)
3. Feature store or serialized artifact for feature transforms (e.g., saved ColumnTransformer)
4. Model training with stratified CV and hyperparameter search (Grid/Randomized + early stopping for XGBoost)
5. Model evaluation with business metrics and confusion-matrix-driven thresholding
6. Explainability exporter (store SHAP global summaries and example local explanations for auditing)
7. Model packaging (ONNX/PMML or pickle + container) and CI for model tests
8. Deployment: batch scoring or online API + monitoring (drift, latency, prediction distributions)

---

## Modeling decisions & rationale
- Logistic Regression for a simple, interpretable baseline and calibration of probabilities.
- Balanced Logistic Regression to improve recall on minority class without changing data distribution.
- Random Forest for robust, low-effort non-linear baseline with limited hyperparameter tuning.
- XGBoost for best predictive performance and fine-grained regularization controls; used with early stopping to reduce overfitting.

Evaluation prioritizes recall (sensitivity) for the churn class because false negatives (missed churners) represent lost revenue; threshold selection must balance outreach cost vs expected retention benefit.

---

## Evaluation & metrics guidance
- Primary metrics: ROC AUC (overall discriminative power), Recall (for catching churners), Precision (cost control), F1 (balanced view).
- Operationalize a decision threshold based on expected cost/benefit (e.g., cost-per-contact vs expected CLTV uplift if retained).
- Suggested reporting: holdout ROC AUC, confusion matrix, precision/recall at selected threshold (e.g., top 10% predicted risk), and calibration plot (reliability diagram).

---

## Explainability & business insights (from notebook)
- SHAP shows top drivers of churn in the experiments: Month-to-month contract, high MonthlyCharges, Fiber optic InternetService, Electronic check payment method, and shorter tenure groups.
- Use global SHAP summary plots to prioritize product/business interventions and local SHAP force plots to craft personalized outreach messaging.

---

## Production considerations
- Serialization: save preprocessing artifacts (scaler, encoders, ColumnTransformer) and model artifacts with versioned names (e.g., model_v1.pkl) and hashed inputs for traceability.
- CI / unit tests: add tests for preprocessing (schema, expected feature counts, edge cases like tenure=0), model inference (shape, runtime), and integration tests for the pipeline.
- Monitoring: implement data-drift checks (feature distributions, missing rates), model performance monitoring (periodic holdout checks), and alerting for significant degradation.
- Security & privacy: avoid storing raw PII in model artifacts; ensure any customer identifiers are hashed or excluded from training artifacts.

---

## Reproducibility
- Notebook documents the exact preprocessing steps. To reproduce exact results:
  - Use fixed seeds in splits and model training (e.g., random_state=42).
  - Use stratified train/test splits: `train_test_split(..., stratify=y, random_state=42)`.
  - Store the environment packages in `requirements.txt` or `environment.yml`.

---

## How to run (developer-friendly)
1. Create environment and install dependencies

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / macOS
.venv\Scripts\activate     # Windows
pip install -r requirements.txt
```

2. Open the notebook
- Run `Telco_Customer_Churn_ML.ipynb` in Jupyter/Colab. The notebook downloads the dataset (kagglehub), cleans it, trains models, and computes SHAP explanations.

3. Convert to scripts
- Extract preprocessing and training cells to `src/` scripts and expose a CLI for training/prediction. Ensure the same preprocessing pipeline is applied in training and inference.

---

## Suggested repository additions to showcase senior skills
- `src/` with modular preprocessing and training code (pure functions + tests)
- `requirements.txt` and `environment.yml`
- `tests/` with unit/integration tests for transformers and model inference
- A simple `docker/` or `Dockerfile` demonstrating containerized scoring
- `ci/` or GitHub Actions workflow to run tests and linting on PRs
- `notebooks/` with a README linking the Colab notebook and a short narrative
- `docs/` with architecture diagrams and model cards

---

## Limitations
- Notebook experiments are static snapshots — production data drift may require retraining and monitoring.
- Cost/benefit analysis for outreach must be integrated with business metrics and customer lifetime value (CLTV) estimates.

---

## Next steps I can take for you
- Extract exact model metrics from `Telco_Customer_Churn_ML.ipynb` and add a results table in README (recommended).
- Generate a `requirements.txt` from the notebook imports.
- Extract preprocessing into a `src/` pipeline and add unit tests.
- Add a minimal GitHub Actions workflow that runs tests and executes a lightweight notebook test.

---

## Contact / Author
- Author: `rashidjibrin12`
- Repo: `rashidjibrin12/Churn-Prediction-Project`


---

Commit: docs: enhance README with senior-level design, engineering, and production notes
