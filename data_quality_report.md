# Data Quality Report
## D2C Churn Capstone — Part 1

---

## 1. Missing Values

| Dataset | Column | Missing Count | Missing % | Recommended Action |
|---|---|---|---|---|
| customers | loyalty_tier | 1,386 | 57.8% | Impute with 'Unknown' or create a separate category |
| customers | skin_type | 401 | 16.7% | Impute with mode or 'Unknown' |
| orders | rating | 80 | 0.8% | Impute with median rating or drop rows |

*(Note: These are the only columns across all datasets with missing values)*

---

## 2. Duplicate Records

| Dataset | Duplicate Rows | Duplicate IDs | Action |
|---|---|---|---|
| customers | 0 | 0 | None needed |
| orders | 0 | 0 | None needed |
| support_tickets | 0 | 0 | None needed |
| web_events_snapshot | 0 | 0 | None needed |
| churn_labels | 0 | 0 | None needed |

---

## 3. Outliers

- **gross_amount**: Values above 99th percentile (> ₹2,308.62) found in 101 rows.
  - Recommendation: Keep but flag; these are high-value customers (whales).
- **Negative gross_amount**: 0 rows found.
  - Recommendation: No action needed. Returns are correctly handled via the `returned` flag rather than negative transaction amounts.
- **delivery_days**: Orders taking > 9.0 days found in 25 rows.
  - Recommendation: Investigate as potential lost packages or tracking bugs.
- **resolution_hours**: Support tickets taking > 60.0 hours found in 20 rows.
  - Recommendation: Flag these severe outliers for CX team review as they are highly correlated with frustration and churn.

---

## 4. Date Consistency Issues

| Issue | Count | Impact |
|---|---|---|
| Orders before customer signup date | 0 | Data pipeline is functioning correctly |
| Future-dated orders (after snapshot) | 1,872 | **SEVERE LEAKAGE RISK!** These orders occurred *after* 2025-09-30. They must be dropped before aggregations/modeling. |

---

## 5. Join / Key Issues

- **0 customers** in `customers.csv` have no matching churn label.
- **0 customers** in `churn_labels.csv` have no customer profile.
- **0 customers** have no order history.
*(All keys map perfectly 1:1 across the datasets!)*

---

## 6. Leakage Risk Columns

The following columns must **NOT** be used as model input features:

| Column | Reason |
|---|---|
| `churn_next_60d` | The actual target variable we are trying to predict |
| `split` | Administrative column for dataset splitting (Train/Test/Validation) |
| *(None)* | No other explicit future-dated leakage columns were found in the raw data (aside from the 1,872 future-dated orders which must be filtered) |

---

## 7. Summary

| Category | Severity | Status |
|---|---|---|
| Missing values | Medium | Handle before modeling (especially loyalty_tier) |
| Duplicates | Low | Clean |
| Outliers | Low | Flag, keep |
| Date issues | Critical | Drop 1,872 future-dated orders before modeling |
| Leakage columns | Critical | Drop target variable and split columns before feature engineering |
