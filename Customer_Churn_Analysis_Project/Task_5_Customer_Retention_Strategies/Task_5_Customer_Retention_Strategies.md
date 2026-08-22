# Task 5: Customer Retention Strategies
## Customer Churn Analysis and Prediction — SaiKet Systems Data Analysis Internship

**Task:** 5 of 6 (extended deliverable)

---

## 1. Business Problem
Findings from Tasks 1–4 confirm *who* churns and *why*. This task turns those findings into
concrete, evidence-linked retention actions, and quantifies which currently-active customers
represent the greatest combination of value and risk.

## 2. Customer Lifetime Value (LTV)

### 2.1 Formula and Assumptions
The dataset does not contain profit margin, acquisition cost, or contract-renewal history, so LTV
must be approximated from the variables that do exist: `tenure`, `MonthlyCharges`, `TotalCharges`,
and `Contract`. Two complementary proxies are used:

**Historical LTV** = `TotalCharges`
The actual revenue already collected from the customer to date. This is a fact already in the
dataset, not an estimate.

**Projected LTV** = `MonthlyCharges` × `Expected_Tenure_Months`,
where `Expected_Tenure_Months` = the **average tenure of currently-retained (non-churned)
customers within the same Contract type**, calculated directly from the dataset:

| Contract Type | Avg. Tenure of Retained Customers (months) |
|---|---:|
| Month-to-month | 21.03 |
| One year | 41.67 |
| Two year | 56.60 |

**Assumption stated explicitly:** this treats the average tenure of customers who have *not yet
churned* on a given contract type as a reasonable estimate of how long a similar, still-active
customer will likely remain — a simplification, not a guarantee, since it does not account for
price changes, competitor activity, or individual customer circumstances. It is presented as a
transparent proxy, not a certified financial LTV.

### 2.2 Projected LTV Results
| Metric | Value |
|---|---:|
| Average Projected LTV (all customers) | $2,162.96 |
| Median Projected LTV | $1,692.92 |
| Avg. Projected LTV — Month-to-month | $1,396.36 |
| Avg. Projected LTV — One year | $2,710.58 |
| Avg. Projected LTV — Two year | $3,439.61 |

**Observation:** Despite month-to-month customers often paying similar or higher monthly rates,
their much shorter expected tenure drops their projected LTV well below one- and two-year contract
customers — reinforcing that contract length protects long-run revenue, not just churn rate.

## 3. High-Value Customers at Risk of Churning

Using the Value/Risk priority framework from Task 3 (High Value = at/above median $70.35 monthly
charge; High Risk = month-to-month contract with ≤12 months tenure):

| Priority Segment | Customers | Churn Rate |
|---|---:|---:|
| **High Value + High Risk** | 816 (all-time) / **247 currently active** | 69.73% |
| Low Value + High Risk | 1,178 | 38.62% |
| High Value + Low Risk | 2,708 | 24.70% |
| Low Value + Low Risk | 2,341 | 7.52% |

**247 currently-active customers** sit in the High Value + High Risk quadrant today. Their combined
Projected LTV is a meaningful amount of at-risk future revenue, and the 10 highest-value examples
(illustrative, from `customerID`) each carry a Projected LTV above $2,100 despite being only 3–12
months into their tenure — precisely the profile that historically converts to lost revenue at a
~70% rate.

**Business Prioritization:** These 247 customers should be the very first names on any retention
outreach list — the company already has "High Value + Low Risk" and "Low Value + Low Risk"
customers well-retained; the return on retention spend is highest where risk is high and value is
also high.

## 4. Data-Driven Retention Recommendations

### Recommendation 1 — Convert Month-to-Month Customers to Term Contracts
- **Problem:** Month-to-month customers churn at 42.71% vs. 2.83% for two-year contracts (Task 2).
- **Evidence:** Contract type is the single largest driver of churn risk in both the EDA (Task 2)
  and the Logistic Regression coefficients (Task 4: Month-to-month coefficient +0.529, Two-year
  coefficient -0.815).
- **Recommended Action:** Offer a discounted or perk-added incentive for month-to-month customers to
  switch to a one- or two-year contract, targeted especially at customers past their first 3 months
  (once initial satisfaction is more established).
- **Target Segment:** Month-to-month customers, prioritized by the 247 currently-active High Value +
  High Risk customers.
- **Expected Business Benefit:** Moving customers even from month-to-month to one-year contract
  drops observed churn from 42.71% to 11.27% — a meaningful reduction in the largest single churn
  driver.
