# Heavy Equipment Selling Price Prediction

Predict the selling price of heavy industrial machinery from operational, geographic, and technical features using classical machine learning models.

| | |
|---|---|
| Problem | Regression |
| Target | `TargetValue` (USD) |
| Metric | RMSLE (lower is better) |
| Pass cutoff | Leaderboard score **< 0.20** |
| Train / test | 138,701 / 15,000 rows |

## Why RMSLE

Sale prices range from about **$7,500 to $142,000**. RMSLE scores relative error on the log scale, so a $5,000 miss matters more on a cheap machine than on an expensive one.

## Approach

1. **Explore** the mix of numeric, categorical, and high-cardinality spec columns, including missingness and outliers (for example a manufacture year of 1001).
2. **Engineer features** that describe condition and time: `MachineAge`, `LogHours`, transaction year/month, and mean-price encodings for high-cardinality categories.
3. **Train on log(price)** so the objective matches RMSLE, using sklearn pipelines to keep preprocessing leakage-free.
4. **Compare models** from simple baselines up to gradient boosting, then tune the best one and write `submission.csv`.

## Results

Validation / CV RMSLE from the notebooks (lower is better):

| Model | Best RMSLE | Notebook |
|---|---|---|
| Dummy regressor | 0.6707 | 06 |
| Ridge | 0.3194 | 04 |
| Random Forest | 0.2164 | 03 |
| XGBoost | 0.1943 | 03 |
| **LightGBM** | **0.1931** | **03** |

LightGBM is the strongest model in this repo. XGBoost is close behind and is the main model in the later end-to-end notebooks.

## Repository layout

```text
.
├── README.md
├── requirements.txt
├── data/
│   ├── README.md              # column descriptions
│   ├── train.csv
│   ├── test.csv
│   ├── metadata.csv
│   └── sample_submission.csv
└── notebooks/
    ├── 01_eda_and_baseline.ipynb
    ├── 02_feature_engineering.ipynb
    ├── 03_model_comparison_lightgbm.ipynb
    ├── 04_milestones_and_cv.ipynb
    ├── 05_classical_models.ipynb
    ├── 06_end_to_end_pipeline.ipynb
    └── 07_xgboost_and_milestones.ipynb
```

Notebooks are numbered in the order they were built. **03** is the strongest CV comparison. **06** is the most documented walkthrough. **07** is the later XGBoost run plus course milestone questions.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Then open a notebook from `notebooks/`. Each notebook looks for CSVs in `../data` locally, and falls back to the Kaggle input path if you run it there.

Training on the full 138k rows can take a while. Some notebooks have a `USE_FULL_DATA` flag so you can run a smaller sample first.

## What the data looks like

Each row is one finalized equipment transaction. Useful signals include machine age and hours, utilization, region, and equipment class. Many `col*` technical fields are sparse and are dropped or imputed during preprocessing. IDs (`TransactionID`, `AssetID`, `ProductConfigID`) are not used as predictors.

See [data/README.md](data/README.md) for the full column list.

## Main findings

- Newer machines and lower utilization tend to sell for more.
- Equipment category and region have a strong effect on price.
- The target is right-skewed; training on log(price) helps.
- Tree-based models beat linear baselines; LightGBM and XGBoost are the ones that clear the 0.20 RMSLE bar in cross-validation.
