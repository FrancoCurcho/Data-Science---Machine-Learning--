# Data Quality, Data Drift & Anomaly Detection

**Python · Pandas · Scikit-learn · Population Stability Index (PSI) · Isolation Forest · Local Outlier Factor**

> A reproducible academic case study examining how data quality, changing distributions, and unusual observations can affect analytical workflows. The objective is to **detect and explain potential issues**, not to label observations as erroneous without evidence.

## Project overview

Using the public `ds_salaries.csv` dataset (3,755 rows), this analysis compares a historical reference period (**2020–2021**) with a later period (**2022–2023**). It explores four variables: salary in USD, experience level, remote-work ratio and company size.

The workflow covers: (1) schema, completeness, domain and duplicate checks; (2) population distribution comparisons using PSI; (3) sensitivity tests; and (4) anomaly detection with two complementary algorithms.

## Key findings

### 1. Data quality and duplicate handling

- **3,755 input rows**; **1,171 exact duplicates** were identified.
- After deduplication, **2,584 rows** remained: **303** reference-period and **2,281** later-period records.
- The four audited variables had **no missing or out-of-domain values** in the displayed checks.
- Exact duplicate rows are not necessarily erroneous records. Deduplication is a modeling choice here and **changes sample frequencies**; results were also checked with duplicates retained.

### 2. Distribution shifts

PSI was calculated using quantile-defined salary bins from the reference period and fixed categorical bins for other features. The following values are from the saved notebook output, **after deduplication**:

| Variable | PSI | Interpretation under the study's thresholds |
| --- | ---: | --- |
| Salary in USD | **0.6722** | Important shift |
| Experience level | **0.5333** | Important shift |
| Remote-work ratio | **0.9481** | Important shift |
| Company size | **1.8506** | Important shift |

![PSI comparison across variables](assets/psi_comparison.png)

The proportion of senior profiles rose from approximately **30.0% to 64.1%**, hybrid work declined from **31.7% to 4.0%**, and the median salary increased from **$79,833 to $135,000**. These are **descriptive comparisons**, not causal conclusions. All four PSI alerts remained in the “important” category when duplicate rows were retained.

**Interpretation matters:** observed changes in predictor distributions are compatible with data drift, while salary distribution changes describe a shift in the target distribution. **PSI alone does not establish concept drift, covariate shift in the strict conditional sense, or the cause of any shift.**

### 3. Anomaly detection

After preprocessing, the analysis compared **Isolation Forest** (300 estimators) with **Local Outlier Factor** (20 neighbors), both using an exploratory contamination setting of 5%.

| Result | Count |
| --- | ---: |
| Flagged by Isolation Forest | 130 |
| Flagged by LOF | 130 |
| Flagged by both methods | **36** |
| Agreement over the union (Jaccard) | **0.161** |

The methods disagreed substantially: **94 records were flagged by Isolation Forest only, and 94 by LOF only**. An anomaly flag is a reason to review a record—not proof that the data should be deleted.

**Example investigation:** record index **3522**, a 2020 Research Scientist entry with a **$450,000** salary, was flagged by LOF but not Isolation Forest. It also exceeded the univariate salary IQR upper fence (about **$310,038**). LOF's classification was sensitive to the chosen number of neighbors, reinforcing the need for human review and contextual validation.

## Why this matters to a client

These methods can be used to design data-quality reports, compare new batches against a reference dataset, investigate outliers and decide when additional model validation is warranted. This repository is a **demonstration of analytical techniques**, not a deployed monitoring service or a prior client engagement.

## Technologies

- Python, Pandas and NumPy for preparation and checks
- Matplotlib for visualizations
- Scikit-learn for preprocessing, Isolation Forest and Local Outlier Factor
- Jupyter Notebook for documented, inspectable analysis

## Repository files

```text
02-data-quality-monitoring/  # rename TP2 to this, if desired
├── README.md
├── Actividad_2_Calidad_Drift_Anomalias.ipynb
├── ds_salaries.csv
└── assets/
    └── psi_comparison.png
```

## Running the analysis

Clone the parent repository (replace the directory path below with `TP2` until you rename it):

```bash
git clone https://github.com/FrancoCurcho/Data-Science---Machine-Learning--.git
cd Data-Science---Machine-Learning--/TP2
python -m venv .venv
source .venv/bin/activate   # Windows PowerShell: .venv\Scripts\Activate.ps1
python -m pip install pandas numpy matplotlib scikit-learn jupyter
jupyter notebook Actividad_2_Calidad_Drift_Anomalias.ipynb
```

The notebook expects `ds_salaries.csv` in the working directory (or in one of its documented fallback locations). Run it from the project directory. **Dependencies are not yet pinned and clean-environment reproducibility has not been verified.** The saved outputs were produced with Python 3.11.16, Pandas 3.0.5 and Scikit-learn 1.9.0, as recorded by the notebook; they are not a verified compatibility requirement.

## Limitations and next steps

- The reference group is much smaller than the later group; changes in dataset composition and collection practices can influence PSI.
- The study tests duplicate sensitivity but does not establish whether duplicate rows correspond to distinct workers.
- LOF warns about duplicate feature combinations and its flags can change with neighbor count.
- The proposed retraining strategy is **not implemented or benchmarked** in this notebook.
- A production workflow would require agreed quality rules, provenance checks, monitoring schedules, validation against model errors, and alert-review procedures.

---

**Author:** [Franco Curcho](https://github.com/FrancoCurcho) · Biomedical Engineer · Advanced studies in Artificial Intelligence (UBA)

*Interested in freelance work involving Python data cleaning, data-quality assessments, exploratory analysis, and machine learning evaluation.*
