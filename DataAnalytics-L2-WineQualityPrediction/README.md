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

| Model | Accuracy | Macro F1 |
|---|---|---|
| **Random Forest** | **0.850** | **0.581** |
| SVC | 0.785 | 0.408 |
| SGD Classifier | 0.753 | 0.321 |
| *Baseline (always predict "medium")* | *0.765* | *—* |

**Top predictive features (Random Forest):** alcohol content, density, and volatile acidity — consistent with established wine-quality research, where alcohol content is one of the strongest single predictors of perceived quality.

**Accuracy alone is misleading on this dataset.** The "low" quality class is only ~3.8% of the test set, and a trivial model that always predicts "medium" already scores 76.5% accuracy — meaning **SGD Classifier (75.3%) actually performs *worse* than doing nothing**, despite its accuracy number looking reasonable in isolation. Per-class evaluation (in the notebook's `classification_report` output) shows why: both SGD and SVC get **0% recall on the "low" class** — they never correctly identify a single low-quality wine — and even Random Forest, the best of the three, only recalls about 10% of them. Macro-F1 (which weighs all classes equally instead of letting the large "medium" class dominate) makes this gap far more visible than accuracy does.

**Conclusion:** Random Forest is the strongest of the three models on both accuracy and macro-F1, and its feature importances give an interpretable, practically useful explanation for a winery's quality-control team. However, **it is not yet reliable for catching low-quality wine** — arguably the more business-critical use case. None of the three models applied class-imbalance handling (e.g. `class_weight="balanced"`, SMOTE oversampling, or collecting more low/high-quality samples), so these results should be read as a baseline to build on, not a finished, deployment-ready solution.

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
