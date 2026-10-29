# Salary Prediction Model — Explainability & Data Leakage Audit

**Python · Scikit-learn · Random Forest · SHAP · Permutation Importance · Model Validation**

> **Case study:** Auditing a regression model that appeared highly accurate but relied on information that would not be appropriate as predictors in a real-world salary prediction scenario.

## At a Glance

| | |
| --- | --- |
| **Problem** | Can we trust an apparently excellent salary prediction model? |
| **Dataset** | Data Science Salaries (`ds_salaries.csv`) |
| **Task** | Regression: predict `salary_in_usd` |
| **Methods** | Random Forest, permutation feature importance (PFI), SHAP |
| **Main finding** | `salary` and `salary_currency` caused target leakage |
| **Deliverable** | Reproducible analytical Jupyter notebook and evaluation |

![Comparison of evaluation metrics before and after leakage correction](assets/model_comparison.png)

## Business Question

A machine learning model can report excellent evaluation metrics while making predictions using information that would not legitimately be available at prediction time. This case study investigates **whether high predictive performance reflects a meaningful model or a data leakage problem**.

This matters for data science consulting, because choosing and validating the right predictors can be more valuable than achieving an impressive but misleading score.

## Workflow

1. **Inspect the dataset.** Review variable types, missing values, and duplicate records. The original analysis reports **1,171 exact duplicate rows**; these are removed before the train/test split to reduce the risk of identical observations appearing on both sides.
2. **Establish a baseline and initial model.** Compare a median baseline with a Random Forest regressor using an 80/20 train/test split (`random_state=42`). Categoricals are one-hot encoded in a Scikit-learn pipeline.
3. **Audit feature importance.** Use permutation feature importance (PFI) to measure the effect of disrupting each input feature on test MAE.
4. **Explain individual predictions.** Use SHAP to inspect how features affect selected low- and high-salary predictions.
5. **Remove leaked predictors.** Exclude `salary` and `salary_currency`, retrain, reevaluate, and reassess feature importance.

## Results

| Test metric | Initial Random Forest | Leakage-corrected Random Forest |
| --- | ---: | ---: |
| **R²** | **0.948** | **0.368** |
| **MAE** | **$2,146** | **$38,577** |
| **RMSE** | **$15,091** | **$52,595** |

The original notebook also reports a **median-baseline MAE of $53,555**. The corrected model outperforms that baseline on this experimental split, but its error remains substantial.

### What revealed the leakage?

In the initial model, permuting `salary` increased MAE by about **$70,297**, and permuting `salary_currency` increased it by approximately **$11,515**. Both variables were linked directly to the conversion used to obtain the USD-denominated target. SHAP explanations of individual predictions confirmed the same dependency.

After removing these columns, the reported R² dropped from **0.948 to 0.368**. That drop should **not** be interpreted as a failure of the audit: it reveals that the previous performance was not a defensible estimate for the intended prediction task.

The corrected model placed greater importance on variables such as employee residence, experience level, and job title.

## Key Takeaways

- **Model performance must be interpreted in context.** High R² can conceal invalid predictors.
- **Explainability complements validation.** PFI revealed a global pattern; SHAP illustrated it at the prediction level.
- **Feature availability matters.** Inputs must be justified for the decision point at which a model will be used.
- **Good reporting includes limitations.** Results apply to this dataset and split; they are not evidence of generalization to an arbitrary salary dataset.

## Repository Files

| File | Purpose |
| --- | --- |
| [`Actividad_1_Interpretabilidad_Modelos.ipynb`](Actividad_1_Interpretabilidad_Modelos.ipynb) | Complete analysis, code, visualizations, and interpretation (Spanish) |
| [`ds_salaries.csv`](ds_salaries.csv) | Dataset used by the notebook |
| [`assets/model_comparison.png`](assets/model_comparison.png) | Summary chart for the README |

## Run the Notebook

From the repository root:

```bash
cd TP1
python -m venv .venv
```

Activate the environment:

```bash
# Linux / macOS
source .venv/bin/activate

# Windows PowerShell
# .venv\Scripts\Activate.ps1
```

Install the main dependencies:

```bash
python -m pip install numpy pandas matplotlib seaborn scikit-learn shap jupyter
```

Then run:

```bash
jupyter notebook Actividad_1_Interpretabilidad_Modelos.ipynb
```

**Reproducibility note:** The project has not yet been tested end-to-end in a fresh, version-pinned environment. Package versions, especially Scikit-learn and SHAP, may affect compatibility. The notebook expects `ds_salaries.csv` in the working directory (or an `upload/` subdirectory).

## Scope and Limitations

This is an **academic case study**, not a commissioned client project. The analysis uses an observational dataset and a single train/test split. Reported performance should not be considered production-ready, and feature importance is not a causal interpretation. Removing exact duplicate records is a modeling choice that should be revisited according to the provenance and intended use of a new dataset.

## Related Freelance Services

The workflow showcases capabilities relevant to:

- Auditing regression and classification models for leakage and validation issues.
- Cleaning datasets and building repeatable preprocessing pipelines.
- Comparing machine learning models against meaningful baselines.
- Interpreting predictions and communicating limitations to stakeholders.

**Portfolio:** [Data Science & Machine Learning](../README.md) · [GitHub profile](https://github.com/FrancoCurcho)
