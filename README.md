# DAM2026 Exam Project — Predicting Student Health Risk

## Competition Details
- **Name:** Playground Series S6E7 - Predicting Student Health Risk
- **Link:** [https://www.kaggle.com/competitions/playground-series-s6e7](https://www.kaggle.com/competitions/playground-series-s6e7)
- **Target:** `health_condition` (Multiclass classification: at-risk, unhealthy, fit)
- **Evaluation Metric:** Balanced Accuracy

- ## Submission Format
- Final file: `submission.csv` 
- Columns: `id`, `health_condition`
- Header exactly: `id,health_condition`
- Allowed labels: `fit`, `at-risk`, `unhealthy`
- No index column
- IDs span `690088`–`840404`

## Team & Roles
| Member | Role | Responsibilities |
|---|---|---|
| Ogbe George Junior | Data & EDA | Data loading, feature dictionary, EDA, missing values audit |
| Ododa Confidence | Preprocessing & Features | Encoding, scaling, leak-proof pipelines, feature engineering |
| Opeyemi Alimi Jamiu | Modeling & Evaluation | Validation scheme, baseline model, tuning, Kaggle submissions |

## Project Status (Intermediate Report)
- [x] Data loaded and explored (EDA completed).
- [x] Missing values identified and handled.
- [x] Preprocessing pipeline built (standard scaling & one-hot encoding).
- [x] Baseline model trained (Random Forest).
- [x] Advanced model trained (LightGBM with 5-Fold CV).
- [ ] Final presentation slides (Planned for defense).

## Results
| Model | Validation Score (Balanced Accuracy) | Kaggle Score |
|---|---|---|
| Baseline (Random Forest) | [PASTE YOUR BASELINE SCORE] | [PASTE KAGGLE SCORE] |
| Final (LightGBM + 5-Fold CV) | [PASTE LIGHTGBM CV SCORE] | [PASTE KAGGLE SCORE] |

## Repository Structure
- `notebooks/01-eda.ipynb` — Data description and EDA (George)
- `src/preprocessing.py` — Preprocessing pipeline (Confidence)
- `notebooks/03-modeling.ipynb` — Validation, baseline, models (Opeyemi)
- `submissions/` — Kaggle submission files and recorded scores (Confidence)
- `docs/` — Supporting document for the intermediate report

## Setup Instructions
1. `pip install -r requirements.txt`
2. Download the data from Kaggle into a `data/` folder.
3. Run notebooks in order: `01-eda.ipynb` → `03-modeling.ipynb`

## References
- Feature engineering logic (risk_factor, heart_rate_dev, bmi_dev, sleep_dev) was inspired by a public Kaggle notebook for this competition. We adapted these features into our own custom LightGBM pipeline.
