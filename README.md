# Ad Channel Intelligence: Multi-Channel Customer Acquisition Analysis

A marketing analytics project analyzing customer acquisition efficiency across four ad channels (Google Ads, Meta Ads, TikTok Ads, Email) to identify budget misallocation and recommend data-driven reallocation strategy.

<img width="1277" height="730" alt="image" src="https://github.com/user-attachments/assets/8948dd64-8c40-4fd1-a022-e068dcf3bd32" />


## Business Problem

Marketing teams often allocate ad budgets based on channel volume (clicks, impressions, new customers) rather than long-term profitability. This project answers a core business question:

> **"Which acquisition channels are actually generating the most value per dollar spent — and are we investing in the right ones?"**

## Data

Three relational datasets, spanning January–December 2025:

| Dataset | Rows | Description |
|---|---|---|
| `ad_spend.csv` | 1,460 | Daily ad spend by channel |
| `customers.csv` | 1,000 | Customer acquisition channel and first order date |
| `orders.csv` | 2,200 | Order-level revenue transactions |

## Methodology

1. **Data Cleaning & Validation** (Python/Pandas)
   - Standardized data types across all three tables (dates, currency, categorical fields)
   - Verified referential integrity — confirmed zero orphan orders and zero customers with missing acquisition data
   - Validated join keys before merging to prevent silent row duplication/loss

2. **Data Integration**
   - Joined `orders` → `customers` (customer-level revenue rollup)
   - Joined `ad_spend` → `customers`/`orders` (channel-level spend vs. return)
   - Sanity-checked post-join totals against pre-join source sums to confirm no data was lost or duplicated

3. **Metric Engineering**
   - **CAC** (Customer Acquisition Cost) = Total Spend ÷ New Customers
   - **LTV** (Customer Lifetime Value) = Total Revenue ÷ New Customers
   - **LTV:CAC Ratio** = LTV ÷ CAC (the core efficiency metric)
   - **ROAS** (Return on Ad Spend) = Total Revenue ÷ Total Spend
   - Repeat purchase rate by channel

4. **Visualization** (Power BI)
   - Star-schema data model with a dedicated date dimension table
   - DAX measures for dynamic, filter-aware KPI calculation
   - Interactive dashboard with channel-level KPIs, monthly CAC trend, spend distribution, and repeat-purchase behavior

## Key Findings

| Channel | Spend Share | LTV:CAC Ratio |
|---|---|---|
| **Email** | 7% | **2.16x** (best) |
| Meta Ads | 32% | 1.42x |
| TikTok Ads | 16% | 1.18x |
| **Google Ads** | **45%** | **1.12x** (worst) |

**The budget is allocated almost inversely to efficiency.** Email — the most profitable channel per dollar spent — receives the smallest share of budget, while Google Ads — the largest budget line — delivers the weakest return.

### Recommendation

Reallocating a portion of Google Ads spend toward Email is projected to improve overall marketing ROI, based on each channel's demonstrated LTV:CAC performance.

### Limitation

Email's dataset is smaller (100 customers vs. 395 for Google Ads), so its efficiency advantage should be validated with increased investment before a full-scale budget shift — a finding based on a smaller sample warrants a staged rollout rather than an immediate large reallocation.

## Tech Stack

- **Python** (Pandas) — data cleaning, joining, validation, metric calculation
- **Power BI** (DAX, Power Query) — data modeling and interactive visualization

## Repository Structure

```
├── data/
│   ├── ad_spend.csv
│   ├── customers.csv
│   └── orders.csv
├── notebooks/
│   └── data_cleaning_and_analysis.ipynb
├── dashboard/
│   └── ad_channel_intelligence.pbix
├── dashboard_screenshot.png
└── README.md
```

## Author

**Ashok Aryal**
[LinkedIn](#) | [GitHub](https://github.com/ashok9847)
