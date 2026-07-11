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

## Dataset
- Source: Telco Customer Churn (downloaded in the notebook from Kaggle: mustafaoz158/telco-customer-churn)
- Observations: 7,043
- Original columns: 21 (including target `Churn`)

Typical predictive features include tenure, MonthlyCharges, TotalCharges, Contract, InternetService, PaymentMethod, SeniorCitizen, Partner, Dependents, and derived features created during feature engineering.

---

## Key preprocessing & feature engineering (from the notebook)
1. TotalCharges conversion and imputation
   - `TotalCharges` was stored as object strings. Converted to numeric with `pd.to_numeric(..., errors='coerce')` and missing values imputed with the median.
2. Binary mapping
   - Columns with `Yes`/`No` values (e.g., `Partner`, `Dependents`, `PhoneService`, `PaperlessBilling`, `Churn`) were mapped to `1`/`0`.
3. Categorical handling
   - `SeniorCitizen` converted to categorical so it is treated as a category (not an ordered numeric value).
4. Feature creation
   - `TenureGroup` (binned tenure): bins = [0, 12, 24, 48, 60, 72] with labels `0–1 yr`, `1–2 yrs`, `2–4 yrs`, `4–5 yrs`, `5–6 yrs`.
   - `MonthlyChargesGroup` (binned MonthlyCharges): `Low`, `Medium`, `High`, `Premium`.
   - `TotalChargesPerMonth` = `TotalCharges` / (`tenure` + 1) — guard against zero-tenure customers.
5. Identifier removal
   - Dropped `customerID` since it is a unique identifier with no predictive power.
6. Encoding
   - One-hot encoding applied to categorical columns with `pd.get_dummies(..., drop_first=True)` — after encoding the notebook shows 39 columns in the processed dataset.

---

## Train / validation setup
- All train/test splits and cross-validation folds in the project were stratified on the target (`Churn`) to preserve class proportions (stratify = y). Use of stratified splits reduces variance in evaluation metrics for imbalanced binary targets.
- Suggested approach used in the notebook: StratifiedKFold for cross-validation and stratified train_test_split for holdout evaluation.

---

## Handling class imbalance
Two strategies were used/considered:
- Balanced classifier (balanced Logistic Regression) — set `class_weight='balanced'` so the classifier penalizes mistakes on the minority class more heavily.
- (Optional) Resampling approaches such as SMOTE, ADASYN, or undersampling/oversampling via `imbalanced-learn` can be introduced in the pipeline if required by deployment constraints. Tree-based models (Random Forest / XGBoost) can also accept sample weights.

---

## Models trained
- Logistic Regression (baseline)
- Balanced Logistic Regression (using class weights)
- Random Forest
- XGBoost (noted in the notebook as delivering the strongest overall performance)

Hyperparameter tuning and model selection were performed with stratified cross-validation. Prioritize metrics aligned to business goals (see Evaluation below) when choosing the final model.

---

## Evaluation metrics
Report and monitor the following metrics for model comparison (and as implemented in the notebook):
- ROC AUC
- Precision
- Recall (sensitivity) — prioritized when we want to catch potential churners for retention outreach
- F1-score
- Confusion matrix

Note: the notebook indicates XGBoost delivered the best overall performance on the experimentation conducted there. Replace or add concrete metric numbers in this README if you want a static summary of results.

---

## Explainability — SHAP
- SHAP was used to explain model predictions and identify the most influential features driving churn.
- Use `shap.TreeExplainer` for Random Forest and XGBoost for fast, exact (for tree models) explanations.
- Use `shap.LinearExplainer` or `shap.KernelExplainer` for Logistic Regression when needed.
- The notebook's SHAP analysis highlights common churn drivers: Month-to-month (`Contract`), high `MonthlyCharges`, `InternetService` = Fiber optic, `PaymentMethod` (e.g., Electronic check), and short `tenure` / `TenureGroup`.
- Produce both global (summary plot / bar plot) and local explanations (force plot / decision plot) to support business actions and individual-customer outreach.

---

## How to reproduce (example)
1. Create environment and install dependencies

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / macOS
.venv\Scripts\activate     # Windows (PowerShell/CMD)

pip install -r requirements.txt
```

Add packages used in the notebook to requirements.txt (examples): pandas, numpy, scikit-learn, xgboost, shap, matplotlib, seaborn, imbalanced-learn, kagglehub

2. Open/run the notebook
- The main analysis is in `Telco_Customer_Churn_ML.ipynb` — open it in Jupyter / Colab (link above) and run the cells in order.

3. Run training / export model
- If you extract training code into scripts, ensure you use the same preprocessing pipeline and `stratify=y` for splits so results match the notebook.

---

## Key findings (from the notebook)
- XGBoost achieved the strongest overall predictive performance among the models evaluated in the notebook.
- SHAP analysis shows the most important churn drivers are: Month-to-month contracts, high MonthlyCharges, Fiber optic InternetService, certain PaymentMethods (e.g., Electronic check), and shorter tenure.

---

## Next steps / improvements
- Replace placeholder metrics here with exact numeric results from experiments in the notebook if you want a static results table in the README.
- Calibrate predicted probabilities and evaluate business impact (expected ROI) of outreach based on different decision thresholds.
- Add time-aware validation (if churn patterns change over time) or deploy a monitored scoring pipeline with drift detection.
- Experiment with cost-sensitive or uplift modeling to prioritize outreach for customers where retention actions are most effective.

---

## Contact / Author
- Repository: `rashidjibrin12/Churn-Prediction-Project`
- Notebook: `Telco_Customer_Churn_ML.ipynb`
- Author: rashidjibrin12


---

If you want, I can: (1) add a results table with the exact metric numbers from the notebook, (2) generate a requirements.txt from the notebook imports, or (3) add a short `Makefile` or CLI script to run preprocessing and training. Tell me which you prefer.