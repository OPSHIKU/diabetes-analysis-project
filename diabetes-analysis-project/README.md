# Diabetes Risk Analysis — Pima Indians Diabetes Dataset

A complete exploratory and statistical analysis of the **Pima Indians Diabetes Database**
(768 patients, 8 clinical features + outcome), covering data cleaning, univariate and
bivariate analysis, feature correlation, and formal hypothesis testing.

## Project Structure

```
diabetes-analysis-project/
├── README.md
├── requirements.txt
├── data/
│   ├── diabetes_raw.csv         # Original dataset (zeros = hidden missing values)
│   └── diabetes_cleaned.csv     # Cleaned & outlier-capped dataset used in the analysis
├── notebook/
│   └── diabetes_analysis.ipynb  # Full analysis notebook (cleaning, EDA, stats, charts)
└── report/
    └── Diabetes_Executive_Summary.pdf   # Executive summary with key charts & insights
```

## Dataset

- **Source:** National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK),
  originally distributed via the UCI Machine Learning Repository / Kaggle, mirrored on
  GitHub at [`jbrownlee/Datasets`](https://github.com/jbrownlee/Datasets).
- **Rows:** 768 female patients, age 21+, of Pima Indian heritage
- **Target:** `Outcome` (1 = diabetic, 0 = non-diabetic)
- **Features:** Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI,
  DiabetesPedigreeFunction, Age

## What's Inside the Notebook

1. **Data loading & inspection** — shape, dtypes, summary statistics
2. **Data cleaning**
   - Detection of physiologically impossible zero values (hidden missing data) in
     Glucose, BloodPressure, SkinThickness, Insulin, and BMI
   - Group-median imputation (by Outcome) for missing values
   - IQR-based outlier detection and winsorization (capping) across all numeric features
3. **Univariate analysis** — histograms, KDE plots, skewness/kurtosis, class balance
4. **Bivariate analysis** — violin plots and group means for every feature vs. Outcome
5. **Feature correlation matrix** — full heatmap + ranked correlation with Outcome
6. **Statistical hypothesis testing**
   - Welch's t-tests (with Cohen's d effect sizes) comparing every feature across
     diabetic vs. non-diabetic groups
   - Chi-square test of independence: pregnancy-count category vs. diabetes outcome
   - One-way ANOVA: glucose level across BMI categories
7. **Executive summary** — actionable insights for screening and modeling

## Key Findings

- **Glucose and Insulin** are the strongest predictors of diabetes (largest correlation
  with Outcome and largest effect sizes in hypothesis testing).
- **BMI and Age** are strong secondary predictors.
- **BloodPressure and DiabetesPedigreeFunction**, while statistically significant, have
  the weakest practical effect sizes.
- Diabetes prevalence **rises sharply with pregnancy count** (chi-square p < 0.05).
- The dataset is moderately **imbalanced** (65% non-diabetic / 35% diabetic) — models
  should use stratified sampling and F1/ROC-AUC rather than raw accuracy.

See `report/Diabetes_Executive_Summary.pdf` for the full write-up with charts, or open
`notebook/diabetes_analysis.ipynb` for the complete code and analysis.

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook notebook/diabetes_analysis.ipynb
```

## License

Dataset is public domain (NIDDK / UCI ML Repository). Analysis and code in this repo are
provided for academic/educational use.
