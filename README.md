# Part 1: Data Audit, EDA & Business Understanding
## D2C Customer Churn Capstone

### Overview
Exploratory data analysis and quality audit of a D2C personal-care brand's customer dataset, as part of a churn intelligence capstone project.

### Setup
```bash
pip install -r requirements.txt
```

### Data
Download the dataset from:
`https://drive.google.com/drive/folders/1PmLapJI1VSDgvl_AxARNKwM1MCd3WFX0`

Place all CSV files in the `data/` folder.

### How to Run
1. Install dependencies: `pip install -r requirements.txt`
2. Place datasets in `data/`
3. Open and run `eda_audit.ipynb` from top to bottom

### Repository Contents
| File | Description |
|---|---|
| `eda_audit.ipynb` | Full EDA notebook with 6 charts and comprehensive statistical aggregations |
| `data_quality_report.md` | Data quality findings (highlighting critical future-dated leakage) |
| `business_memo.md` | Business-facing insights memo for the marketing and CX teams |
| `charts/` | Directory containing all saved output chart images |
| `requirements.txt` | Python dependencies |

### Key Findings
- **Overall churn rate:** 47.0%
- **Strongest churn predictor:** Recency (median of 125 inactive days for churned customers)
- **Unexpected Insight:** High return rate (>30%) causes churn to spike to 58.5%. Interestingly, support tickets correlated negatively with churn, implying frustrated customers silently return items and leave rather than complaining to CX.
- 5 data-backed churn-risk hypotheses fully documented in the notebook.