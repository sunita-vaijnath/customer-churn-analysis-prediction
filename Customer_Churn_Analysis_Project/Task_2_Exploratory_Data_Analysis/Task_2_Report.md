# Task 2 Report — Exploratory Data Analysis

## Objective
Quantify the churn problem and identify which customer groups, contract types, payment methods,
services, and charge levels are associated with higher churn.

## Overall Churn
- Total customers: **7,043**
- Churned: **1,869 (26.54%)**
- Retained: **5,174 (73.46%)**

## Key Findings

| # | Finding | Value |
|---|---|---|
| 1 | Overall churn rate | 26.54% |
| 2 | Churn — Month-to-month contract | 42.71% |
| 3 | Churn — One year contract | 11.27% |
| 4 | Churn — Two year contract | 2.83% |
| 5 | Churn — Electronic check payers | 45.29% (highest of all payment methods) |
| 6 | Churn — Mailed check / Bank transfer / Credit card | 19.11% / 16.71% / 15.24% |
| 7 | Churn — tenure 0–12 months | 47.44% |
| 8 | Churn — tenure 61–72 months | 6.61% |
| 9 | Churn — Senior citizens vs non-seniors | 41.68% vs 23.61% |
| 10 | Churn — No partner vs has partner | 32.96% vs 19.66% |
| 11 | Churn — No dependents vs has dependents | 31.28% vs 15.45% |
| 12 | Churn — Fiber optic vs DSL vs No internet | 41.89% vs 18.96% vs 7.40% |
| 13 | Churn — No TechSupport vs has TechSupport | 41.64% vs 15.17% |
| 14 | Churn — No OnlineSecurity vs has OnlineSecurity | 41.77% vs 14.61% |
| 15 | Avg MonthlyCharges — churned vs retained | $74.44 vs $61.27 |
| 16 | Avg TotalCharges — churned vs retained | $1,531.80 vs $2,549.91 |

## Business Interpretation
Churn is concentrated in a recognizable profile: **new customers (under 12 months tenure), on
flexible month-to-month contracts, paying by electronic check, without support add-ons
(TechSupport/OnlineSecurity), and often on Fiber optic internet paying above-average monthly
charges.** Senior citizens and single-household customers (no partner/dependents) also churn more.

Because churners have *higher* monthly charges but *lower* total lifetime charges, the business is
consistently losing high-value customers before it recoups their acquisition cost — the most
expensive kind of churn.

## EDA Conclusion
The overall 26.54% churn rate is high for a subscription business. Contract length and tenure are
the strongest levers: month-to-month, low-tenure customers churn 5–15x more than long-tenure,
two-year-contract customers. Payment automation and support add-ons act as retention anchors, while
Fiber optic internet — despite being the premium product — has the highest churn of any internet
type, warranting a service-quality or pricing review. These findings are carried forward into
customer segmentation (Task 3) and the churn prediction model (Task 4).
