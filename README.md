# Diabetes-Predictive-Models
This project builds predictive models for diabetes status using the Pima Indians diabetes dataset. The workflow includes data cleaning (removing impossible values), outcome recoding, and model development using tidymodels. Logistic regression and random forest models are evaluated with accuracy and ROC AUC, and ROC curves are visualized to compare performance. Variable importance is analyzed to highlight which health metrics contribute most to diabetes prediction.

## Data Preparation
- Load the dataset with 500 observations and 7 variables
- Converted character variables to factors
- Replaced impossible values (0 for glucose, blood pressure, BMI) with NA
- Recoded the outcome variable into:
  - "No diabetes"
  - "Diabetes
 
## Modeling Workflow
- Train/test split (75/25) stratified by outcome)
- Preprocessing recipe:
  - Median imputation for numeric predictors
  - Mode imputation for nominal predictors
  - Dummy encoding
  - Remove zero-variance predictors
  - Normalize numeric predictors
 
## Models
- **Logistic Regression**
  - Interpretable baseline model
- **Random Forest**
  - 500 trees
  - Permutation-based variable importance

## Evaluation Metrics
- Accuracy and ROC AUC calculated on the test set
- Results:
  - Logistic Regression: Accuracy = 0.864, ROC AUC = 0.908
  - Random Forest: Accuracy = 0.896, ROC AUC = 0.934

## Visualizations
- ROC curve for random forest
- Variable importance plot showing:
  - Glucose as the strongest predictor
  - Age, BMI, and insulin are also contributing

## Summary
Both models performed well, with the random forest achieving slightly higher accuracy and ROC AUC. Variable importance results align with clinical expectations, highlighting glucose as the most influential predictor of diabetes risk.  
