# Income Prediction — Model Validation & Bias Auditing

**Python · Data Analysis · Regression · Leakage Prevention · Model Evaluation · Fairness Auditing**

> **Portfolio case study:** A reproducible income-prediction experiment that compares linear regression strategies, prevents data leakage, and audits model errors across demographic groups.

[**View the analysis notebook**](./Actividad_4_Ingresos_Leakage_Sesgos.ipynb) · [**Explore my GitHub profile**](https://github.com/FrancoCurcho)

## Project Overview

Predicting income requires more than fitting a regression model. Data preparation, asymmetric targets, evaluation design, repeated profiles, and differences in performance across demographic groups can strongly affect conclusions.

This academic project compares standard linear regression with a log-transformed-target regression. It uses group-aware data splitting and cross-validation, evaluates the selected model on a reserved test set, and documents subgroup errors and model limitations.

**Goal:** Improve predictive performance on mean absolute error (MAE) without overstating what the model can reliably predict.

## Key Results

| Metric | Result |
| --- | ---: |
| Records / input features | 10,000 / 8 |
| Unique input profiles | 8,535 |
| Development / held-out test rows | 7,993 / 2,007 |
| Selected model | Linear regression with log-transformed target |
| Cross-validation MAE (selected model) | 29,483.3 units |
| Held-out test MAE | **29,309.6 units** |
| Held-out test RMSE | 63,827.1 units |
| Held-out test R² | 0.181 |
| Median-baseline test MAE | 35,940.4 units |
| Test MAE improvement over baseline | **18.45%** |
| Mean signed test error | −11,279.3 units |

*All amounts refer to units used in the supplied dataset; they are not presented as USD. These are notebook-reported results, not independent reruns.*

![Comparison of held-out test MAE](./assets/tp4_test_mae.png)

**Interpretation:** The selected model reduces average absolute error relative to the baseline but has limited explanatory power (R² = 0.181) and tends to underpredict, particularly for higher incomes. Better MAE does **not** mean universally better performance.

## Methodology

### 1. Data inspection and quality checks

- Examined **10,000 records** with eight predictors and one income target.
- Identified missing values in weekly hours (**500**), education (**300**), and employer type (**400**).
- Found **86** exactly repeated rows after their first occurrence; did not automatically discard them.
- Kept extreme income values rather than assuming they were invalid.

### 2. Leakage-aware evaluation design

- Grouped identical input profiles together to keep the same profile from appearing in both development and test data.
- Used a group-aware hold-out test split and five-fold group-aware cross-validation for model selection.
- Fitted imputation, encoding, and scaling **inside** the training folds through Scikit-learn pipelines.
- Used test data only after selecting the model using cross-validation results.

### 3. Regression model comparison

| Candidate | Mean cross-validation MAE | Mean CV RMSE | Mean CV R² |
| --- | ---: | ---: | ---: |
| Median baseline | 36,359.0 | — | — |
| Linear regression (original income) | 31,216.5 | 57,423.6 | 0.271 |
| **Linear regression (log income)** | **29,483.3** | 60,789.6 | 0.182 |

*The notebook reports the baseline MAE but these particular summary figures do not specify baseline RMSE or R².*

The log-transformed candidate was chosen because it achieved the lowest cross-validation MAE. It performed **worse on RMSE and R²**, illustrating a meaningful trade-off rather than an across-the-board improvement.

### 4. Group-level error audit

The final model was evaluated on the held-out test set using subgroup sizes, MAE, RMSE, mean signed error, and bootstrapped confidence intervals.

**Selected results by sex:**

| Group | Test observations | MAE |
| --- | ---: | ---: |
| Female | 1,003 | 23,922.2 |
| Male | 1,004 | 34,691.8 |

The absolute MAE differs, but mean income also differs. The MAE-to-mean-income ratios reported in the notebook were **54.3%** and **53.1%**, respectively, showing why metrics should be interpreted in context. The notebook also analyzes categories of race, with smaller sample sizes for some groups.

**Important:** Differences in error are descriptive evidence of uneven model performance. They do not, by themselves, establish causal discrimination or the appropriateness of using the model to make real-world decisions.

## Technical Stack

| Area | Tools |
| --- | --- |
| Data preparation | Python, Pandas, NumPy |
| Modeling | Scikit-learn, LinearRegression, TransformedTargetRegressor |
| Validation | GroupShuffleSplit, GroupKFold, cross-validation |
| Preprocessing | Imputation, scaling, one-hot encoding, pipelines |
| Evaluation | MAE, RMSE, R², residuals, subgroup comparison |
| Reporting | Jupyter Notebook, Matplotlib |

## Why This Project Matters

This study demonstrates transferable capabilities relevant to freelance data-science projects:

- Building reliable preprocessing and modeling pipelines.
- Preventing data leakage through careful evaluation design.
- Comparing models using business-relevant metrics instead of one headline score.
- Investigating model errors across groups and documenting limitations.
- Communicating results clearly through a notebook and model card.

## Repository Files

```text
04-income-prediction-audit/
├── README.md
├── Actividad_4_Ingresos_Leakage_Sesgos.ipynb
├── census_income.xlsx
└── assets/
    └── tp4_test_mae.png
```

## Run Locally

Clone the repository:

```bash
git clone https://github.com/FrancoCurcho/Data-Science---Machine-Learning--.git
cd Data-Science---Machine-Learning--/04-income-prediction-audit
```

If the directory is still named `TP4`, use `cd Data-Science---Machine-Learning--/TP4` instead.

Create a Python environment and install the main dependencies:

```bash
python -m venv .venv
source .venv/bin/activate   # Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install pandas numpy matplotlib scikit-learn scipy jupyter openpyxl
jupyter notebook Actividad_4_Ingresos_Leakage_Sesgos.ipynb
```

Keep `census_income.xlsx` beside the notebook. **Reproducibility caveat:** These are suggested dependencies; versions have not been pinned and the full notebook has not been rerun here in a clean environment. Check the notebook's data-loading and library-version assumptions before execution.

## Limitations & Next Steps

- The test R² indicates limited predictive power. This is a methodological demonstration, **not a production-ready income estimator**.
- The log-transformed model underestimates income on average; future work could assess re-transformation corrections within cross-validation.
- Some demographic subgroups are small, so their estimates require caution.
- Models with and without sensitive attributes should be compared carefully; dropping such attributes alone does not guarantee fairness.
- A future iteration could add pinned dependencies, automated execution checks, and exported residual plots from the notebook.

## About the Project

This is an **academic project**, not a paid client assignment. All reported results refer to the particular dataset and evaluation described in the notebook and must not be generalized to other populations.

**Author:** [Franco Curcho](https://github.com/FrancoCurcho) · Biomedical Engineer · Artificial Intelligence postgraduate studies at the University of Buenos Aires (UBA)

---

*Trustworthy predictive modeling requires defensible evaluation, transparent limitations, and careful interpretation of errors.*
