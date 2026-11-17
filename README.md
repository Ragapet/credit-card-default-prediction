# Credit Card Default Prediction

This project predicts whether a credit card client will default in the next month. It compares logistic regression and gradient boosting, and explores how the costs of missed defaults and false alarms affect the decision threshold.

## Data

The [Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) dataset from UCI contains 30,000 clients from Taiwan, with demographic data, credit limits and six months of payment history.
Dataset by I-Cheng Yeh (2009). Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Approach

* Explore the data and create features from bills, payments and repayment delays.
* Use L1 regularization for feature selection in logistic regression.
* Compare models using 5-fold stratified cross-validation repeated 5 times.
* Evaluate the final models on a separate 20% test set.
* Select thresholds using validation predictions and assumed error costs.
* Estimate uncertainty with 10,000 bootstrap samples of the test set.

## Results

Gradient boosting was selected based on cross-validation. The final test results were:

|Model|ROC AUC|Average precision|Brier score|
|-|-:|-:|-:|
|Logistic regression (L1)|0.7694|0.5307|0.1382|
|Gradient boosting|0.7828|0.5584|0.1346|

Higher ROC AUC and average precision are better; lower Brier score is better.

Actual error costs are unknown, so there is no single recommended threshold. The cost performance of the selected thresholds was not evaluated on the test set.

## How to run

1. Install pandas, NumPy, scikit-learn, SciPy, Matplotlib, Seaborn, xlrd and Jupyter Notebook.
2. Place `default of credit card clients.xls` in `Data/` and create `Results/` if needed.
3. Open [Credit Default.ipynb](Jupyter/Credit%20Default.ipynb) with `Jupyter/` as the working directory and run all cells.

`LOAD_TRAIN_RESULTS = True` reuses saved training results when available. Set it to `False` to rerun training.

