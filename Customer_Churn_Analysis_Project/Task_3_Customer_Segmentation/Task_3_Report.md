# Task 3 Report — Customer Segmentation

## Objective
Segment customers by tenure, monthly charges, and contract type (as specified in the project
brief), quantify churn per segment, and identify the highest-value at-risk group.

## Approach
Rule-based segmentation was used instead of clustering or RFM: the brief names the three
segmentation variables directly, and rule-based bands on named variables stay directly
business-interpretable, unlike a k-means/RFM output that would need translation back into these
same terms. RFM specifically does not apply — this dataset has no purchase recency/frequency data.

## Segment Results

### Tenure Segments
| Segment | Customers | Churn Rate |
|---|---:|---:|
| New (0–12mo) | 2,186 | 47.44% |
| Developing (13–24mo) | 1,024 | 28.71% |
| Established (25–48mo) | 1,594 | 20.39% |
| Loyal (49–72mo) | 2,239 | 9.51% |

### Monthly Charges Segments
| Segment | Customers | Churn Rate |
|---|---:|---:|
| High (>$70) | 3,583 | 35.36% |
| Medium ($35–$70) | 1,725 | 23.94% |
| Low (≤$35) | 1,735 | 10.89% |

### Highest-Risk Combined Segments (Tenure × Charges × Contract, min. 30 customers)
| Segment | Customers | Churn Rate |
|---|---:|---:|
| New (0-12mo) \| High (>$70) \| Month-to-month | 856 | **69.04%** |
| Developing (13-24mo) \| High (>$70) \| Month-to-month | 430 | 49.07% |
| New (0-12mo) \| Medium ($35-$70) \| Month-to-month | 629 | 45.47% |
| Established (25-48mo) \| High (>$70) \| Month-to-month | 539 | 41.74% |

### Lowest-Risk Combined Segments
| Segment | Customers | Churn Rate |
|---|---:|---:|
| New (0-12mo) \| Low (≤$35) \| Two year | 51 | 0.00% |
| Developing (13-24mo) \| Low (≤$35) \| Two year | 65 | 0.00% |
| Loyal (49-72mo) \| Low (≤$35) \| Two year | 365 | 0.82% |

### Value/Risk Priority Framework
(High Value = at/above median $70.35 monthly charge; High Risk = month-to-month contract with
≤12 months tenure)

| Priority Segment | Customers | % of Base | Churn Rate |
|---|---:|---:|---:|
| **High Value + High Risk** | 816 | 11.6% | **69.73%** |
| Low Value + High Risk | 1,178 | 16.7% | 38.62% |
| High Value + Low Risk | 2,708 | 38.4% | 24.70% |
| Low Value + Low Risk | 2,341 | 33.2% | 7.52% |

## Business Interpretation
Churn risk is **compounding, not additive**: each risk factor (low tenure, high charges,
month-to-month contract) independently raises churn, and when all three stack together the churn
rate jumps to nearly 70% — almost triple the overall baseline of 26.54%. The **816 "High Value +
High Risk" customers (11.6% of the base)** are the single highest-priority group for retention
investment, since they pay premium prices but are the least contractually secured.

## Recommendations by Segment
1. **High Value + High Risk (816 customers):** Immediate priority — proactive retention outreach,
   contract-upgrade incentives, and service-quality review within the first 90 days.
2. **New + Month-to-month + High Charges (856 customers, 69.04% churn):** Structured onboarding
   program with an early contract-lock-in offer.
3. **Loyal + Two-year contract customers (near-0% churn):** Low-touch; suitable as a referral/
   advocacy base rather than a retention-spend target.

## Conclusion
Segmenting on tenure, monthly charges, and contract type — and combining them — surfaces a small,
identifiable, high-value customer group responsible for a disproportionate share of churn risk.
This segmentation feeds directly into the customer lifetime value and retention-strategy work in
Task 5.

**Output file:** `Task_3_Segmented_Dataset.csv`
