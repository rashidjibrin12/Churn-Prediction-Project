# Customer Churn Prediction — Telco Retention Analytics

A portfolio-style machine learning project focused on predicting customer churn in the telecommunications industry and translating model insights into actionable business recommendations.

## Project Overview
Customer churn is one of the most important challenges for subscription-based businesses. In telecom, churn is especially costly because customer acquisition is expensive, switching costs are low, and lost subscribers often create a compounding revenue impact across multiple service lines.

This project builds an end-to-end churn prediction pipeline using the Telco Customer Churn dataset. The workflow includes:
- data cleaning and preprocessing
- exploratory data analysis
- feature engineering
- model comparison and validation
- explainable AI using SHAP
- business-focused recommendations for retention strategy

The goal is not only to predict churn, but to identify the strongest drivers of churn and turn them into practical retention actions for a telecom business.

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
- pandas
- NumPy
- matplotlib
- seaborn
- scikit-learn
- XGBoost
- SHAP
- Kagglehub
- GitHub for version control and project sharing

## Dataset
The project uses the public Telco Customer Churn dataset from Kaggle.

Dataset characteristics:
- 7,043 customer records
- 21 original features
- target variable: Churn (Yes/No)
- mixed categorical and numerical variables
- includes contract type, payment method, service usage, pricing, tenure, and customer status

This dataset is a strong fit for churn analysis because it captures both behavioral and commercial signals that influence customer retention.

## Methodology
The analysis follows a practical machine learning workflow:

1. Data loading and inspection
   - downloaded the Kaggle dataset
   - reviewed columns, data types, and target distribution

2. Data cleaning
   - corrected data type issues such as string-based TotalCharges
   - handled missing values
   - removed non-predictive identifiers like customerID

3. Feature engineering
   - transformed Yes/No variables into binary numeric values
   - converted categorical fields into model-ready formats
   - created derived features such as tenure groups and monthly charge groups
   - engineered TotalChargesPerMonth to capture customer value patterns

4. Model development
   - compared multiple models including Logistic Regression, Balanced Logistic Regression, Random Forest, and XGBoost
   - assessed each model on prediction quality and business relevance

5. Model interpretation
   - used SHAP values to explain the contribution of features to churn risk
   - linked predictions back to customer behavior and product factors

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
This project presents a complete churn analytics workflow: clean data, engineer value-driving features, compare machine learning models, and translate predictive power into business-ready insights. It is a strong example of applied data science for customer retention and strategic decision-making in a telecom context.
