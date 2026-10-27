# Data Science & Machine Learning Portfolio

**Python | Data Analysis | Machine Learning | Predictive Modeling | Model Evaluation**

Welcome to my Data Science and Machine Learning portfolio!

I'm **Franco Curcho**, a Biomedical Engineer pursuing advanced studies in Artificial Intelligence at the University of Buenos Aires (UBA).

I specialize in applying Python, statistical analysis, and machine learning techniques to solve complex problems, extract meaningful insights, and develop reliable data-driven solutions.

This repository contains practical projects covering exploratory data analysis, data quality assessment, anomaly detection, predictive modeling, explainable AI, and model auditing.

---

## Technical Skills

| Area | Technologies & Methods |
|---|---|
| Programming | Python, SQL |
| Data Analysis | Pandas, NumPy, Matplotlib, Seaborn |
| Machine Learning | Scikit-learn, Regression, Classification, Random Forest |
| Explainable AI | SHAP, Permutation Feature Importance |
| Data Quality | Missing Values, Outlier Detection, Data Drift |
| Model Evaluation | Cross-Validation, MAE, RMSE, R², Data Leakage Prevention |
| Development Tools | Jupyter Notebook, Git, GitHub |

---

## Featured Projects

### 01. Machine Learning Interpretability & Data Leakage Detection

**Predicting Data Science Salaries with Explainable AI**

[Explore Project](./TP1)

**Objective**

Develop and evaluate a salary prediction model while investigating feature importance, model reliability, and potential data leakage.

**Methods and Tools**
- Data preprocessing with Pandas.
- Regression modeling using Random Forest.
- Feature importance analysis using permutation importance.
- Local interpretability using SHAP.
- Model evaluation using MAE, RMSE, and R².
- Identification and correction of target leakage.

**Key Results**

| Metric | Original Model | After Leakage Correction |
|---|---:|---:|
| R² | 0.948 | 0.368 |
| MAE | $2,146 | $38,577 |
| RMSE | $15,091 | $52,595 |

**Key Insight**

The original model achieved an apparently excellent R² of 0.948. However, the analysis revealed target leakage caused by variables containing information directly related to the target.

After removing the problematic features, R² decreased to 0.368, providing a more realistic assessment of predictive performance.

**Practical Application**

This project demonstrates the importance of model auditing, feature selection, explainability, and reliable evaluation before deploying predictive systems.

---

### 02. Data Quality, Data Drift & Anomaly Detection

**Monitoring Data Reliability and Detecting Unusual Observations**

[Explore Project](./TP2)

**Objective**

Evaluate data quality, identify changes in feature distributions, and detect anomalous records that could affect analytical workflows and machine learning models.

**Methods and Tools**
- Data completeness and validity checks.
- Feature distribution analysis.
- Population Stability Index (PSI).
- Isolation Forest.
- Local Outlier Factor (LOF).
- Investigation and interpretation of anomalous observations.

**Key Insights**

The analysis investigates how changes in data distributions may affect model reliability and how anomaly detection methods can identify potentially unusual observations.

**Practical Application**

These techniques can support automated data validation, dataset monitoring, quality assurance, and the detection of inconsistencies in business data.

---

### 03. Exploratory Data Analysis — Communities and Crime

**Exploring Socioeconomic and Crime-Related Data**

[Explore Project](./Tp3)

**Objective**

Analyze the Communities and Crime dataset to explore socioeconomic variables, study statistical distributions, and investigate relationships within the data.

**Methods and Tools**
- Data loading and preprocessing.
- Exploratory Data Analysis (EDA).
- Descriptive statistics.
- Distribution and variable relationship analysis.
- Data visualization and interpretation.

**Practical Application**

Exploratory analysis helps organizations understand their data, identify meaningful patterns, and prepare datasets for more advanced statistical analysis and machine learning.

---

### 04. Regression Modeling, Data Leakage Prevention & Bias Auditing

**Building and Evaluating Reliable Income Prediction Models**

[Explore Project](./TP4)

**Objective**

Develop a regression workflow for income prediction, compare modeling approaches, implement leakage prevention strategies, and audit predictive performance across demographic groups.

**Methods and Tools**
- Missing-value imputation.
- Feature preprocessing with Scikit-learn pipelines.
- Linear Regression.
- Target transformation using logarithms.
- Group-aware data splitting and cross-validation.
- Model evaluation against a baseline.
- Model auditing and performance comparison across groups.

**Key Results**

| Model | Test MAE |
|---|---:|
| Median Baseline | 35,940 |
| Selected Regression Model | 29,310 |

The selected model reduced test MAE relative to the median baseline. The project also analyzes predictive limitations and differences in model performance across demographic groups.

**Practical Application**

This project demonstrates responsible model development, appropriate validation strategies, performance auditing, and the evaluation of models beyond a single aggregate metric.

---

## Repository Structure

```text
Analisis-de-datos-2/
│
├── TP1/
│   ├── Actividad_1_Interpretabilidad_Modelos.ipynb
│   └── ds_salaries.csv
│
├── TP2/
│   ├── Actividad_2_Calidad_Drift_Anomalias.ipynb
│   └── ds_salaries.csv
│
├── Tp3/
│   ├── Actividad_3_Communities_Crime.ipynb
│   ├── communities.data
│   └── communities.names
│
└── TP4/
    ├── Actividad_4_Ingresos_Leakage_Sesgos.ipynb
    └── census_income.xlsx
```

Project instructions and supporting materials are available within the corresponding directories.

---

## Running the Projects

Clone the repository:

```bash
git clone https://github.com/FrancoCurcho/Analisis-de-datos-2.git
cd Analisis-de-datos-2
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Install the main libraries:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn shap jupyter openpyxl threadpoolctl
```

Launch Jupyter:

```bash
jupyter notebook
```

Navigate to the desired project folder and open its notebook.

**Note:** These are the main dependencies identified in the notebooks. Package versions have not yet been pinned, and full reproducibility across environments has not been verified.

---

## What I Can Help You With

The techniques demonstrated in these projects can be applied to real-world business challenges, including:

- **Data Analysis:** cleaning, preprocessing, exploring, and visualizing datasets.
- **Python Automation:** automating repetitive data processing and reporting tasks.
- **Machine Learning:** developing and evaluating predictive models.
- **Data Quality:** detecting missing values, anomalies, inconsistencies, and distribution shifts.
- **Model Auditing:** identifying leakage, investigating feature importance, and evaluating model reliability.
- **Technical Reporting:** communicating analytical findings through documented workflows and visualizations.

My focus is on delivering clear, reproducible, and technically sound solutions.

---

## About This Portfolio

These projects were developed in an academic setting as part of my training in Artificial Intelligence.

They demonstrate practical techniques and analytical approaches that can be adapted to professional applications.

Performance metrics refer to the specific datasets and experimental setups described in each notebook; they should not be interpreted as guaranteed performance on other datasets.

---

## Let's Connect

I'm interested in freelance opportunities, collaborative projects, and professional roles involving Data Science, Machine Learning, Python development, and Artificial Intelligence.

**GitHub:** [FrancoCurcho](https://github.com/FrancoCurcho)

*Turning data into insights and building reliable AI solutions.*