- **KPI to Monitor:** Contract-upgrade conversion rate; churn rate of upgraded cohort vs.
  non-upgraded cohort at 90/180 days.

### Recommendation 2 — Migrate Electronic Check Payers to Automatic Payment
- **Problem:** Electronic check payers churn at 45.29%, the highest of any payment method, vs.
  15–19% for bank transfer, credit card, or mailed check (Task 2).
- **Evidence:** Payment method shows the largest churn gap of any billing attribute in the EDA.
- **Recommended Action:** Prompt electronic-check customers to switch to automatic bank transfer or
  credit card payment, potentially with a small first-payment incentive.
- **Target Segment:** All customers currently on Electronic check (2,365 customers).
- **Expected Business Benefit:** Automatic payment methods are associated with roughly a 2–3x lower
  churn rate; even partial migration should measurably reduce churn among this group.
- **KPI to Monitor:** % of electronic-check customers migrated to autopay; churn rate before/after
  migration.

### Recommendation 3 — Proactively Offer Support Add-Ons During Onboarding
- **Problem:** Customers without `TechSupport` or `OnlineSecurity` churn at ~42%, vs. ~15% for
  customers who have these add-ons (Task 2).
- **Evidence:** Both services show among the largest churn-rate gaps of any service variable, and
  both appear among the strongest churn indicators (via their "No internet service" categories) in
  the Task 4 model.
- **Recommended Action:** Bundle a free trial of `TechSupport` and `OnlineSecurity` into new-customer
  onboarding, especially for Fiber optic subscribers.
- **Target Segment:** New customers (0–12 months tenure) subscribing to internet service without
  these add-ons.
- **Expected Business Benefit:** Closing this add-on gap for even a portion of new sign-ups should
  reduce churn in the highest-risk (New (0-12mo)) tenure segment, currently at 47.44%.
- **KPI to Monitor:** Add-on attach rate at signup; 12-month churn rate of customers with vs. without
  the trial add-on.

### Recommendation 4 — Investigate Fiber Optic Service Quality/Pricing
- **Problem:** Fiber optic customers churn at 41.89%, more than double DSL's 18.96%, despite Fiber
  optic being the premium product.
- **Evidence:** Task 2 service analysis and the Task 4 model (Fiber optic coefficient +0.594, one of
  the largest positive coefficients) both flag this independently.
- **Recommended Action:** Conduct a service-quality and pricing review for Fiber optic customers
  (e.g. reliability complaints, price-vs-competitor benchmarking) rather than assuming price alone
  explains the gap.
- **Target Segment:** All Fiber optic customers, especially those also on month-to-month contracts.
- **Expected Business Benefit:** Even a modest reduction in Fiber optic churn would meaningfully move
  the overall 26.54% churn rate, since Fiber optic is a large customer segment.
- **KPI to Monitor:** Fiber optic churn rate over time; customer satisfaction/NPS for Fiber optic
  subscribers specifically.

### Recommendation 5 — Priority Retention Program for High Value + High Risk Customers
- **Problem:** 247 currently-active customers combine above-median monthly charges with a
  month-to-month contract and ≤12 months tenure — this combined profile churned at 69.73%
  historically.
- **Evidence:** Task 3 combined-segment and priority-framework analysis.
- **Recommended Action:** Build a dedicated retention track (personal outreach, loyalty pricing, or a
  "white-glove" onboarding check-in) specifically for customers who fall into this quadrant, rather
  than a generic retention campaign.
- **Target Segment:** The 247 currently-active High Value + High Risk customers, identifiable by
  `customerID` in the Task 3 segmented dataset.
- **Expected Business Benefit:** This is the highest-revenue-per-customer, highest-churn-probability
  group identified anywhere in the analysis — retaining even a fraction of them protects a
  disproportionate share of at-risk revenue relative to the size of the group (247 of 5,174 currently
  active customers, ~4.8%).
- **KPI to Monitor:** Churn rate of the 247-customer cohort over the next 2 quarters vs. the
  historical 69.73% benchmark for this profile.

## 5. Conclusion
Every recommendation above is tied directly to a measured finding from Tasks 1–4, not a generic
best practice. The clearest, most actionable levers are contract length and payment automation —
both are attributes the company can directly influence — while the Fiber optic churn gap and the
247 High Value + High Risk active customers represent the highest-priority areas for investigation
and intervention, respectively.
