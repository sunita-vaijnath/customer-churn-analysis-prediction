# Task 1 Report — Data Cleaning and Preprocessing

## Objective
Audit the raw Telco Customer Churn dataset and produce a clean, model-ready dataset for the
downstream EDA, segmentation, and prediction tasks.

## Dataset Snapshot (Before Cleaning)
- Rows: 7,043
- Columns: 21
- Missing values (naive `.isnull()` check): 0
- Duplicate rows: 0
- Duplicate `customerID` values: 0

## Key Findings

| # | Issue Found | Root Cause | Treatment Applied |
|---|---|---|---|
| 1 | `TotalCharges` stored as text (`object`), not numeric | 11 rows contained a blank string instead of a number | Converted to `float64`; blanks imputed with `0` |
| 2 | The 11 blank `TotalCharges` rows | All 11 customers have `tenure = 0` (brand-new sign-ups, not yet billed) — a logical explanation, not random corruption | Imputed with `0` rather than mean/median (fabricating history) or row deletion (losing valid new-customer records) |
| 3 | `SeniorCitizen` encoded as `0/1` while similar columns are `Yes/No` text | Source data convention | Left numeric — already model-ready, no functional issue |
| 4 | Binary text columns (`Partner`, `Dependents`, `PhoneService`, `PaperlessBilling`, `Churn`, `gender`) | N/A | Mapped to `1`/`0` |
| 5 | Multi-category service/billing columns | N/A | Left as readable text; one-hot encoded inside the Task 4 modeling pipeline to prevent data leakage |

No duplicate rows or duplicate customer IDs were found, so no row-removal deduplication was needed.

## Encoding Strategy Rationale
- **Binary Yes/No fields → 1/0 mapping.** Two mutually exclusive categories with a natural
  true/false meaning don't need one-hot dummy columns.
- **Multi-category fields (Contract, PaymentMethod, InternetService, and the six service add-ons)
  → one-hot encoding**, deferred to the Task 4 pipeline. These categories have no inherent order, and
  "No internet service" / "No phone service" are treated as genuine categories (not missing data)
  since they describe a real customer state.
- **`customerID` → excluded from modeling entirely.** Verified as a unique, non-duplicated
  identifier with zero predictive value; kept only as a lookup key for Task 5's high-risk customer
  list.

## Before vs After Summary

| Metric | Before | After |
|---|---|---|
| Shape | (7043, 21) | (7043, 21) |
| Missing values | 0 (naive) / 11 hidden in `TotalCharges` | 0 |
| Duplicate rows | 0 | 0 |
| `TotalCharges` dtype | object (text) | float64 |
| Binary categorical columns | text (`Yes`/`No`) | numeric (`1`/`0`) |

## Conclusion
The dataset required minimal but important cleaning. The single genuine data-quality defect —
blank `TotalCharges` values tied to zero-tenure customers — was identified, explained, and corrected
with a justified imputation rather than a default zero-fill applied blindly. The dataset is now fully
typed, free of missing values and duplicates, and partially encoded, ready for exploratory analysis,
segmentation, and predictive modeling.

**Output file:** `Task_1_Cleaned_Dataset.csv` (7,043 rows × 21 columns)
