# Task 6 Report — Visualizations

## Objective
Consolidate the project's key visual evidence into one notebook, including the box plot, violin
plot, and pair plot the brief specifically requires, with each chart saved as a standalone file.

## Charts Produced (12 total, saved in `charts/`)

| # | Chart | Type | Answers |
|---|---|---|---|
| 1 | Overall churn distribution | Pie | How big is the churn problem? |
| 2 | Tenure distribution | Histogram | How is the customer base distributed by tenure? |
| 3 | Monthly charges by churn | Box plot | Do churners pay more per month? |
| 4 | Tenure by churn | Violin plot | How does the full tenure distribution differ by churn? |
| 5 | Total charges by contract, split by churn | Violin plot | Does the churn/charges relationship hold across contract types? |
| 6 | Tenure / Monthly / Total charges | Pair plot | How do the three numeric features relate to each other and to churn? |
| 7 | Contract type vs churn | Bar | Which contract type is riskiest? |
| 8 | Payment method vs churn | Bar | Which payment method is riskiest? |
| 9 | Demographic churn (senior citizen, partner) | Bar | Which demographics churn more? |
| 10 | Service add-on churn | Bar | Do support add-ons reduce churn? |
| 11 | Segment-level priority churn | Bar | How much riskier is the "High Value + High Risk" segment? |
| 12 | Model feature importance | Horizontal bar | What did the trained model actually learn as top churn drivers? |

## Key Visual Insights
- The **box plot** confirms churned customers have a higher median and IQR of monthly charges than
  retained customers.
- The **violin plot** of tenure by churn status shows churners' tenure distribution is heavily
  concentrated near 0 months, while retained customers spread much more broadly toward higher
  tenure — a sharper visual than a bar chart alone can convey.
- The **pair plot** shows `tenure` and `TotalCharges` are strongly positively related (expected,
  since charges accumulate over time), while churned customers cluster tightly in the low-tenure,
  low-total-charges region across every pairwise combination.
- The **model feature-importance chart**, loaded directly from the saved Task 4 model, independently
  confirms the same top drivers (tenure, contract type, internet service type) that the purely
  descriptive EDA and segmentation work in Tasks 2–3 identified — giving the project two independent
  lines of evidence pointing to the same conclusions.

## Conclusion
All 12 visualizations reproduce or extend a finding already established quantitatively elsewhere in
the project, so this notebook functions as the project's visual summary rather than a set of
standalone charts. Every figure uses the actual dataset and is saved as a PNG file in `charts/` for
reuse in presentations or reports.
