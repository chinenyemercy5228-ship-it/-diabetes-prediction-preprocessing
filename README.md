# Diabetes Prediction Dataset — Data Cleaning, EDA & Preprocessing

A public health-informed exploration of a 100,000-patient diabetes dataset: cleaning, exploratory analysis, and preprocessing in preparation for future model training.

## 📊 Dataset

**Source:** [Diabetes Prediction Dataset](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset) by Mohammed Mustafa, via Kaggle

100,000 patient records with the following features:

| Column | Description |
|---|---|
| `gender` | Female / Male / Other |
| `age` | Patient age |
| `hypertension` | 0 = No, 1 = Yes |
| `heart_disease` | 0 = No, 1 = Yes |
| `smoking_history` | never, current, former, ever, not current, No Info |
| `bmi` | Body Mass Index |
| `HbA1c_level` | Average blood sugar level over 2-3 months |
| `blood_glucose_level` | Blood glucose level at time of measurement |
| `diabetes` | Target variable — 0 = No, 1 = Yes |

*The raw CSV is not included in this repo — download it directly from the Kaggle link above.*

## 🎯 Objective

Approach this dataset the way a public health background demands: clean it carefully, question assumptions before applying textbook rules, and let the data confirm (or challenge) what clinical knowledge already suggests about diabetes risk factors.

## 🧹 What Was Done

**1. Data Cleaning**
- Checked for missing values — none found (fully complete dataset)
- Identified and removed 3,854 exact duplicate rows (100,000 → 96,146 records)
- Relabeled the ambiguous `"No Info"` category in `smoking_history` to `"unknown"` — kept as its own category rather than dropped, since it represented roughly a third of all records

**2. Exploratory Data Analysis**
- Descriptive statistics overall and split by diabetes outcome
- Univariate distributions (histograms, bar charts) for every column
- Bivariate analysis — how each feature individually relates to diabetes outcome
- Correlation analysis across numeric features

**3. The Outlier Decision**
Standard practice is to flag and remove statistical outliers. Before doing that, I checked who the flagged outliers actually were in `HbA1c_level` and `blood_glucose_level` — and found they were overwhelmingly diabetic patients. These aren't data errors; HbA1c and glucose are the literal diagnostic markers for diabetes, so extreme values are exactly what a severely diabetic patient's chart looks like. **No outliers were removed from these columns.**

**4. Encoding**
- One-hot encoded `gender` and `smoking_history` (`pd.get_dummies`, `drop_first=True`) — neither column has a natural order, so one-hot avoids implying a false ranking
- Dataset is now fully numeric and ready for the next phase

## 🔑 Key Insight

Diabetic patients in this dataset were, on average, **21 years older**, had a **higher BMI**, and showed **hypertension and heart disease rates roughly 4-5x higher** than non-diabetic patients — confirming the dataset behaves consistently with real-world clinical patterns before any modeling was even attempted.

## 🛠️ Tech Stack

- Python
- Pandas
- Matplotlib
- Jupyter Notebook

## 📌 Status

**Preprocessing complete — model training is next.** This repo currently covers cleaning, EDA, and encoding. A future update will cover handling class imbalance (only ~8.8% of records are diabetic), feature scaling, model training, and evaluation.

## 🙏 Acknowledgments

Built as part of the **TechRise AI & ML Track**, with guidance from my tutor.

## 👋 About

I'm a Public Health professional transitioning into AI/ML, building healthcare technology solutions with Python — one dataset at a time. Connect with me on www.linkedin.com/in/elechi-chinenye-freelancer or follow along as I build this out further.
