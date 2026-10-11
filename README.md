# Patterns in Encrypted HTTPS Traffic

Machine learning analysis of encrypted HTTPS/TCP traffic using Tstat flow statistics. The notebook explores traffic patterns, classifies domain-name labels, groups domains by traffic behavior, and estimates server-to-client byte volume and round-trip time (RTT).

The analysis uses numerical flow measurements rather than decrypted application content.

## Repository Contents

- [`ML4N_project.ipynb`](ML4N_project.ipynb): Python notebook containing preprocessing, exploratory analysis, model training, evaluation, and visualizations.
- [`ML4N_project.pdf`](ML4N_project.pdf): report describing the methods and results.

## Analysis Workflow

1. **Data exploration and preprocessing:** data-quality checks, flow statistics, aggregation by client IP and domain, logarithmic transformations, removal of constant and correlated features, and PCA/t-SNE visualizations.
2. **Classification:** Decision Tree, Random Forest, and K-Nearest Neighbors, with five-fold cross-validation and sequential hyperparameter tuning through validation curves. Evaluation includes accuracy, weighted F1, per-class reports, confusion matrices, and one-vs-rest ROC curves.
3. **Clustering:** domain-level feature aggregation, standardization, PCA, K-Means, DBSCAN, and hierarchical clustering with Ward linkage.
4. **Regression:** Lasso, Decision Tree, and Random Forest for `_s_bytes_all` and `_s_rtt_avg`, with three-fold cross-validation and grid search. Evaluation includes MAE, RMSE, and R².

## Data

Execution requires two CSV files in the same directory as the notebook:

```text
https_training.csv
https_test.csv
```

These files are not included in the repository. They must use the Tstat feature schema expected by the notebook, including numerical columns prefixed with `_` and the metadata columns `c_ip`, `time`, and `label`.

The saved analysis uses 147,863 training flows and 114,580 test flows, with 123 columns and 26 domain-name labels. The notebook preserves the supplied training/test split and excludes `c_ip`, `time`, and `label` from predictive feature matrices.

## Requirements

- Python 3
- JupyterLab
- NumPy
- pandas
- SciPy
- scikit-learn
- Matplotlib
- seaborn
- IPython

## Running the Notebook

From the repository directory, install the dependencies:

```bash
python -m pip install jupyterlab numpy pandas scipy scikit-learn matplotlib seaborn ipython
```

Place the two CSV files beside the notebook, then start JupyterLab:

```bash
python -m jupyter lab
```

Open `ML4N_project.ipynb` and run the cells in order. Full execution includes cross-validation, hyperparameter searches, and t-SNE, which can require substantial time and memory. Some cells save figures as PNG files in the working directory.

The notebook contains saved outputs that can be inspected without rerunning the analysis. The PDF provides a separate presentation of the results.
