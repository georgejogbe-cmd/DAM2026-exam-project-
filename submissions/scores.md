# KAGGLE SUBMISSION SCORE

All scores use balanced accuracy.

| Model | Submission File | Validation Score | Kaggle Public Score | Kaggle Private Score |
|---|---|---:|---:|---:|
| Random Forest | submission_random_forest.csv | 0.947202 | 0.94698 | 0.94683 |
| Selected Histogram Gradient Boosting | submission.csv | 0.949958 | 0.94973 | 0.94972 |

## EVALUATION NOTE

- Local validation used the same stratified 80:20 split for both models.
- Each submission model was retrained on all labelled training records.
- Both Kaggle submissions completed successfully after the competition deadline.
- Histogram gradient boosting achieved the highest validation and Kaggle scores.
- The trivial most frequent class baseline achieved 0.333333 validation balanced accuracy and was not submitted to Kaggle.
