# Communities and Crime — Exploratory Data Analysis

**Python · Pandas · Descriptive Statistics · Data Visualization · Data Quality**

> **Portfolio case study:** Exploring a multivariate socioeconomic and crime dataset to understand its structure, assess data quality, and communicate patterns that deserve further investigation.

[View the analysis notebook](./Actividad_3_Communities_Crime.ipynb) · [Dataset documentation](./communities.names)

## Project Overview

Organizations often need to make sense of complex datasets before building predictive models or drawing conclusions. This project applies **exploratory data analysis (EDA)** to the *Communities and Crime* dataset, examining socioeconomic characteristics and crime-related indicators through descriptive statistics and visualization.

The emphasis is on understanding data distributions, missingness, variable relationships and interpretation limits — not claiming that correlations establish causality.

## Business-Relevant Skills Demonstrated

- Inspecting structured datasets and their accompanying data dictionaries.
- Preparing data for statistical analysis, including evaluating missing or non-applicable values.
- Summarizing numeric variables with descriptive statistics and distribution plots.
- Exploring relationships among variables and documenting relevant limitations.
- Communicating technical findings in an interpretable notebook.

These methods transfer to data profiling, quality assurance, research analytics, reporting and the discovery phase of machine-learning projects.

## Dataset

**Source:** UCI Machine Learning Repository — *Communities and Crime* dataset.

- `communities.data` — observations.
- `communities.names` — feature descriptions and dataset background.
- `Actividad_3_Communities_Crime.ipynb` — project notebook.

The dataset describes communities using socioeconomic, demographic and crime-related attributes. Consult `communities.names` for feature definitions, missing-value conventions, and source information before interpreting results.

## Analytical Workflow

| Stage | Purpose |
| --- | --- |
| **1. Data understanding** | Inspect variables, data types, source documentation and available observations. |
| **2. Data quality assessment** | Examine missing values, special-value markers and limitations in the records. |
| **3. Descriptive statistics** | Characterize central tendency, variability and potentially skewed distributions. |
| **4. Exploratory visualization** | Examine distributions and relationships among selected variables. |
| **5. Interpretation** | Explain observed patterns, caveats and implications for further analysis. |

## Findings and Interpretation

This project demonstrates a reproducible **exploratory approach**, rather than a deployed crime-prediction system. The principal deliverable is the documented notebook and its statistical/visual analysis.

**Important interpretation notes:**

- An observed association between socioeconomic indicators and crime measures does **not** establish causality.
- Missing values and variable definitions can influence comparisons; consult the data dictionary.
- The dataset is historical and should not be treated as a current description of communities.
- Findings should not be used to make decisions about individuals or communities without careful review of fairness, measurement limitations and broader context.

> **Planned portfolio enhancement:** Add two or three plots exported directly from the executed notebook, with exact statistics and written takeaways. Figures and numeric findings are intentionally not invented in this README.

## Technologies

- **Python** for data processing and analysis
- **Pandas and NumPy** for tabular manipulation and descriptive statistics
- **Matplotlib / Seaborn** for visualization, where used in the notebook
- **Jupyter Notebook** for a documented and inspectable workflow

## Reproducing the Analysis

From the root of the repository:

```bash
git clone https://github.com/FrancoCurcho/Data-Science---Machine-Learning--.git
cd Data-Science---Machine-Learning--/03-communities-crime-eda
```

> If you have not renamed the original `Tp3` directory yet, use `cd Data-Science---Machine-Learning--/Tp3` instead.

Create a virtual environment and install the main analysis packages:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install pandas numpy matplotlib seaborn jupyter scikit-learn
jupyter notebook Actividad_3_Communities_Crime.ipynb
```

The notebook and dataset files should remain in the same directory unless its relative file paths are adjusted. These are suggested dependencies; the full notebook has **not been freshly executed and validated** in a clean environment.

## Limitations and Next Steps

1. Verify that all notebook cells execute sequentially in a clean Python environment.
2. Export representative charts to an `assets/` directory and add concise evidence-based captions.
3. Add a verified results table with concrete statistics after reviewing notebook outputs.
4. Consider extracting reusable cleaning and plotting functions into a separate script.

## About This Project

Developed as an **academic data-analysis project**, presented here as a portfolio case study. It is not a commercial client engagement.

**Author:** [Franco Curcho](https://github.com/FrancoCurcho) · Biomedical Engineer · Artificial Intelligence studies at the University of Buenos Aires

---

*Good analytical work starts with careful data understanding and transparent limitations.*
