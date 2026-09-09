# DataAnalytics-L1-CleaningData

Name: Godword Adjei
Track: Data Analytics
Level: 1
Task: Cleaning Data
Internship: Oasis Infobyte — OIBSIP

## Objective

Take a raw, messy public dataset and produce an analysis-ready version of it, documenting every cleaning decision along the way.

## Dataset

| | |
|---|---|
| Source | Kaggle — https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data?resource=download |
| Raw file | data/AB_NYC_2019.csv |
| Raw shape | (48895 × 16) |
| Cleaned file | outputs/cleaned_data.csv |
| Cleaned shape | (48895 × 16) |

## Tools

Python · pandas · NumPy · Matplotlib · Seaborn · Jupyter Notebook

## What the notebook does

- **Data quality report** — per-column dtype, null count, null %, cardinality and a sample value, exported to `outputs/data_quality_report.csv`
- **Duplicates** — exact duplicate rows detected and dropped
- **Missing values** — columns more than 60% empty are dropped; remaining numeric nulls filled with the median, categorical nulls with "Unknown"
- **Outliers** — detected with the IQR rule (outside [Q1 − 1.5·IQR, Q3 + 1.5·IQR]) and capped at the fences
- **Consistency** — whitespace stripped, date columns parsed to datetime, column names normalised to snake_case
- **Export** — cleaned CSV plus a before/after comparison table

## Cleaning decisions and rationale

| Issue | Treatment | Why |
|---|---|---|
| Duplicate rows | Dropped | Exact repeats inflate every count and average |
| Column >60% empty | Dropped | Imputing a mostly-empty column invents data |
| Numeric nulls | Median fill | Median resists the skew that the mean does not |
| Categorical nulls | "Unknown" | Missingness is information; don't guess a real category |
| Outliers | Capped, not dropped | Dropping loses a whole record over one bad field |
| ID / coordinate columns | Excluded from capping | An ID is a label, not a measurement; coordinate spread is real geography |

## Results

| Metric | Before | After |
|---|---|---|
| Rows | 48895 | 48895 |
| Columns | 16 | 16 |
| Duplicate rows | 0 | 0 |
| Missing cells | 20141 | 10052 |

Note: `last_review` retains 10052 missing values by design — these correspond to listings with zero reviews, so there is no real date to impute (missingness is meaningful here, per the rationale above).

## Files

```
DataAnalytics-L1-CleaningData/
├── DataCleaning.ipynb          # main notebook
├── README.md
├── data/
│   └── AB_NYC_2019.csv         # raw file (download from Kaggle)
└── outputs/
    ├── cleaned_data.csv
    ├── data_quality_report.csv
    ├── outlier_report.csv
    ├── 01_missing_values.png
    ├── 02_outliers_before.png
    └── 03_outliers_after.png
```

## How to run

```bash
pip install -r ../requirements.txt
jupyter notebook DataCleaning.ipynb
```

Then Cell → Run All.


#oasisinfobyte
