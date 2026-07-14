# Hyperparameter Study Project

This project performs hyperparameter tuning and sensitivity analysis on several classification models using the datasets included in the repository. The objective is to evaluate model behaviour (Decision Tree, KNN, Logistic Regression, SVM) across hyperparameter sets and report sensitivity/variance of performance metrics.

## Project structure

```
hyperparameter_study
├── src
│   ├── main.py                     # Entry point that orchestrates experiments
│   ├── preprocessing.py            # Data loading & preprocessing helpers
│   ├── sensitivity_analysis.py     # Functions to run experiments and compute metrics
│   └── models                       # Model wrappers & training utilities
│       ├── decision_tree.py
│       ├── knn.py
│       ├── logistic_regression.py
│       └── svm.py
├── data                             # Datasets used for experiments
│   ├── diabetes_binary.csv
│   ├── mushrooms.csv
│   ├── student_dropout_success.csv
│   ├── credit_card.csv
    └── abalone.csv
├── hyperparameters                   # JSON files defining hyperparameter grids/sets
│   ├── decision_tree_params.json
│   ├── knn_params.json
│   ├── logistic_regression_params.json
│   └── svm_params.json
├── results                           # Output from experiments
│   ├── sensitivity_metrics.csv       # Per-run metrics (F1, AUC, accuracy, etc.)
│   ├── variance_summary.csv          # Aggregated variance / sensitivity summaries
│   └── summary_report.txt            # Human-readable summary of findings
├── package.json                      # Optional project metadata (if present)
└── README.md                         # This file
```

Notes on data
- The `data/` folder contains the actual CSV files used for experiments. Confirm column names and target column in `src/preprocessing.py` before running.
- Datasets vary in size and feature types; preprocessing currently handles missing values, basic encoding, and scaling where required.

Hyperparameter configuration
- Hyperparameter sets for each model live in `hyperparameters/*.json`. Each JSON should define the grid or list of values the study should evaluate. Example expected keys (per model):
  - Decision Tree: max_depth, min_samples_split, criterion, etc.
  - KNN: n_neighbors, weights, metric, etc.
  - Logistic Regression: penalty, C (regularization), solver, max_iter, etc.
  - SVM: C, kernel, gamma, degree (for poly), etc.
- The format used by `src/sensitivity_analysis.py` reads these JSONs and runs combinations described there. Adjust JSONs to extend or restrict the search space.

Setup instructions

1. Clone the repository and change to the project directory.
2. Ensure you have Python 3.8+ and required packages installed. If a requirements file is added, run:
   ```
   pip install -r requirements.txt
   ```
   If not present, install typical packages used: pandas, numpy, scikit-learn.
3. Place any additional datasets in the `data/` directory.
4. Update hyperparameter JSONs in `hyperparameters/` as needed.
5. Run the main experiment:
   ```
   python src/main.py
   ```

Usage guidelines
- src/main.py: entry point — configures experiments, loads hyperparameter sets, iterates datasets and models, and writes results to `results/`.
- src/preprocessing.py: data checks, encoding, scaling, train/test split logic.
- src/sensitivity_analysis.py: runs model training and evaluation for hyperparameter sets; computes metrics such as F1, AUC, accuracy, and variance across runs.
- src/models/*: individual model wrappers that accept hyperparameter dicts and expose fit/predict interfaces.

Results and outputs
- Per-run metrics are saved to `results/sensitivity_metrics.csv`.
- Aggregated variance and sensitivity summaries are in `results/variance_summary.csv`.
- A plain text summary is available at `results/summary_report.txt`.

Contributing
- Improve preprocessing for specific datasets by editing `src/preprocessing.py`.
- Add or refine hyperparameter search strategies in `src/sensitivity_analysis.py`.
- Add new model wrappers in `src/models/` following the existing interface.

License
- This project is provided under the MIT License