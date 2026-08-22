# Task 4 Report — Churn Prediction Model

## Objective
Build a churn prediction model using Logistic Regression (as required), compare it against
alternative classifiers, and evaluate all models with metrics appropriate for an imbalanced
business-risk problem.

## Setup
- **Target:** `Churn` (binary, from Task 1 encoding)
- **Features:** All columns except `customerID` and `Churn` (17 features: 3 numeric, 14 categorical)
- **Train/Test split:** 80/20, stratified on `Churn`, `random_state=42`
- **Preprocessing:** `ColumnTransformer` inside a `Pipeline` — `StandardScaler` for numeric
  features, `OneHotEncoder` for multi-category text features, already-binary columns passed
  through — fit only on the training set to avoid data leakage.

## Model Comparison (calculated on the held-out test set)

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| **Logistic Regression** | 0.8055 | 0.6572 | 0.5588 | 0.6040 | 0.8420 |
| Decision Tree (max_depth=6) | 0.7913 | 0.6342 | 0.5053 | 0.5625 | 0.8345 |
| Random Forest (n=200, max_depth=10) | 0.8027 | 0.6579 | 0.5348 | 0.5900 | 0.8351 |

Logistic Regression achieves the highest ROC-AUC (0.842) and the best F1-score (0.604) among the
three models, and is used as the primary model for interpretability.

## Why Accuracy Alone Is Not Enough
Because only 26.5% of customers churn, a model predicting "No churn" for everyone would already
score ~73% accuracy while identifying zero at-risk customers — useless for retention targeting.
**Recall (55.9%)** tells the business the model catches just over half of actual churners in the
test set; **precision (65.7%)** tells the business that when the model flags a customer as likely to
churn, it is correct about two-thirds of the time. Given that missing a churner is typically costlier
than a wasted retention offer, the business may choose to lower the classification threshold below
0.5 to trade some precision for higher recall.

## Top Churn Risk Factors (Logistic Regression coefficients, standardized)

| Feature | Coefficient | Direction |
|---|---:|---|
| Tenure | -1.244 | Longer tenure → lower churn risk |
| Two-year contract | -0.815 | Two-year contract → lower churn risk |
| DSL internet | -0.701 | DSL → lower churn risk vs. other internet types |
| Monthly charges | -0.600 | *(net effect after controlling for other correlated features)* |
| Fiber optic internet | +0.594 | Fiber optic → higher churn risk |
| Month-to-month contract | +0.529 | Month-to-month → higher churn risk |
| Total charges | +0.520 | Higher accumulated charges → higher churn risk |
| Paperless billing | +0.370 | Paperless billing → higher churn risk |
| No internet service (various add-ons) | -0.349 | No-internet customers → lower churn risk |

**Caveat:** these coefficients show statistical association within this dataset, not proven
causation — the model cannot confirm that changing one attribute for a specific customer would
change their actual behavior.

## Business Interpretation
- **Who is most likely to churn:** Short-tenure customers on month-to-month contracts with fiber
  optic internet, higher accumulated charges, and paperless billing — consistent with the Task 2/3
  findings.
- **How the company can use this model:** Score the active customer base monthly; route the
  highest-predicted-probability customers to the retention team proactively, rather than waiting for
  a cancellation request.

## Conclusion
The Logistic Regression model (ROC-AUC 0.842, Accuracy 80.6%) provides both solid predictive
performance and full interpretability via its coefficients, which independently confirm the churn
drivers found in the earlier exploratory and segmentation work. The trained pipeline is saved as
`model/churn_logistic_regression_pipeline.joblib` for reuse.

**Output files:** `model/churn_logistic_regression_pipeline.joblib`, `model/model_comparison_results.csv`
