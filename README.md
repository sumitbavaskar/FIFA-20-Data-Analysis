# FIFA-20-Data-Analysis

## Project overview

This repository contains an end-to-end exploratory data analysis (EDA), feature engineering, and simple model creation work on the FIFA 20 player dataset. The goal is to analyze player attributes, engineer useful features, and build a model that predicts player ratings (or other targets) using the available attributes.

Files included in the repository:

* `EDA.ipynb` — Exploratory Data Analysis notebook (visualizations, distributions, correlations).
* `FeatureEngineering (3).ipynb` — Notebook with data cleaning, preprocessing, and feature engineering steps.
* `Model Creation.ipynb` — Notebook containing model training, evaluation and results.
* `players_20.csv` — Original/raw FIFA 20 players dataset (CSV).
* `cleaned_data.csv` — A cleaned/preprocessed CSV derived from the notebooks.
* `README.md` — This file.

> NOTE: file listing and repository structure referenced from the original GitHub repository.

## Goals and scope

1. Perform EDA to understand distributions and relationships between player attributes (e.g., age, nationality, overall rating, potential, positions, wage).
2. Clean and preprocess the dataset (handle missing values, convert categorical columns, extract/normalize features such as 'value' and 'wage').
3. Create new features that improve model performance (e.g., position groups, age buckets, aggregate skills).
4. Train and evaluate baseline machine learning models to predict player `overall` rating (or another chosen target).

## Quick start — requirements

Create a Python environment (recommended: `venv` or `conda`) and install the packages used in the notebooks. Typical packages used:

```bash
python -m pip install --upgrade pip
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

If you prefer a `requirements.txt`, you can create one with the environment packages above.

## How to reproduce the analysis

1. Clone the repository:

```bash
git clone https://github.com/sumitbavaskar/FIFA-20-Data-Analysis.git
cd FIFA-20-Data-Analysis
```

2. Start Jupyter Notebook / Lab and open the notebooks in the repo:

```bash
jupyter notebook
# or
jupyter lab
```

3. Run the notebooks in order:

   * `EDA.ipynb` — explore the data and visual outputs
   * `FeatureEngineering (3).ipynb` — run cleaning and feature engineering cells
   * `Model Creation.ipynb` — run model training and evaluation

**Tip:** If a notebook cell expects `players_20.csv` or `cleaned_data.csv` in a particular path, ensure those files are in the working directory (they are included in the repository).

## Data description (high level)

The dataset contains player-level details from FIFA 20. Typical columns you can expect (but verify in the CSV):

* Player identifiers and demographics: `sofifa_id`, `player_url`, `short_name`, `long_name`, `age`, `dob`, `nationality`.
* Contract/club info: `club`, `club_position`, `club_number`, `height`, `weight`.
* Skills and attributes: `overall`, `potential`, `pace`, `shooting`, `passing`, `dribbling`, `defending`, `physic`, and many more fine-grained attributes.
* Financials: `value_eur`, `wage_eur`, `release_clause_eur` (or the string versions which may require parsing).

Refer to the `players_20.csv` and `cleaned_data.csv` files in the repo for the exact column names and formats.

## Notebooks — short summaries

* **EDA.ipynb**

  * Overview of dataset size and missing values
  * Univariate distributions (age, overall rating, potential)
  * Correlation heatmap and pairwise relationships
  * Top players by position / nationality and other exploratory visualizations

* **FeatureEngineering (3).ipynb**

  * Parsing and normalizing monetary columns (`€` strings -> numeric)
  * Handling missing attributes, imputations, and dropping irrelevant columns
  * Encoding categorical variables (positions, club, nationality)
  * Creating derived features (e.g., `attack_score`, `defense_score`, `is_young_prospect`)

* **Model Creation.ipynb**

  * Splitting dataset into train/test sets
  * Training baseline models (e.g., Linear Regression, Random Forest)
  * Evaluating using RMSE, MAE, R² (or other metrics)
  * Simple hyperparameter tuning and feature importance analysis

## Example commands (train a model)

Inside `Model Creation.ipynb` there are runnable cells that demonstrate model training. To reproduce a minimal example in a script:

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error

df = pd.read_csv('cleaned_data.csv')
X = df.drop(columns=['overall'])
y = df['overall']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = RandomForestRegressor(n_estimators=100, random_state=42)
model.fit(X_train, y_train)
preds = model.predict(X_test)
print('RMSE:', mean_squared_error(y_test, preds, squared=False))
```

(Adjust feature selection and preprocessing to match the notebook steps.)

## Results & model notes

* The notebooks include baseline model results. Expect baseline performance to vary depending on features used and preprocessing.
* Use feature importance from tree-based models to identify which attributes (pace, shooting, passing, age, potential, etc.) most influence predictions.

## Suggestions / Improvements (next steps)

* Add a `requirements.txt` or `environment.yml` for reproducibility.
* Add small example scripts (`run_eda.py`, `train_model.py`) so users can run steps without opening notebooks.
* Add unit tests for key preprocessing functions.
* Expand model experiments: cross-validation, stacking, or gradient boosting (XGBoost/LightGBM) for improved accuracy.
* Add visual examples or sample output images (saved PNGs) to the repo to showcase EDA plots and model performance.

## Licence

No license file is provided in the repository. Add an open-source license (MIT, Apache-2.0, or similar) if you want others to reuse the work.

## Acknowledgements

* FIFA 20 dataset sources (check original data attribution if extracted from SOFIFA or other public sources) — be sure to follow their terms of use.

