# Diabetes Classification & Risk Factor Modeling in Tidymodels

[![R Language](https://img.shields.io/badge/Language-R-blue.svg)](https://www.r-project.org/)
[![Framework](https://img.shields.io/badge/Framework-Tidymodels-orange.svg)](https://www.tidymodels.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An end-to-end Machine Learning pipeline utilizing the **Pima Indians Diabetes Dataset** to classify diabetes status based on clinical physiological markers. This project demonstrates modern data preprocessing, missing data handling via median/mode imputation, model training (Logistic Regression vs. Random Forest), and variable importance evaluation using the `tidymodels` ecosystem in R.

---

## Executive Summary

* **Objective:** Build and compare interpretable and ensemble classification models to predict diabetes onset while identifying primary clinical risk factors.
* **Best Model:** Both models achieved strong baseline performance on the test set, with **Logistic Regression** showing a slight edge in discrimination ($\text{ROC AUC} = 0.883$).
* **Key Finding:** Across both parametric and tree-based importance metrics, **Plasma Glucose Concentration** emerged as the single most dominant predictor of diabetes risk, closely followed by **BMI** and **Age**[cite: 1, 2].

---

## Performance Comparison

Model metrics evaluated on an independent 25% test set ($N = 125$) stratified by outcome[cite: 1, 2]:

| Model Architecture | Engine | Accuracy | ROC AUC | Primary Strength |
| :--- | :--- | :---: | :---: | :--- |
| **Logistic Regression** | `glm` | **0.832** | **0.883** | Highly interpretable, strong probability calibration[cite: 1, 2] |
| **Random Forest** | `ranger` | **0.832** | 0.874 | Captures non-linear feature interactions[cite: 1, 2] |

---

## Visualizations & Diagnostics

### 1. Model Discrimination (ROC Curve)
The Receiver Operating Characteristic (ROC) curve evaluates sensitivity versus specificity across decision thresholds for the Random Forest model on unseen test data[cite: 1, 2].

<p align="center">
  <img src="results/roc_curve.png" width="70%" alt="Random Forest ROC Curve">
</p>

### 2. Clinical Feature Importance
Permutation-based variable importance (`ranger`) highlights which clinical metrics drive the decision boundary[cite: 1, 2].

<p align="center">
  <img src="results/variable_importance.png" width="70%" alt="Variable Importance Plot">
</p>

> **Key Takeaway:** Glucose levels demonstrate more than double the predictive weight of the next highest physiological feature[cite: 1, 2]. This aligns directly with standard diagnostic criteria (e.g., Fasting Plasma Glucose / OGTT)[cite: 1, 2].

---

## Machine Learning Pipeline & Data Preprocessing

1. **Data Cleaning & Physiology Corrections:**
   * Replaced biologically impossible zero values in `bmi`, `glucose`, and `blood_pressure` with `NA`[cite: 1, 2].
2. **Train/Test Stratification:**
   * Split data 75/25 stratified by target variable (`outcome`) to preserve class balance across sets[cite: 1, 2].
3. **Recipe Transformations (`recipes`):**
   * `step_impute_median()` for numerical features[cite: 1, 2].
   * `step_impute_mode()` for categorical features[cite: 1, 2].
   * `step_dummy()` one-hot encoding for nominal predictors[cite: 1, 2].
   * `step_zv()` removal of zero-variance columns[cite: 1, 2].
   * `step_normalize()` feature scaling (z-score standardization) across all numeric predictors[cite: 1, 2].

---

## Repository Structure

```text
Diabetes-Predictive-Models/
├── data/
│   └── diabetes.csv                         # Raw Pima Indians Dataset
├── results/
│   ├── roc_curve.png
│   └── variable_importance.png
├── .gitignore
├── Diabetes-Predictive-Models.Rproj
├── LICENSE
├── README.md
├── Rodriguez_Katherine_Diabetes_Code.Rmd   # Primary R Markdown script
└── Rodriguez_Katherine_Diabetes_Code.pdf

```
## How to Reproduce

1. Clone the Repository

```{bash}
git clone [https://github.com/your-username/Diabetes-Predictive-Models.git](https://github.com/your-username/Diabetes-Predictive-Models.git)
cd Diabetes-Predictive-Models
```
2. Install Required R Packages

```{r}
install.packages(c("tidyverse", "tidymodels", "ranger"))

```
3. Run the Analysis

Open Rodriguez_Katherine_Diabetes_Code.Rmd in RStudio and click Knit (or run the chunks sequentially). Outputs will automatically update in the results/ folder.
---
## Future Roadmap

-  [ ] Implement $k$-fold cross-validation ($k=10$) for more robust variance estimation.
-  [ ] Hyperparameter tuning via grid search for mtry and min_n in ranger.
-  [ ] Integrate XGBoost / LightGBM workflows for gradient-boosted comparison.
-  [ ] Explore threshold tuning (e.g., Youden's $J$ statistic) to optimize sensitivity in clinical risk settings.

## Dependencies & Acknowledgments

-  Built with: `tidyverse`, `tidymodels`, `ranger`

-  Data Source: Pima Indians Diabetes Database (National Institute of Diabetes and Digestive and Kidney Diseases / UCI Machine Learning Repository).