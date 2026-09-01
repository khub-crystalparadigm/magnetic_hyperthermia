# SAR Prediction with TabPFN — Nanoparticle Dataset

A full ML workflow that predicts Specific Absorption Rate (SAR, W/g) for magnetic
nanoparticles from a tabular property dataset, using [TabPFN](https://tabpfn.com)
as the regressor, and then runs an inverse-design search (differential evolution)
to propose high-SAR nanoparticle compositions.

## Pipeline

The notebook `tabpfn_workflow.ipynb` follows one linear pipeline, top to bottom:

1. **Setup** — installs and imports.
2. **Data loading** — reads the raw Excel file, strips invisible Unicode from
   column names, drops non-feature/identifier columns.
3. **Exploratory data analysis** — shape, dtypes, missingness, categorical
   cardinality, correlation with the target.
4. **Train / val / test split** (80 / 10 / 10) — the test set is locked away
   before any preprocessing.
5. **Preprocessing** — presence-flag features, ordinal-encoding of categoricals,
   `MissForest` imputation for numeric NaNs. All transformers are fit on
   `x_train` only.
6. **Feature engineering** — `QuantileTransformer` scaling of inputs, `log1p` +
   `MinMaxScaler` on the target.
7. **Model training** — fits a `TabPFNRegressor` on the scaled training data.
8. **Evaluation** — R² / RMSE on val and test, actual-vs-predicted plots,
   residual analysis, SHAP feature importance, partial dependence plots,
   physical-scale sanity checks.
9. **Inverse design** — a differential-evolution search over structural and
   dopant-composition variables (with LRT-safety and dopant-sum constraints)
   proposes candidate high-SAR compositions, saved to
   `top_candidates_tabpfn.xlsx`.

No modelling logic, transformer order, or scoring math was changed while
preparing this repo — the edits below are purely housekeeping for a public/shared
git history.

## What changed for git

| Change | Cell(s) | Why |
|---|---|---|
| Removed the hardcoded TabPFN API token | Model training cell | A real secret (`tabpfn_sk_...`) was committed in plain text. It now reads `TABPFN_TOKEN` from the environment, falling back to an interactive `getpass()` prompt so nothing sensitive touches disk or git history. **This exposed token should be revoked/rotated at tabpfn.com regardless**, since it was in a file you uploaded. |
| Guarded the Colab download cell | Last cell | `from google.colab import files` only exists inside Google Colab; it would `ImportError` on any other machine or in CI. Wrapped in `try/except` so it's a no-op elsewhere (the file is already saved to disk by the previous cell either way). |
| Removed two fully commented-out cells | Old cells 9 and 39 (target-distribution plot, debug print block) | Both were 100% comments — no executable code, so removing them changes nothing about the pipeline's behavior. Keeping them would just be clutter in a shared repo; if you want that scratch analysis back, it's preserved in the notebook's git history after your first commit. |
| Added `requirements.txt`, `.gitignore`, this `README.md` | — | Standard repo hygiene: pinned-free dependency list, keep data/secrets/generated plots out of version control. |

### Blocks kept as-is (safe to include)
Every numbered pipeline section (1–9 above) — data loading, EDA, split,
preprocessing, feature engineering, training, evaluation, and the inverse-design
search — is unmodified logic and fine to commit and share.

### Blocks you should double-check before pushing
- **Cell 2** (`%pip install ...`) — kept as a convenience "run once" cell. If you'd
  rather standardize on `requirements.txt`, replace it with
  `!pip install -r requirements.txt`.
- **Data loading cell** (`pd.read_excel("Final.xlsx")`) — the raw dataset file
  itself is **not** included and is excluded via `.gitignore` (`Final.xlsx`,
  `*.xlsx`). Keep proprietary/unpublished experimental data out of git; store it
  separately (data storage, DVC, etc.) and document the expected path here.
- **Rewritten `y_test`/`x_test` in place mid-notebook** (evaluation section) —
  functionally fine since it runs top-to-bottom once, but be aware later cells
  depend on the *inverse-transformed* `y_test`, not the scaled one. Not changed,
  just flagging for anyone editing cell order later.
- **Duplicate constant definitions** — `FREE_DOPANT_COLS`, `FE_COL`,
  `FE_BOUNDS`, `DOPANT_SUM_TARGET`, `FREE_DOPANT_IDXS` are each defined twice in
  the inverse-design section (harmless — the second definition just re-runs
  identically — but worth consolidating if you refactor into `.py` modules
  later).

## Setup

```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

TabPFN needs an API token for datasets above its default size limit:

```bash
export TABPFN_TOKEN=your_token_here    # get one at https://tabpfn.com
```

If you don't set the environment variable, the notebook will prompt for the
token interactively (via `getpass`) when it reaches the training cell.

## Data

Place your dataset as `Final.xlsx` in the same directory as the notebook (or
change the path in the "Data Loading" cell). Expected target column:
`f_SAR_W_g`. See `FEATURE_NAMES` / `CAT_COLS` / `DROP_COLS` at the top of the
notebook for the exact schema the pipeline expects.

## Outputs

Running the notebook end-to-end produces (all git-ignored by default):
- Diagnostic plots (`*.png`): actual-vs-predicted, residuals, SHAP summary,
  partial dependence, LRT/dopant analyses.
- `top_candidates_tabpfn.xlsx` — top inverse-design candidates.
- `top50_high_SAR_predictions.csv`, `top50_high_SAR_summary.xlsx`,
  `top50_high_SAR_recipe.xlsx` — top-50 predicted-SAR summary and a
  recommended-range "recipe" table.

## Notes

- TabPFN Regressor is a prior-fitted transformer — it needs no hyperparameter
  search, but does need the environment variable
  `TABPFN_ALLOW_CPU_LARGE_DATASET=1` set for larger datasets on CPU (already
  handled in the notebook).
- The inverse-design search (`differential_evolution`) can take a while
  depending on `subset_sizes`, `max_subsets_per_size`, and
  `n_candidates_per_subset` — reduce these for a faster, coarser search.
