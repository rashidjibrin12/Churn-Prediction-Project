# Customer Churn Prediction - Telco Retention Analytics

A machine learning project focused on predicting customer churn in the telecommunications industry and translating model insights into actionable business recommendations.

## Project Overview
Customer churn is one of the most important challenges for subscription-based businesses. In telecom, churn is especially costly because customer acquisition is expensive, switching costs are low, and lost subscribers often create a compounding revenue impact across multiple service lines.

This project builds an end-to-end churn prediction pipeline using the Telco Customer Churn dataset. The goal is not only to predict churn, but to identify the strongest drivers of churn and turn them into practical retention actions for a telecom business.

## Business Questions
This analysis was designed to answer the following questions:
1. Which customer segments are most likely to churn?
2. Which service and contract features increase churn risk the most?
3. What pricing or product indicators are associated with churn?
4. Which customers should be prioritized for retention campaigns?
5. What actions can a telecom provider take to reduce churn before it happens?

## Skills Demonstrated
- Data cleaning and preprocessing
- Exploratory data analysis (EDA)
- Feature engineering and business variable transformation
- Categorical encoding and model-ready data preparation
- Machine learning model training and comparison
- Classification performance evaluation
- Business interpretation of model output
- Explainable AI with SHAP
- Communication of insights for non-technical stakeholders

## Tools Used
- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost
- SHAP
- Kagglehub
- GitHub for version control and project sharing

## Dataset
The project uses the public Telco Customer Churn dataset from Kaggle.

Dataset characteristics:
- 7,043 customer records
- 21 original features
- Target variable: Churn (Yes/No)
- Mixed categorical and numerical variables
- Includes contract type, payment method, service usage, pricing, tenure, and customer status

This dataset is a strong fit for churn analysis because it captures both behavioral and commercial signals that influence customer retention.

## Methodology
The analysis follows a practical machine learning workflow:

1. Data loading and inspection
   - Downloaded the Kaggle dataset
   - Reviewed columns, data types, and target distribution

2. Data cleaning
   - Corrected data type issues such as string-based TotalCharges
   - Handled missing values
   - Removed non-predictive identifiers like customerID

3. Feature engineering
   - Transformed Yes/No variables into binary numeric values
   - Converted categorical fields into model-ready formats
   - Created derived features such as tenure groups and monthly charge groups
   - Engineered TotalChargesPerMonth to capture customer value patterns

4. Model development
   - Compared multiple models including Logistic Regression, Balanced Logistic Regression, Random Forest, and XGBoost
   - Assessed each model on prediction quality and business relevance

5. Model interpretation
   - Used SHAP values to explain the contribution of features to churn risk
   - Linked predictions back to customer behavior and product factors

<img width="1428" height="1060" alt="{B3A88774-6159-4ACA-9D14-04C1BA66A941}" src="https://github.com/user-attachments/assets/08048701-88d2-44e5-bfcb-9734d5d22929" />

<img width="1591" height="1033" alt="{01CA76CA-F377-4D63-977C-5F535D8C4621}" src="https://github.com/user-attachments/assets/3949a2d4-60aa-4d40-9316-740216ddf656" />



## Key Findings
The notebook reveals several recurring churn patterns that are highly relevant to telecom retention strategy:

- Customers on month-to-month contracts are much more likely to churn than those on annual or multi-year plans.
- Higher monthly charges are strongly associated with churn risk.
- Fiber optic internet service is a major churn driver compared with DSL or other service types.
- Customers without online security features show a higher probability of leaving.
- Shorter tenure is closely linked to greater churn risk, especially for new or recently acquired customers.
- Payment behavior and service usage patterns also matter; customers relying on electronic check payments and limited service bundles appear more vulnerable.
- XGBoost delivered the strongest overall model performance among the tested algorithms, making it the most effective choice for prediction in this project.

SHAP analysis confirmed that the most influential predictors were not random; they aligned with clear business signals such as contract structure, service type, pricing, and customer engagement.

## Recommendations
Based on the findings, the following actions would help reduce customer churn:

- Target at-risk customers early: prioritize customers with short tenure and month-to-month contracts for proactive retention outreach.
- Improve retention for high-risk pricing segments: review affordability concerns for customers with high monthly charges.
- Promote bundled protection services: encourage customers to adopt online security, backup, and support packages to reduce churn risk.
- Reassess fiber customer experience: investigate dissatisfaction drivers for Fiber optic customers and improve onboarding and service support.
- Design personalized retention campaigns: use churn probability scores to trigger interventions for specific customer groups.
- Strengthen onboarding and customer education: new customers need clear value communication and support to reduce early churn.
- Use explainable AI in decision-making: leverage SHAP-driven insights to guide marketing, customer success, and product strategy decisions.

## Business Impact
This project demonstrates how machine learning can move beyond prediction and become a decision-support tool for business teams. By combining strong predictive performance with interpretable insights, the model helps stakeholders understand not only who is likely to churn, but why it happens and what interventions are most likely to work.

## Repository Contents
- `Telco_Customer_Churn_ML.ipynb` — full analysis notebook
- `README.md` — project summary and portfolio documentation

## Summary
This project follows a complete churn analytics workflow; clean the data, engineer value-driving features, compare machine learning models, and translate predictive power into business-ready insights. 
