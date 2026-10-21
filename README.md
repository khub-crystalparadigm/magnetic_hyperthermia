# Hyperthermia: Machine Learning for SAR Prediction

A machine-learning research project for predicting the **specific
absorption rate (SAR, W/g)** of magnetic nanoparticles for magnetic
hyperthermia. The repository contains model-specific Jupyter notebooks,
evaluation plots, feature-importance analyses, candidate-optimization
outputs, retrospective analysis, and similarity checks.

## Project objectives

-   Predict nanoparticle SAR from available material and experimental
    features.
-   Compare multiple regression algorithms using a consistent modelling
    workflow.
-   Evaluate predictions with actual-versus-predicted plots and
    regression metrics.
-   Interpret model behaviour using SHAP feature-importance analyses.
-   Explore candidate compositions and optimization behaviour using
    TabPFN-based workflows.
-   Compare proposed candidates with existing records through
    nearest-neighbour similarity analysis.
-   Perform retrospective analysis of high-performing records.

## Repository architecture

``` text
Hyperthermia/
├── Models/
│   ├── CatBoost/
│   │   ├── Hyperthermia_CB.ipynb
│   │   ├── actual_vs_predicted_PI.png
│   │   ├── dopant_sar_scatter.png
│   │   ├── pdp_2d_all_pairs_subplot.png
│   │   ├── residuals_distribution.png
│   │   ├── residuals_vs_dopants.png
│   │   ├── residual_distribution.png
│   │   └── shap_summary.png
│   ├── Decision Trees/
│   │   ├── hyperthermia-dt.ipynb
│   │   ├── dt_actual_vs_predicted.png
│   │   └── dt_shap_summary.png
│   ├── Gaussian Process Regression/
│   │   ├── hyperthermia-gpr.ipynb
│   │   ├── gpr_actual_vs_predicted.png
│   │   └── gpr_shap_summary.png
│   ├── K - Nearest Neighbors/
│   │   ├── hyperthermia-knn.ipynb
│   │   ├── knn_actual_vs_predicted.png
│   │   └── knn_shap_summary.png
│   ├── LightGBM/
│   │   ├── hyperthermia-gbm.ipynb
│   │   ├── lgb_actual_vs_predicted.png
│   │   └── lgb_shap_summary.png
│   ├── Linear Regression/
│   │   ├── hyperthermia-linear.ipynb
│   │   ├── lr_actual_vs_predicted.png
│   │   └── lr_shap_summary.png
│   ├── Multi Layer Perceptron/
│   │   ├── hyperthermia-mlp.ipynb
│   │   ├── mlp_actual_vs_predicted.png
│   │   └── mlp_shap_summary.png
│   ├── Random Forest/
│   │   ├── hyperthermia-rfr.ipynb
│   │   ├── rf_actual_vs_predicted.png
│   │   └── rf_shap_summary.png
│   ├── Ridge Regression/
│   │   ├── hyperthermia-ridge.ipynb
│   │   ├── ridge_actual_vs_predicted.png
│   │   └── ridge_shap_summary.png
│   ├── TabPFN/
│   │   ├── Hyperthermia_TabPFN.ipynb
│   │   ├── actual_vs_predicted_PI.png
│   │   ├── Distribution.png
│   │   ├── optimaization_convergence_plot.png
│   │   ├── pdp_2d_all_pairs_subplot.png
│   │   ├── Random_seed.png
│   │   ├── Residuals.png
│   │   ├── residuals_vs_dopants.png
│   │   ├── ShapSummary.png
│   │   └── top_candidates_tabpfn (1).xlsx
│   └── XGBoost/
│       ├── hyperthermia-xgb.ipynb
│       ├── xgb_actual_vs_predicted.png
│       └── xgb_shap_summary.png
├── Retrospective Analysis/
│   ├── hyperthermia-retro.ipynb
│   ├── optimaization_convergence_plot_retro.png
│   ├── Random_seed_retro.png
│   └── top_candidates_tabpfn_retro.xlsx
└── Similarity Check/
    ├── Similarity.ipynb
    ├── Similarity_plot.png
    ├── SIMILARITY_RETRO.xlsx
    └── top_existing_performers.xlsx
```

