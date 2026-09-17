# USFG: Uncertainty-Stratified Faithfulness Gap

Code for a study testing whether a model's uncertainty (epistemic/aleatoric) is
actually linked to the faithfulness of its post-hoc explanations (SHAP/LIME) in credit
scoring — and, at the same time, testing the measuring instrument used to answer that
question, on three public credit datasets (Home Credit Default Risk, Taiwan Credit
Default, Give Me Some Credit).

Main finding: most of the apparent "higher uncertainty → less faithful explanation"
association is attributable to a shared confounder, the predicted probability position,
rather than to an independent effect of uncertainty on explanation quality.

## Pipeline structure

Eight computational notebooks, run in sequence:

| Notebook | Role | Run environment |
|---|---|---|
| `NB1_preprocess.ipynb` | Preprocess the three datasets, build splits | Kaggle |
| `NB2_train_M1_xgboost.ipynb` | Train the XGBoost benchmark (M1) | Kaggle |
| `NB3_train_basins.ipynb` | Train the pool of 50 neural network basins | Kaggle (GPU) |
| `NB4_budget_grid.ipynb` | M x T = 50 budget grid, build architectures M2-M5 | Kaggle |
| `NB5_compute_xai.ipynb` | Generate SHAP/LIME explanations, measure Comprehensiveness/Sufficiency | Kaggle (GPU) |
| `NB6_table.ipynb` | Aggregate result tables from NB1-NB5 outputs | Local |
| `NB7_visualize.ipynb` | Build every figure in the report | Local |
| `NB8_validate_usfg.ipynb` | Construct-validate the USFG-c metric on simulated data | Local |

`NB1`-`NB5` must run on Kaggle (they read data through `/kaggle/input/...`, and `NB3`
and `NB5` need a GPU). `NB6`-`NB8` run on a local machine, reading intermediate results
through the relative paths `../kaggle-output/` and `../result/`.

## Reproducing the results

1. On Kaggle, create a new notebook for each of `NB1`-`NB5` and attach the three
   datasets:
   - [Home Credit Default Risk](https://www.kaggle.com/competitions/home-credit-default-risk)
   - [Taiwan Credit Default (UCI, via Kaggle)](https://www.kaggle.com/datasets/uciml/default-of-credit-card-clients-dataset)
   - [Give Me Some Credit](https://www.kaggle.com/competitions/GiveMeSomeCredit)
2. Run `NB1` -> `NB2` -> `NB3` -> `NB4` -> `NB5` in order, download each `/kaggle/working/`
   output, and place it under `kaggle-output/` following the structure described in
   `kaggle-output/README.md`.
3. Run `NB6`, `NB7`, `NB8` from the `notebooks/` directory (the relative paths
   `../result/` and `../kaggle-output/` assume the notebook is running from that exact
   location).

The root random seed is fixed at 42, and every derived seed is generated deterministically
from it, with one exception: the explanation reproducibility measurement relies on the
explanation tool's own internal random number generator (SHAP/LIME), so the stability
table alone is not reproducible digit for digit across runs.

## `result/`

Pre-aggregated tables and figures (the output of `NB6`-`NB8`), small enough and free of
any personally identifying information, so they are committed directly to the repo for
readers to inspect or reuse without having to rerun the full pipeline.

## License

The source code in this repository is released under the MIT License (see `LICENSE`).
That license applies to the *code*; the three credit datasets used in the study are
subject to their own usage terms on Kaggle, are not covered by the MIT license above,
and are not redistributed in this repository.

## Citation

If you reuse the code or results in this repository, please cite the corresponding
research report (BIT GENESIS RESEARCH AWARDS 2026, University of Economics Ho Chi Minh
City).
