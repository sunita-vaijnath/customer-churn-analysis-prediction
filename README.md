# Customer-Churn-Analysis-Prediction
Customer Churn Analysis and Prediction project developed  Data Analysis project. This project uses exploratory data analysis, customer segmentation, Logistic Regression, churn risk analysis, customer lifetime value analysis, and an interactive Power BI dashboard to identify key churn drivers and provide data-driven customer retention strategies.
## Dataset
`Telco_Customer_Churn_Dataset_.csv` — 7,043 customer records, 21 columns
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

## Conclusion
This project audited, analyzed, segmented, and modeled a 7,043-customer telecom dataset end-to-end.
Churn is concentrated in a clear, actionable profile — new, high-paying, contractually uncommitted
customers without support add-ons — and the trained Logistic Regression model (ROC-AUC 0.842)
translates that profile into a working, interpretable prediction tool the business can act on.
