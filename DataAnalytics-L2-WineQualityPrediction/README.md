# DataAnalytics-L2-WineQualityPrediction

Name: Godword Adjei
Track: Data Analytics
Level: 2
Task: Wine Quality Prediction
Internship: Oasis Infobyte — OIBSIP

## Objective

Train and compare multiple classification models predicting wine quality from physicochemical properties (acidity, density, alcohol, etc.).

## Dataset

| | |
|---|---|
| Source | UCI Machine Learning Repository — [Wine Quality Dataset](https://archive.ics.uci.edu/dataset/186/wine+quality) |
| Raw files | data/winequality-red.csv, data/winequality-white.csv |
| Combined shape | 6,497 samples × 12 features (11 chemical properties + quality score) |
| Missing values | 0 |

## Tools

Python · pandas · NumPy · scikit-learn (RandomForestClassifier, SGDClassifier, SVC) · Matplotlib · Seaborn · Jupyter Notebook

## What the notebook does

- **EDA** — distribution plots for all 11 chemical features, correlation heatmap
- **Class imbalance handling** — raw quality scores (3–9) are heavily skewed toward 5–6; binned into 3 balanced-ish classes (`low` 3–4, `medium` 5–6, `high` 7–9) to make the classification problem tractable
- **Stratified train/test split** — preserves class ratios in both sets
- **3 classifiers trained** — Random Forest, SGD Classifier, and SVC, all on standardized features
- **Evaluation** — accuracy, full classification report, and confusion matrix per model
- **Feature importance** — from the Random Forest model
- **Model comparison table** — exported to `outputs/model_comparison.csv`

## Results

| Model | Accuracy |
|---|---|
| **Random Forest** | **0.850** |
| SVC | 0.785 |
| SGD Classifier | 0.753 |

**Top predictive features (Random Forest):** alcohol content, density, and volatile acidity — consistent with established wine-quality research, where alcohol content is one of the strongest single predictors of perceived quality.

**Conclusion:** Random Forest is the best-performing and most practical model for this task — it captures the non-linear relationships between chemical properties and quality without manual feature engineering, and its feature importances give an interpretable explanation that's useful for a winery's quality-control team, not just a black-box prediction.

## Files

```
DataAnalytics-L2-WineQualityPrediction/
├── WineQualityPrediction.ipynb   # main notebook
├── README.md
├── data/
│   ├── winequality-red.csv        # raw file (UCI ML Repository)
│   └── winequality-white.csv      # raw file (UCI ML Repository)
└── outputs/
    ├── model_comparison.csv
    ├── 01_feature_distributions.png
    ├── 02_correlation_heatmap.png
    ├── 03_confusion_matrices.png
    └── 04_feature_importance.png
```

## How to run

```bash
pip install -r ../requirements.txt
jupyter notebook WineQualityPrediction.ipynb
```

Then Cell → Run All.

## Demo video

(paste your LinkedIn post URL here)

#oasisinfobyte
