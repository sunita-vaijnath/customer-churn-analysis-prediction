# Customer Churn Analysis and Prediction

## Organization
SaiKet Systems — Data Analysis Internship

## Business Problem
Telecommunications companies lose recurring revenue whenever customers cancel their subscriptions
("churn"). This project analyzes a real telecom customer dataset to quantify the churn problem,
identify which customers are most at risk, and build a predictive model that can flag likely
churners before they leave — turning a reactive retention process into a proactive one.

## Objectives
1. Clean and prepare the raw dataset for reliable analysis (Task 1).
2. Quantify overall churn and identify the demographic, contract, payment, and service factors most
   associated with churn (Task 2).
3. Segment customers by tenure, monthly charges, and contract type to find the highest-risk,
   highest-value groups (Task 3).
4. Build and evaluate a machine-learning model that predicts individual customer churn risk (Task 4).

## Dataset
`Telco_Customer_Churn_Dataset_.csv` — 7,043 customer records, 21 columns, covering demographics
(gender, senior citizen status, partner, dependents), account information (tenure, contract type,
payment method, paperless billing), subscribed services (phone, internet, streaming, security/backup
add-ons), billing (monthly and total charges), and the churn label.

## Tasks Completed
The SaiKet Systems brief requires a minimum of 4 of 6 possible tasks. This project completes all 6 tasks:

✅ Task 1 — Data Cleaning and Preprocessing
✅ Task 2 — Exploratory Data Analysis
✅ Task 3 — Customer Segmentation
✅ Task 4 — Churn Prediction Model
✅ Task 5 — Customer Retention Strategies
✅ Task 6 — Visualizations

Tasks 1–6 form the core analytical workflow: data quality, exploratory analysis, customer segmentation, and predictive modeling. Tasks 5–6 extend the analysis with business-focused retention recommendations, customer lifetime value estimation, and a dedicated collection of visualizations.

## Technologies
- Python 3
- Pandas, NumPy
- Matplotlib, Seaborn
- Scikit-learn
- Jupyter Notebook

## Project Structure

Customer_Churn_Analysis_Project/
│
├── Telco_Customer_Churn_Dataset_.csv
│
├── Task_1_Data_Cleaning_and_Preprocessing/
│   ├── Task_1_Data_Cleaning_and_Preprocessing.ipynb
│   ├── Task_1_Cleaned_Dataset.csv
│   └── Task_1_Report.md
│
├── Task_2_Exploratory_Data_Analysis/
│   ├── Task_2_Exploratory_Data_Analysis.ipynb
│   └── Task_2_Report.md
│
├── Task_3_Customer_Segmentation/
│   ├── Task_3_Customer_Segmentation.ipynb
│   ├── Task_3_Segmented_Dataset.csv
│   └── Task_3_Report.md
│
├── Task_4_Churn_Prediction_Model/
│   ├── Task_4_Churn_Prediction_Model.ipynb
│   ├── Task_4_Model_Report.md
│   └── model/
│       ├── churn_logistic_regression_pipeline.joblib
│       └── model_comparison_results.csv
│
├── Task_5_Customer_Retention_Strategies/
│   └── Task_5_Customer_Retention_Strategies.md
│
├── Task_6_Visualizations/
│   ├── Task_6_Visualizations.ipynb
│   ├── Task_6_Report.md
│   └── charts/
│       └── (12 saved PNG chart files)
│
├── README.md
└── requirements.txt


## Key Findings
- **Overall churn rate: 26.54%** (1,869 of 7,043 customers).
- **Contract type is the strongest churn lever:** Month-to-month churn 42.71% vs. One year 11.27%
  vs. Two year 2.83%.
- **The first 12 months of tenure is the highest-risk period:** 47.44% churn vs. 6.61% for
  customers with 61–72 months tenure.
- **Electronic check payers churn most** among payment methods (45.29% vs. 15–19% for other
  methods).
- **Missing support add-ons correlate with higher churn:** customers without `TechSupport` or
  `OnlineSecurity` churn at ~42% vs. ~15% for those with the service.
- **The combined highest-risk segment** — new (0–12mo), high-charge (>$70), month-to-month
  customers — churns at **69.04%**, and the "High Value + High Risk" priority segment (816
  customers, 11.6% of the base) churns at **69.73%**, nearly triple the overall baseline.

## Machine Learning Results
Logistic Regression (primary model), evaluated on a stratified 20% held-out test set:

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| **Logistic Regression** | 0.8055 | 0.6572 | 0.5588 | 0.6040 | 0.8420 |
| Decision Tree | 0.7913 | 0.6342 | 0.5053 | 0.5625 | 0.8345 |
| Random Forest | 0.8027 | 0.6579 | 0.5348 | 0.5900 | 0.8351 |

Top churn-risk indicators from the Logistic Regression coefficients: short tenure, month-to-month
contract, fiber optic internet, higher total charges, and paperless billing.

## Customer Lifetime Value (Task 5)
A Projected LTV proxy (`MonthlyCharges` × average tenure of retained customers on the same contract
type) shows Two-year contract customers carry the highest average projected value ($3,439.61) vs.
Month-to-month customers ($1,396.36). **247 currently-active customers** fall into the "High Value +
High Risk" quadrant (above-median charges, month-to-month, ≤12 months tenure) — a group that has
historically churned at 69.73% and represents the top retention priority.

## Business Recommendations
1. **Prioritize the "High Value + High Risk" segment (247 currently-active customers)** — new,
   high-paying, month-to-month customers — for proactive retention outreach.
2. **Incentivize contract upgrades** for month-to-month customers, since churn drops from 42.71% to
   2.83% between month-to-month and two-year contracts.
3. **Migrate electronic-check payers to automatic payment methods**, since electronic check has the
   highest churn rate (45.29%) of all payment methods.
4. **Bundle or proactively offer `TechSupport`/`OnlineSecurity`** during onboarding, since customers
   without these add-ons churn roughly 2.7x more than those with them.
5. **Investigate Fiber optic service quality/pricing**, since Fiber optic churns at 41.89% —
   more than double DSL's 18.96% — despite being the premium product.
6. **Deploy the trained model to score the active customer base monthly** and route
   high-probability churners to the retention team before they cancel.

Full recommendation detail (problem, evidence, action, target segment, expected benefit, and KPI
for each) is in `Task_5_Customer_Retention_Strategies/Task_5_Customer_Retention_Strategies.md`.

## Conclusion
This project audited, analyzed, segmented, and modeled a 7,043-customer telecom dataset end-to-end.
Churn is concentrated in a clear, actionable profile — new, high-paying, contractually uncommitted
customers without support add-ons — and the trained Logistic Regression model (ROC-AUC 0.842)
translates that profile into a working, interpretable prediction tool the business can act on.
