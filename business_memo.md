# Business Memo: Data Insights Before Campaign Launch

**To:** Product, Marketing & Customer Experience Teams
**From:** Data Analytics
**Date:** May 24, 2026
**Subject:** Key findings from customer data — action required before retention campaign

---

## Executive Summary

Our analysis of the customer base reveals an **overall churn rate of 47.0%**. The data shows clear behavioural patterns that distinguish customers likely to churn. However, several critical data quality issues (specifically future-dated data leakage) must be resolved before launching any predictive models or retention campaigns.

---

## Key Finding 1 — Inactivity is the Strongest Churn Signal

Customers who churn exhibit extreme inactivity. The median recency (days since last order) for a churned customer is **125 days**, meaning they stop interacting with the brand months before we officially consider them "churned."

**Recommendation**: Do not wait for a machine learning model to be built—immediately flag any customer inactive for 60+ days for priority outreach.

---

## Key Finding 2 — High Returns Drive "Silent" Churn (Not Support Tickets!)

Our initial assumption was that angry customers submitting lots of support tickets were the ones churning. **The data proved this wrong.** Churned customers actually submit *fewer* tickets on average (0.74) than retained customers (0.85). 

Instead, **Returns** are the real culprit. Customers with a return rate of >30% have a massive **58.5% churn rate** (compared to the 47% average). They don't complain to support; they simply return the product and silently leave forever.

**Recommendation**: The CX team should intercept customers the moment a high-value return is processed, offering a proactive apology or discount before the customer silently churns.

---

## Key Finding 3 — Low Web Activity Precedes Churn

Churned customers showed significantly lower web/app engagement, logging a median of only **3.0 sessions** compared to **6.0 sessions** for retained customers. A drop in web sessions is a leading indicator that precedes the drop in orders.

**Recommendation**: Set an automated marketing trigger for customers with zero web/app sessions in the last 14 days.

---

## Data Issues Requiring Immediate Attention

1. **57.8% of customer records have a missing `loyalty_tier`** — This severely limits our ability to personalize campaigns based on customer value. The CRM team must fill this gap.
2. **1,872 Future-Dated Orders** — We discovered thousands of orders dated *after* the snapshot date. This is a severe data pipeline issue.
3. **Leakage risk**: If those 1,872 future orders are passed into the predictive model, the model will "cheat" by looking into the future. They must be aggressively filtered out by Data Engineering immediately.

---

## Recommended Next Steps

| Priority | Action | Owner |
|---|---|---|
| High | Flag 60-day inactive customers for outreach | Marketing |
| High | Proactive outreach for customers with >30% return rate | Customer Support |
| Critical | Filter 1,872 future-dated orders to prevent data leakage | Data Engineering |
| Medium | Fill missing `loyalty_tier` data | CRM Team |
| Low | Set up app inactivity trigger (14 days) | Product |
