# DataAnalytics-L1-CustomerSegmentation

Name: Godword Adjei
Track: Data Analytics
Level: 1
Task: Customer Segmentation Analysis
Internship: Oasis Infobyte — OIBSIP

## Objective

Segment an e-commerce customer base into distinct groups based on purchasing behavior (RFM analysis + K-Means clustering), enabling targeted marketing strategies per segment.

## Dataset

| | |
|---|---|
| Source | UCI Machine Learning Repository — [Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail) |
| Raw file | data/online_retail.xlsx |
| Raw shape | 541,909 transactions × 8 columns |
| Customers analyzed | 4,338 (after removing guest checkouts and cancelled orders) |

## Tools

Python · pandas · NumPy · scikit-learn (KMeans, StandardScaler) · Matplotlib · Seaborn · Jupyter Notebook

## What the notebook does

- **Data cleaning** — removes transactions with no `CustomerID` (guest checkouts), cancelled orders (InvoiceNo starting with "C"), and non-positive quantity/price rows
- **RFM feature engineering** — computes Recency (days since last purchase), Frequency (distinct orders), and Monetary (total spend) per customer
- **Standardization** — scales RFM features with `StandardScaler` before clustering
- **K-Means clustering** — determines the optimal number of clusters (k=4) via the Elbow Method, then fits the final model
- **Cluster visualization** — scatter plots of Recency vs Monetary and Frequency vs Monetary, colored by cluster
- **Cluster profiling** — mean RFM values and customer count per cluster, exported to `outputs/cluster_profile.csv`
- **Marketing recommendations** — a written strategy per customer segment

## Results

| Cluster | Recency (days) | Frequency (orders) | Monetary (£) | Customers | Segment |
|---|---|---|---|---|---|
| 0 | 43.7 | 3.68 | 1,359.05 | 3,054 | Regular / moderate-value customers |
| 1 | 248.08 | 1.55 | 480.62 | 1,067 | Dormant / at-risk (long inactive, low value) |
| 2 | 7.38 | 82.54 | 127,338.31 | 13 | VIP / wholesale-scale buyers |
| 3 | 15.5 | 22.33 | 12,709.09 | 204 | Loyal, frequent, high-value customers |

## Marketing recommendations by segment

- **Cluster 2 (VIP/wholesale):** Only 13 customers, but by far the highest spend and frequency. Assign dedicated account management, priority support, and negotiated bulk pricing to retain them — losing even one materially impacts revenue.
- **Cluster 3 (Loyal/high-value):** Strong candidates for a formal loyalty program, early access to new stock, and personalized upsell offers to grow toward Cluster 2 behavior.
- **Cluster 0 (Regular):** The largest segment by count. Cross-sell and bundle campaigns can increase average order value without needing new customer acquisition spend.
- **Cluster 1 (Dormant/at-risk):** Average last purchase was 248 days ago. Targeted win-back email campaigns with discount incentives are appropriate; if response rates stay low, deprioritize further marketing spend on this group.

## Files

```
DataAnalytics-L1-CustomerSegmentation/
├── CustomerSegmentation.ipynb   # main notebook
├── README.md
├── data/
│   └── online_retail.xlsx        # raw file (UCI ML Repository)
└── outputs/
    ├── cluster_profile.csv
    ├── 01_elbow_method.png
    ├── 02_cluster_scatter.png
    └── 03_customers_per_cluster.png
```

## How to run

```bash
pip install -r ../requirements.txt
jupyter notebook CustomerSegmentation.ipynb
```

Then Cell → Run All.

## Demo video

#oasisinfobyte
