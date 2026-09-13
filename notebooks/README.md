# Notebooks

Numbered in the order they were developed. Each one finds the CSVs in `../data` on your machine, or under `/kaggle/input` if you run it on Kaggle.

| Notebook | What it covers | Models | Best RMSLE |
|---|---|---|---|
| [01_eda_and_baseline.ipynb](01_eda_and_baseline.ipynb) | First look at the data, basic features, course milestones 1–2 | Random Forest | 0.2282 |
| [02_feature_engineering.ipynb](02_feature_engineering.ipynb) | Time features, machine age, boosting models, milestones 1–3 | RF, XGBoost, LightGBM | — |
| [03_model_comparison_lightgbm.ipynb](03_model_comparison_lightgbm.ipynb) | Clean 3-fold CV comparison and error analysis | Ridge, RF, XGBoost, LightGBM | **0.1931** (LightGBM) |
| [04_milestones_and_cv.ipynb](04_milestones_and_cv.ipynb) | Same CV setup on full data, plus milestones 1–3 | Ridge, RF, XGBoost, LightGBM | 0.1974 (XGBoost) |
| [05_classical_models.ipynb](05_classical_models.ipynb) | sklearn-only models and milestones 1–4 | Ridge, RF, Gradient Boosting | 0.4485 |
| [06_end_to_end_pipeline.ipynb](06_end_to_end_pipeline.ipynb) | Full write-up: EDA → features → models → submission | Dummy, Ridge, RF, XGBoost | 0.2063 |
| [07_xgboost_and_milestones.ipynb](07_xgboost_and_milestones.ipynb) | Later XGBoost run with milestones 1–4 | Ridge, RF, XGBoost | 0.2044 |

If you only want to read one notebook, start with **06** for the narrative or **03** for the best scores.
