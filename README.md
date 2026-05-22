# Customer-lifetime-and-value-churn-prediction
# 🛒 Customer Lifetime Value & Churn Prediction

> **Retail cohort analysis + predictive churn model + Power BI dashboard**  
> Tools: Python · SQL · Power BI · scikit-learn

---

## Business Problem

A mid-size retail chain loses ~25% of customers annually. Marketing spends equally across all customers — no differentiation by risk or value. This project answers two questions:

1. **Who is about to leave?** (Churn prediction)
2. **Who is worth saving?** (CLV segmentation)

---

## Project Architecture

```
├── data/
│   ├── raw/                    # Raw transaction data (CSV)
│   └── processed/              # Cleaned + feature-engineered data
├── notebooks/
│   ├── 01_eda.ipynb            # Exploratory data analysis
│   ├── 02_rfm_cohorts.ipynb    # RFM scoring + cohort retention curves
│   ├── 03_clv_model.ipynb      # CLV calculation + customer segmentation
│   └── 04_churn_model.ipynb    # Churn prediction model (XGBoost)
├── sql/
│   ├── cohort_query.sql        # Monthly cohort retention query
│   └── rfm_base.sql            # RFM aggregation query
├── dashboard/
│   └── retail_clv_dashboard.pbix   # Power BI dashboard file
├── outputs/
│   ├── churn_risk_export.csv   # Ranked customer list (risk × CLV)
│   └── executive_summary.pdf   # Non-technical findings brief
└── README.md
```

---

## Dataset

**Source:** [UCI Online Retail Dataset](https://www.kaggle.com/datasets/carrie1/ecommerce-data) — Kaggle  
**Records:** 541,909 transactions · 4,372 customers · 12 months  
**Fields used:** `CustomerID`, `InvoiceDate`, `Quantity`, `UnitPrice`, `Country`

---

## Methodology

### 1. RFM Segmentation
Calculated three behavioural metrics per customer:
- **Recency** — days since last purchase
- **Frequency** — number of unique orders
- **Monetary** — total spend over 12 months

### 2. Cohort Retention Analysis
Grouped customers by acquisition month. Tracked retention rate at 1, 3, 6, and 12 months to identify which cohorts have the highest natural loyalty.

### 3. CLV Calculation
```
CLV = Predicted Survival Rate × Avg Order Value × Purchase Frequency × Gross Margin
```
Segmented customers into four tiers: **Champions, At-Risk, Promising, Lost**.

### 4. Churn Prediction Model
Trained an XGBoost classifier on 80% of data. Features included:
- Recency, Frequency, Monetary (RFM)
- Purchase frequency trend (3-month rolling average)
- Category diversity score
- Days since first purchase (tenure)

**Model Performance:**

| Metric | Score |
|--------|-------|
| Accuracy | 87% |
| Precision (churn) | 83% |
| Recall (churn) | 79% |
| ROC-AUC | 0.91 |

---

## Key Findings

- **Top 20% of customers** generate 68% of total revenue — classic 80/20 rule confirmed
- **Churn risk peaks at month 3–4** post-acquisition — a critical intervention window
- **High-frequency, low-recency customers** are the highest-priority retention targets
- **Cohort Dec–Jan** (holiday shoppers) have 40% lower 6-month retention than Feb–Mar cohorts

---

## Power BI Dashboard

![Dashboard Preview](outputs/dashboard_preview.png)

**Pages:**
1. **Overview** — KPI cards: cohort size, avg CLV, churn rate, revenue at risk
2. **Churn Risk** — Scatter plot of churn probability vs. CLV, drill-through by segment
3. **Cohort Drilldown** — Retention heatmap by acquisition month
4. **Action List** — Prioritised customer export for retention campaigns

---

## Business Impact (Projected)

| Scenario | Outcome |
|----------|---------|
| Target top 150 at-risk customers with retention offer | $48,000 revenue protected |
| Shift 15% of marketing budget to Champions segment | +9% repeat purchase rate |
| Early intervention at month 3 for new cohorts | 5–7% improvement in 12-month retention |

---

## How to Run

```bash
# Clone the repo
git clone https://github.com/NehaKapoor13/retail-clv-churn.git
cd retail-clv-churn

# Install dependencies
pip install -r requirements.txt

# Run notebooks in order
jupyter notebook notebooks/01_eda.ipynb
```

**Requirements:** Python 3.9+ · pandas · numpy · scikit-learn · xgboost · matplotlib · seaborn · Power BI Desktop

---

**Neha** · Data Analyst · Doha, Qatar  
[LinkedIn]((https://www.linkedin.com/in/neha-sammi-kapoor/)) · [GitHub](https://github.com/NehaKapoor13) · nehakapoor213001@gmail.com
