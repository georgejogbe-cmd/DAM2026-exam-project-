# DAM2026 Project — Intermediate Status Report

**Team:** Ogbe George Junior, Ododa Confidence, Opeyemi Alimi Jamiu  
**Competition:** Playground Series S6E7 — Predicting Student Health Risk  
**Competition link:** https://www.kaggle.com/competitions/playground-series-s6e7  
**Target:** `health_condition` — at-risk, unhealthy and fit  
**Metric:** Balanced accuracy  
**Working environment:** Python in Google Colab  

## 1. What Has Been Done

### Data Loading and Exploratory Analysis — George

The synthetic dataset contains 690,088 training records and 295,753
test records. The training data have 15 columns: seven numeric
predictors, six categorical predictors, an identifier and the target.

The target is strongly imbalanced: 85.87% of records are at-risk,
8.36% are unhealthy and 5.77% are fit. Balanced accuracy gives equal
importance to recall for each class.

EDA included numeric histograms, categorical bar charts, boxplots
by health category and within-category target proportions.

Key findings were:

- Unhealthy records generally had shorter sleep duration, while
  fit records had longer sleep duration.
- High stress was associated with a larger unhealthy proportion.
- Fit records generally had higher step counts and longer exercise
  duration.
- BMI distributions differed across classes, although they overlapped.
- Heart rate and water intake showed relatively similar distributions
  across classes.

Missing values occurred in all 13 predictors. No repeated rows with
identical predictors and target were found after excluding `id`.
Unusual values were inspected and retained where there was no clear
evidence of error.

These patterns describe associations in synthetic data, not causal
effects or clinical rules.

### Preprocessing and Feature Engineering — Confidence

Preprocessing was implemented within scikit-learn pipelines.
Learned transformations were fitted on the training portion only
during validation.

For logistic regression and random forest, numeric missing values
were filled with training medians and missing-value indicators were
added. Categorical missing values were represented as `missing`,
followed by one-hot encoding. Numeric scaling was applied for
logistic regression but was unnecessary for random forest.

Histogram gradient boosting handled numeric missing values directly.
Categorical features were ordinal encoded and explicitly identified
as categorical inputs.

Two engineered features were tested separately and together:

- Squared sleep duration.
- Step count multiplied by exercise duration.

Squared sleep duration left balanced accuracy unchanged at 0.949958.
The activity interaction, alone or together with squared sleep
duration, produced 0.949827. Neither improved performance, so the
original features were retained.

### Modelling and Evaluation — Opeyemi

All models were compared using the same stratified 80:20
training-validation split with `random_state=42`.

A most frequent class predictor established the trivial baseline.
Three different trained model types were then evaluated:

1. Balanced logistic regression.
2. Balanced random forest.
3. Balanced histogram gradient boosting.

A grid search tested six combinations of `max_leaf_nodes` and
`l2_regularization` for gradient boosting. It used three-fold
stratified cross-validation on a 120,000-record subset of the
training portion, excluding the external validation portion.

The selected settings were fitted on the full training portion.
The tuned model scored 0.949929 on validation, compared with
0.949958 for the original gradient boosting model. Tuning did
not improve performance.

### Kaggle Submissions

The original histogram gradient boosting model was selected because
it achieved the highest validation balanced accuracy.

Both histogram gradient boosting and random forest were retrained
on all labelled training records. Their predictions were submitted
separately as `submission.csv` and `submission_random_forest.csv`.

Both submissions completed successfully after the competition
deadline.

## 2. Current Scores

All scores below are balanced accuracy.

| Model | Validation Score | Kaggle Public Score | Kaggle Private Score |
|---|---:|---:|---:|
| Most frequent class baseline | 0.333333 | Not submitted | Not submitted |
| Balanced logistic regression | 0.915104 | Not submitted | Not submitted |
| Balanced random forest | 0.947202 | 0.94698 | 0.94683 |
| Selected histogram gradient boosting | 0.949958 | 0.94973 | 0.94972 |
| CV-tuned histogram gradient boosting | 0.949929 | Not submitted | Not submitted |

Histogram gradient boosting performed best on both local validation
and Kaggle. Its public Kaggle score was approximately 0.023 percentage
points below its validation score.

The close scores suggest that performance transferred well to the
competition test data. However, repeated comparisons on the same
validation set mean that its score is a development estimate rather
than a completely independent final assessment.

## 3. Plan Until the Defence

| Member | Planned Work |
|---|---|
| Ogbe George Junior | Examine minority-class patterns further, refine feature descriptions and prepare the data and EDA presentation section. |
| Ododa Confidence | Review preprocessing, investigate feature contributions and document why the tested features were retained or rejected. |
| Opeyemi Alimi Jamiu | Assess model stability across additional training-data splits or folds, examine classification errors and finalise the model comparison. |
| All members | Finalise repository documentation, supporting materials and presentation slides; ensure individual contributions are visible through commits; practise the 15–20 minute group presentation and answers to questions. |

## 4. Sources and Acknowledgements

Competition: Yan, Y., Reade, W. and Park, E. (2026).
Predicting Student Health Risk. Kaggle.
https://www.kaggle.com/competitions/playground-series-s6e7

The supplied notebook `kaggle-s607-fastai-fold.ipynb` was consulted
as a reference example. Its author and original URL remain to be
identified for a complete acknowledgement.

The implemented solution uses scikit-learn pipelines, three model
types, separate feature experiments and a hyperparameter search.
