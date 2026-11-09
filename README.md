# DAM2026 Exam Project — Predicting Student Health Risk

## Competition
- **Name:** Playground Series S6E7 - Predicting Student Health Risk
- **Link:** https://www.kaggle.com/competitions/playground-series-s6e7
- **Target:** `health_condition` (Multiclass classification)
- **Evaluation Metric:** Balanced Accuracy

## Team & Roles
| Member | Role | Owns |
|---|---|---|
| Ogbe George Junior | Data & EDA | Data loading, feature dictionary, EDA, missing values audit |
| Ododa Confidence | Preprocessing & Features | Encoding, scaling, leak-proof pipelines, feature engineering |
| Opeyemi Alimi Jamiu | Modeling & Evaluation | Validation scheme, baseline model, tuning, Kaggle submissions |

## Repository Structure
- `notebooks/01-eda.ipynb` — Data description and EDA (George)
- `src/preprocessing.py` — Preprocessing pipeline (Confidence)
- `notebooks/03-modeling.ipynb` — Validation, baseline, models (Opeyemi)
- `submissions/` — Kaggle submission files and recorded scores (Opeyemi)
- `docs/` — Supporting document for the intermediate report

## How to reproduce
1. `pip install -r requirements.txt`
2. Download data from Kaggle into `data/`
3. Run notebooks in order 01 → 03

## References
- Feature engineering (risk_factor, heart_rate_dev, bmi_dev, sleep_dev) was inspired by a public Kaggle notebook for this competition. We adapted these features into our own LightGBM pipeline.
