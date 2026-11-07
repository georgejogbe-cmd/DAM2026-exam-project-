# DAM2026 Exam Project — [INSERT COMPETITION NAME]

## Competition
- **Name:** [INSERT COMPETITION NAME]
- **Link:** [INSERT LINK]
- **Target:** [INSERT TARGET COLUMN]
- **Evaluation Metric:** [INSERT METRIC]

## Team & Roles
| Member | Role | Owns |
| Ogbe George Junior | Data & EDA | Data loading, feature dictionary, EDA, missing values audit |
| Ododa Confidence | Preprocessing & Features | Encoding, scaling, leak-proof pipelines, feature engineering |
| Opeyemi Alimi Jamiu | Modeling & Evaluation | Validation scheme, baseline model, tuning, Kaggle submissions |

## Repository Structure
- `notebooks/01-eda.ipynb` — Data description and EDA (George)
- `src/preprocessing.py` — Preprocessing pipeline (Confidence)
- `notebooks/03-modeling.ipynb` — Validation, baseline, models (Opeyemi)
- `submissions/` — Kaggle submission files and recorded scores (Confidence)
- `docs/` — Supporting document for the intermediate report

## How to reproduce
1. `pip install -r requirements.txt`
2. Download data from [] into `data/`
3. Run notebooks in order 01 → 03