> **Data file note:** The notebooks expect an input workbook named
> `Final.xlsx`, but it is not present in the supplied ZIP archive.
> Obtain the authorized dataset and place it where the relevant notebook
> expects it, or update the notebook's data-loading path before running.

## Folder guide

### `Models/`

Contains the model-specific notebooks and generated diagnostic figures.

  --------------------------------------------------------------------------------------
  Model folder                     Notebook                      Purpose
  -------------------------------- ----------------------------- -----------------------
  `CatBoost/`                      `Hyperthermia_CB.ipynb`       CatBoost regression and
                                                                 model diagnostics

  `Decision Trees/`                `hyperthermia-dt.ipynb`       Decision-tree
                                                                 regression

  `Gaussian Process Regression/`   `hyperthermia-gpr.ipynb`      Gaussian-process
                                                                 regression

  `K - Nearest Neighbors/`         `hyperthermia-knn.ipynb`      K-nearest-neighbour
                                                                 regression

  `LightGBM/`                      `hyperthermia-gbm.ipynb`      LightGBM regression

  `Linear Regression/`             `hyperthermia-linear.ipynb`   Linear regression
                                                                 baseline

  `Multi Layer Perceptron/`        `hyperthermia-mlp.ipynb`      Neural-network
                                                                 regression with an MLP

  `Random Forest/`                 `hyperthermia-rfr.ipynb`      Random-forest
                                                                 regression

  `Ridge Regression/`              `hyperthermia-ridge.ipynb`    L2-regularized linear
                                                                 regression

  `TabPFN/`                        `Hyperthermia_TabPFN.ipynb`   TabPFN modelling,
                                                                 candidate exploration,
                                                                 and
                                                                 optimization-related
                                                                 analysis

  `XGBoost/`                       `hyperthermia-xgb.ipynb`      Gradient-boosted-tree
                                                                 regression with XGBoost
  --------------------------------------------------------------------------------------

The folders also contain plots for model evaluation and interpretation.
Depending on the model, these include actual-versus-predicted SAR, SHAP
summaries, residual distributions, residuals against dopant variables,
partial-dependence plots, and optimization diagnostics.

### `Retrospective Analysis/`

Contains a retrospective modelling and candidate-analysis workflow. Its
outputs include optimization-convergence and random-seed plots, plus an
Excel workbook of retrospective TabPFN candidates.

### `Similarity Check/`

Contains a nearest-neighbour similarity workflow and related outputs.
The notebook compares candidate records against records from the
existing dataset; the folder includes a similarity visualization and
Excel workbooks for similarity results and existing high-performing
records.

## Modelling workflow

The notebooks implement a machine-learning workflow that generally
includes:

1.  **Data loading and cleaning** --- load the Excel dataset, clean
    column names, and remove non-predictive identifiers where
    appropriate.
2.  **Exploratory data analysis** --- inspect data types, missing
    values, target distributions, and feature correlations.
3.  **Data splitting** --- create training, validation, and test
    subsets.
4.  **Preprocessing** --- handle missing values, encode categorical
    features, engineer features, and scale inputs.
5.  **Target transformation** --- notebooks using the shared workflow
    apply `log1p` to SAR and scale the transformed target; predictions
    are converted back to SAR units for interpretation.
6.  **Model fitting and tuning** --- train the relevant estimator; some
    workflows use Optuna for hyperparameter optimization.
7.  **Evaluation** --- compare predicted and observed SAR and calculate
    regression metrics such as (R\^2) and RMSE.
8.  **Interpretability and diagnostics** --- use SHAP and model-specific
    plots to inspect feature effects and prediction errors.
9.  **Candidate analysis** --- the TabPFN and retrospective workflows
    include candidate-generation or optimization-related analysis.

Implementation details can differ between notebooks. Check the relevant
notebook before assuming that every model uses exactly the same
preprocessing, tuning strategy, or evaluation protocol.

## Outputs and how to read them

-   **Actual vs. predicted plots:** points closer to the identity line
    indicate predictions closer to measured values.
