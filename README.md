# TabPFN API-Based Classification Model

This project implements a binary classification model for material properties using the **TabPFN Cloud API**. The pipeline is documented and executable via the provided Jupyter Notebook.

## Overview

The model uses the `TabPFNClassifier` to perform binary classification. TabPFN is a prior-data fitted network that provides fast and accurate predictions for tabular data. By using the cloud API, the model offloads heavy computation to the cloud.

### Key Features
- **Data Preprocessing**: Automatically handles feature selection (excluding identifiers like `mv_id` and `Formula`) and splits the dataset into 60% training, 20% validation, and 20% testing sets.
- **Model Training**: Leverages the TabPFN Cloud API out of the box via a provided API token.
- **Evaluation**: Computes comprehensive classification and regression error metrics (Accuracy, Precision, Recall, F1-Score, ROC-AUC, MSE, RMSE, MAE, Hamming Loss).
- **Outputs**: Saves predictions and evaluation metrics to CSV files and generates visual performance reports (Confusion Matrix, Metrics Bar Chart).

## Prerequisites

To run the notebook, you need Python and the following packages installed:
- `tabpfn`
- `pandas`
- `numpy`
- `scikit-learn`
- `matplotlib`
- `seaborn`

You can install them by running:
```bash
pip install tabpfn pandas numpy scikit-learn matplotlib seaborn
```

## Setup & Usage

1. **Provide the Dataset**: Ensure the dataset file `training_dataset (1).csv` is in the same directory as the notebook.
2. **API Token**: The notebook is pre-configured to use a specific TabPFN API token. If you need to use a different token, update the `TABPFN_TOKEN` environment variable in Step 3 of the notebook.
3. **Run the Notebook**: Execute `tabpfn_api_classification.ipynb` cell by cell. 

## Project Structure

- `tabpfn_api_classification.ipynb`: The main Jupyter Notebook containing the end-to-end classification pipeline.
- `training_dataset (1).csv`: The input training dataset (needs to be available in the directory).

### Generated Artifacts
Running the notebook will output the following files:
- `tabpfn_api_predictions.csv`: Contains the actual label, predicted label, and confidence (probability) for the test set.
- `tabpfn_api_metrics.csv`: Contains the final test set metrics (Accuracy, Precision, Recall, F1-Score, ROC-AUC).

## Evaluation Metrics Output
The notebook provides a detailed summary of the model's performance, including:
- Confusion Matrix Heatmap
- Metrics Comparison Chart
- Additional error analysis (90th percentile error interval, errors per class)
