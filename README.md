# DAM2026 Exam Project — Predicting Student Health Risk
This project compares machine learning models for predicting student
health categories from lifestyle and health-related features.

The target variable is `health_condition`, with three classes:
`at-risk`, `unhealthy` and `fit`.

The project was developed in Python using Google Colab.

## Competition Details
- **Name:** Playground Series S6E7 - Predicting Student Health Risk
- **Link:** [https://www.kaggle.com/competitions/playground-series-s6e7](https://www.kaggle.com/competitions/playground-series-s6e7)
- **Target:** `health_condition` (Multiclass classification: at-risk, unhealthy, fit)
- **Evaluation Metric:** Balanced Accuracy

## Dataset
The competition data are synthetically generated and were inspired
by the College Student Health Behavior Dataset.

| File | Rows | Columns | Purpose |
|---|---:|---:|---|
| train.csv | 690,088 | 15 | Model development and validation |
| test.csv | 295,753 | 14 | Competition predictions |
| sample_submission.csv | 295,753 | 2 | Submission format template |

### Numeric Features
- `sleep_duration`
- `heart_rate`
- `bmi`
- `calorie_expenditure`
- `step_count`
- `exercise_duration`
- `water_intake`

### Categorical Features

- `diet_type`
- `stress_level`
- `sleep_quality`
- `physical_activity_level`
- `smoking_alcohol`
- `gender`

### Target Distribution

| Health Condition | Count | Percentage |
|---|---:|---:|
| at-risk | 592,561 | 85.87% |
| unhealthy | 57,724 | 8.36% |
| fit | 39,803 | 5.77% |

## Team and Roles

| Member | Role | Responsibilities |
|---|---|---|
| Ogbe George Junior | Data and EDA | Data loading, feature descriptions, exploratory analysis and missing-value audit |
| Ododa Confidence | Preprocessing and Features | Model-specific preprocessing, categorical encoding, scaling and feature experiments |
| Opeyemi Alimi Jamiu | Modelling and Evaluation | Validation, baseline, model comparison, tuning and Kaggle submissions |

## Exploratory Data Analysis

The notebook includes numeric histograms, categorical bar charts,
boxplots by health condition and within-category target proportions.

The main findings were:

- Sleep duration differed noticeably across health categories.
  The unhealthy group had a lower median, while the fit group
  had a higher median.
- Stress level showed a strong association with the target.
  High-stress records had a larger unhealthy proportion, while
  low-stress records had a larger fit proportion.
- Fit records generally had higher step counts and longer
  exercise duration.
- BMI was generally higher in the unhealthy group and lower
  in the fit group, although distributions overlapped.
- Heart rate and water intake showed relatively similar
  distributions across classes.
- Missing values occurred in every predictor.
- No repeated rows with identical predictors and target were
  found after excluding `id`.

Unusual values were inspected rather than automatically removed.
These findings describe associations in synthetic data and should
not be interpreted as causal effects or clinical rules.

## Preprocessing

Preprocessing was implemented inside scikit-learn pipelines so
that learned transformations were fitted on training data only.

### Logistic Regression

- Numeric missing values filled with training medians.
- Numeric missing-value indicators added.
- Numeric inputs standardised.
- Categorical missing values represented as `missing`.
- Categorical features one-hot encoded.
- Balanced class weights used.

### Random Forest

- Numeric missing values filled with training medians.
- Numeric missing-value indicators added.
- Categorical missing values represented as `missing`.
- Categorical features one-hot encoded.
- No numeric scaling applied.
- Balanced class weights used.

### Histogram Gradient Boosting

- Numeric missing values handled directly by the model.
- Categorical missing values represented as `missing`.
- Categorical features ordinal encoded and explicitly identified
  as categorical inputs to the model.
- No numeric scaling applied.
- Balanced class weights used.

## Validation and Models

A stratified 80:20 training-validation split was created with
`random_state=42`. All model comparisons used this same split.

The following approaches were evaluated:

1. Most frequent class predictor: the trivial baseline.
2. Balanced logistic regression.
3. Balanced random forest.
4. Balanced histogram gradient boosting.

The baseline always predicted `at-risk`. It achieved approximately
85.87% ordinary accuracy but only 33.33% balanced accuracy,
demonstrating why ordinary accuracy alone is misleading here.

The validation set was used for several development comparisons,
so its results are not a completely independent final assessment.

## Feature Engineering

Two new features were tested:

- `sleep_duration_squared`: squared sleep duration.
- `steps_exercise_interaction`: step count multiplied by exercise duration.

Each feature was evaluated separately and together using the
same validation split and gradient boosting settings.

| Experiment | Validation Balanced Accuracy |
|---|---:|
| Original features | 0.949958 |
| Sleep duration squared | 0.949958 |
| Activity interaction | 0.949827 |
| Both engineered features | 0.949827 |

Neither feature improved validation performance. The original
feature set was retained.

## Hyperparameter Tuning
A grid search evaluated six combinations of:

- `max_leaf_nodes`: 15, 31 and 63
- `l2_regularization`: 1.0 and 10.0

The search used three-fold stratified cross-validation on a
120,000-record subset drawn from the training portion.
The external validation portion was excluded from the search.

The selected settings were then fitted on the full training
portion and evaluated on the existing validation set.

The tuned model achieved 0.949929 balanced accuracy, compared
with 0.949958 for the original gradient boosting model.
Tuning therefore did not improve validation performance.

## Results

All scores below use balanced accuracy.

| Model | Validation Score | Kaggle Public Score | Kaggle Private Score |
|---|---:|---:|---:|
| Most frequent class baseline | 0.333333 | Not submitted | Not submitted |
| Balanced logistic regression | 0.915104 | Not submitted | Not submitted |
| Balanced random forest | 0.947202 | 0.94698 | 0.94683 |
| Selected histogram gradient boosting | 0.949958 | 0.94973 | 0.94972 |
| CV-tuned histogram gradient boosting | 0.949929 | Not submitted | Not submitted |

Histogram gradient boosting was selected because it achieved
the highest validation balanced accuracy. It also achieved
higher public and private Kaggle scores than random forest.

For both submitted models, public Kaggle performance was close
to local validation performance.

## Submission Format

Two submission files were produced:

- `submission.csv`: histogram gradient boosting predictions.
- `submission_random_forest.csv`: random forest predictions.

Each submitted pipeline was retrained on all labelled training
records before predicting the competition test set.

Submission requirements:

- Columns: `id`, `health_condition`
- Header: `id,health_condition`
- Allowed labels: `at-risk`, `unhealthy`, `fit`
- Number of prediction rows: 295,753
- Test IDs: `690088`–`985840`
- No additional index column

## Repository Contents

The analysis and modelling code are organised in one Google Colab
notebook. It contains data loading, EDA, preprocessing, validation,
model comparisons, feature experiments, tuning and submission creation.

Other project files include:

- `README.md`: project overview, methods and results.
- `requirements.txt`: Python dependencies.
- `submissions/scores.md`: recorded validation and Kaggle scores.


## Running the Notebook in Google Colab

1. Download the project notebook from this repository.
2. Open https://colab.research.google.com/.
3. Choose **File → Upload notebook** and select the `.ipynb` file.
4. Download `playground-series-s6e7.zip` from the competition.
5. Run the notebook cells in order from the top.
6. When prompted by the upload cell, upload the competition ZIP.
7. The notebook extracts the CSV files into the Colab runtime.
8. Continue through EDA, model evaluation and submission creation.
9. Download the generated result files and save the notebook.

Colab runtime files and variables are temporary. After a runtime
reset, upload the data again and rerun the necessary earlier cells.

The code uses pandas, NumPy, scikit-learn and Matplotlib.
Additional dependencies can be installed in a Colab code cell with:

```python
!pip install -r requirements.txt
