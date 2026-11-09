# DAM2026 Project - Intermediate Status Report

**Team:** Ogbe George Junior, Ododa Confidence, Opeyemi Alimi Jamiu  
**Competition:** Playground Series S6E7 - Predicting Student Health Risk  
**Target:** `health_condition` (3-class classification: at-risk, unhealthy, fit)  
**Metric:** Balanced Accuracy  

## 1. What has been done

*   **Data Loading & EDA (George):** The dataset contains 690,088 training rows and 15 columns. We identified 7 numeric features (e.g., `bmi`, `sleep_duration`) and 6 categorical features (e.g., `diet_type`, `stress_level`). The target `health_condition` is highly imbalanced (85.87% at-risk, 8.36% unhealthy, 5.77% fit). This means plain accuracy is misleading, and the model must be optimized for balanced accuracy.
*   **Missing Values & Preprocessing (Ododa):** Almost all features have missing values. We decided to handle numeric features using median imputation (robust to outliers) and categorical features using a constant imputation strategy (filling with the string `"missing"`, as the absence of data can be a predictive signal). We built a leak-proof `ColumnTransformer` pipeline for scaling and one-hot encoding. 
*   **Modeling & Evaluation (Opeyemi):** We set up a Stratified 5-Fold Cross-Validation scheme. We established a baseline using a Random Forest Classifier with `class_weight='balanced'`. We then implemented an advanced LightGBM model, applying feature engineering (creating a `risk_factor` based on health habits, and deviations from normal BMI/heart rate/sleep).
*   **Submission:** We generated a `submission.csv` using the ensemble of our 5 LightGBM models and submitted it to Kaggle.

## 2. Current Scores

| Model | Validation Score (Balanced Accuracy) | Kaggle Score |
| :--- | :--- | :--- |
| Baseline (Random Forest) | [INSERT BASELINE SCORE] | [INSERT KAGGLE SCORE] |
| Final (LightGBM + 5-Fold CV) | [INSERT LIGHTGBM SCORE] | [INSERT KAGGLE SCORE] |

*(Note: Replace the brackets with your actual scores from Colab and Kaggle).*

## 3. Plan until defense

*   **George:** Conduct deeper EDA on the minority classes (`unhealthy`, `fit`). Create the final 15-20 minute presentation slide deck and ensure the GitHub repository is clean and well-documented.
*   **Ododa:** Experiment with additional feature engineering (e.g., combining activity levels). Verify that the final preprocessing pipeline is optimized and robust.
*   **Opeyemi:** Train at least one more model type (e.g., Logistic Regression) to fulfill the "three different models" requirement. Tune LightGBM hyperparameters using RandomizedSearchCV and compare the results in a final model comparison table.
*   **All:** Practice the final presentation and prepare to answer questions about individual contributions.
