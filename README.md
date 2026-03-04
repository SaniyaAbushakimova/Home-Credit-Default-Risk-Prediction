Project completed on February 6, 2026.

# Home-Credit-Default-Risk-Prediction

## Project Overview

This project aims to predict loan default risk for applicants of Home Credit Bank. The task is a binary classification problem where the goal is to determine whether a client will experience payment difficulties.

The dataset contains multiple relational tables describing applicants' financial histories, including previous loans, credit bureau records, and installment payments. These tables were merged into a single applicant-level dataset through **extensive feature engineering and aggregation**.

The final dataset includes 386 engineered features describing applicants' credit behavior, financial history, and demographic attributes.

Two modeling approaches were explored:
1. Logistic Regression (baseline model)
2. Gradient Boosting Models (XGBoost and LightGBM with Optuna hyperparameter tuning)

## Repository Contents

* `solution_notebook.ipynb` – Full pipeline including data preprocessing, feature engineering, model training, and evaluation
* `presentation_report.pdf` – Detailed report describing dataset structure, feature engineering process, modeling methodology, and evaluation results
* `results_table.xlsx` – Summary of model performance metrics
* `test_predictions/` – Generated predictions for the test dataset

## Dataset
The dataset originates from the [Home Credit Default Risk Kaggle](https://www.kaggle.com/c/home-credit-default-risk) competition and contains several relational tables describing different aspects of client financial behavior.

Key tables include:
* `application_train.csv` – Main applicant data with demographic and financial information
* `bureau.csv` – Credit bureau records of previous loans
* `bureau_balance.csv` – Monthly balance history of bureau loans
* `previous_application.csv` – Historical loan applications
* `POS_CASH_balance.csv` – Point-of-sale loan balances
* `installments_payments.csv` – Installment payment history
* `credit_card_balance.csv` – Credit card usage history

## Exploratory Data Analysis (EDA)

EDA and preprocessing were performed in `solution_notebook.ipynb` and include:

* **Data Cleaning**
* **Handling missing values**
* **Correcting anomalous placeholder values** (e.g., DAYS_EMPLOYED = 365243)
* **Removing irrelevant or redundant variables**
* **Feature Engineering**
  * Significant feature engineering was required to combine the relational tables into a single dataset. Key steps included:
    1. Aggregating historical financial records at the applicant level.
    2. Creating statistical summaries such as mean, max/min, standard deviation, and count of previous loans.
    3. Generating behavioral features such as credit utilization, payment delay statistics, and loan application frequency.
    4. Creating ratio-based features describing financial stability (e.g., income-to-credit ratios).
  * After aggregation, all features were merged with the main application table using left joins on applicant ID.

The final dataset contained 386 engineered features and 356,249 applicants.

## Model Implementation & Performance

Two modeling approaches were evaluated.

1. **Logistic Regression (Baseline)**
* Logistic Regression was used as a baseline model to establish a benchmark for predictive performance.
* Features were standardized before training.
* ROC-AUC: 0.77133

2. **Gradient Boosting Models**
* Two tree-based ensemble models were trained: XGBoost, LightGBM
* Hyperparameters were optimized using Optuna, an automated hyperparameter search framework.
* Feature importance scores from tree models were used to remove the lowest 30% of features, reducing the feature space from 386 to 272 variables.
* ROC-AUC (XGBoost): 0.79083
* ROC-AUC (LightGBM): 0.78934

## Key Takeaways
* Extensive feature engineering from relational datasets can substantially improve predictive performance.
* Gradient boosting models outperform linear models for structured financial datasets.
* Handling class imbalance and optimizing for recall is critical for credit risk applications.
* Aggregating historical financial behavior provides strong predictive signals for default risk.