-   **SHAP summary plots:** show how input features contribute to model
    predictions; interpretation depends on the model and data.
-   **Residual plots/distributions:** help reveal systematic errors,
    spread, and potential outliers.
-   **PDP / 2D PDP plots:** show modelled relationships between selected
    features and predicted SAR.
-   **Optimization convergence plots:** show how the objective evolves
    during an optimization procedure.
-   **Candidate Excel workbooks:** contain generated or shortlisted
    candidates; inspect the workbook columns and notebook logic for the
    precise meaning of each field.
-   **Similarity outputs:** help assess how closely proposed candidates
    resemble existing dataset records.

Model predictions and optimization outputs are computational estimates,
not experimental confirmation. Candidate materials should be
independently validated before drawing scientific or application-level
conclusions.

## Requirements

The notebooks use Python and common data-science libraries. Depending on
the notebook, dependencies include:

-   `numpy`
-   `pandas`
-   `matplotlib`
-   `seaborn`
-   `scikit-learn`
-   `scipy`
-   `openpyxl`
-   `shap`
-   `xgboost`
-   `lightgbm`
-   `catboost`
-   `optuna`
-   `tabpfn`
-   `joblib`

The exact environment is notebook-dependent. Some notebooks install
packages within notebook cells, but a dedicated environment is
recommended for reproducibility. TabPFN may require additional setup or
an API token depending on the version, dataset size, and service
requirements.

## Getting started

### 1. Clone the repository

``` bash
git clone <YOUR_REPOSITORY_URL>
cd Hyperthermia
```

Replace `<YOUR_REPOSITORY_URL>` with the URL of your Git repository.

### 2. Create a Python environment

Using `venv`:

``` bash
python -m venv .venv
```

Activate it on Linux/macOS:

``` bash
source .venv/bin/activate
```

On Windows PowerShell:

``` powershell
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

Install the dependencies required by the notebook you plan to run. A
starting point is:

``` bash
python -m pip install --upgrade pip
python -m pip install numpy pandas matplotlib seaborn scikit-learn scipy openpyxl shap xgboost lightgbm catboost optuna joblib
```

Install and configure `tabpfn` separately if running the TabPFN or
related retrospective workflow:

``` bash
python -m pip install tabpfn
```

Package versions and TabPFN setup requirements may change; use versions
compatible with the notebook code and your Python environment.

### 4. Add the dataset

Place the authorized `Final.xlsx` workbook at the path used by the
notebook. Some notebooks refer to a Kaggle input path, while others load
`Final.xlsx` from the current working directory. Update those paths as
needed. The dataset is not included in the supplied archive.

### 5. Run a notebook

Launch Jupyter:

``` bash
python -m pip install jupyter
jupyter lab
```

Open the notebook for the model or analysis you want to run. Execute the
cells in order, verify that the data path and dependencies are correct,
and review the evaluation metrics and plots produced by that notebook.

## Reproducibility notes

-   Record Python and package versions when generating results.
-   Keep dataset versions and train/validation/test splits documented.
-   Fit preprocessing transformations on training data only to avoid
    data leakage.
-   Keep the test set separate from model selection and hyperparameter
    tuning.
-   Record random seeds and optimization settings when comparing runs.
-   Treat saved figures and Excel files as outputs from particular runs;
    regenerate them if the dataset or code changes.
-   Do not commit private credentials, API tokens, or restricted
    datasets to a public repository.

## Repository status and scope

This README describes the contents of the supplied archive. The archive
contains notebooks, figures, and selected Excel analysis outputs; it
does not include `Final.xlsx`, a root-level dependency lockfile, or a
single unified training script. Exact results therefore depend on
obtaining the dataset and recreating the notebook environment.

## License and data availability

Add the license that applies to your code and confirm the data's
redistribution terms before publishing the repository. Do not imply that
the dataset is openly licensed unless you have verified its license and
provenance.

------------------------------------------------------------------------

*For research use. Validate model performance and candidate predictions
against appropriate experimental evidence before using them to guide
material selection or application decisions.*
