# kaggle-output/

This directory is a placeholder for the intermediate results produced by `NB1`-`NB5`
when run on Kaggle (trained models, SHAP/LIME explanations, per-applicant uncertainty
tables, ...). The contents are not committed to the repository because of their size
and because the three underlying credit datasets may only be used within the scope of
their respective Kaggle competitions, not redistributed elsewhere.

To reproduce, run `NB1`-`NB5` on Kaggle, download the results, and recreate the
following structure:

```
kaggle-output/
  NB1-outputs/        # NB1_preprocess.ipynb
  NB2-outputs/        # NB2_train_M1_xgboost.ipynb
  NB3-outputs/
    NB3-result/        # NB3_train_basins.ipynb
  NB4-outputs/        # NB4_budget_grid.ipynb
  NB5-outputs/        # NB5_compute_xai.ipynb
```

See the full instructions in the `README.md` at the repository root.
