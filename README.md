# Diabetes Risk Prediction — Exploratory Data Analysis & Classification

A self-directed data science project exploring which health and lifestyle factors best predict diabetes risk, using a 100,000-patient dataset.

## Dataset

[Diabetes Prediction Dataset](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset) (Kaggle) — 100,000 patient records, 9 features (age, BMI, hypertension, heart disease, smoking history, HbA1c level, blood glucose level, gender) and a binary diabetes label.

The CSV is not included in this repo (3.8 MB, easily re-downloaded from Kaggle). Download it and place it in the project root as `diabetes_prediction_dataset.csv` to run the notebook.

## What this project covers

- **Data cleaning**: handling implicit missingness (35,816 "No Info" entries in smoking history), duplicate removal, categorical encoding, and a documented decision to keep extreme BMI values as plausible clinical cases rather than outliers to drop.
- **Train/validation/test split (70/15/15)** done before any modeling decisions, with the test set untouched until final evaluation.
- **Descriptive statistics and manual distribution analysis** (mean, median, std, skewness) computed with NumPy.
- **Visualization**: feature distributions, diabetes rate by age group, boxplots by diabetes status, correlation heatmap.
- **Probability analysis**: conditional probabilities (e.g. P(diabetes | hypertension), P(diabetes | HbA1c ≥ 6.5%)) and a Monte Carlo simulation estimating expected diabetic cases in a random screening of 1,000 patients.
- **Classification**: Logistic Regression and Decision Tree, evaluated on accuracy, precision, recall, and F1 — chosen specifically because the dataset is imbalanced (~8.5% positive class), which makes accuracy alone misleading.

## Results

Decision Tree was selected as the better-performing model on the validation set and evaluated once on the held-out test set:

| Metric | Score |
|---|---|
| Accuracy | 0.973 |
| Precision | 1.000 |
| Recall | 0.697 |
| F1 | 0.821 |

HbA1c level and blood glucose were the strongest predictors, consistent with clinical diagnostic guidelines.

## Known limitations

- **Recall is the weak point.** The model misses roughly 30% of actual diabetes cases. In a screening context that's a real cost (false negatives matter more than false positives), and it's the main thing I'd address next — likely with class weighting, resampling, or a different decision threshold.
- Only two model families were tried. Ensemble methods (Random Forest, XGBoost) would likely close some of the recall gap.
- The dataset is synthetic; real-world clinical data would behave differently, especially around the imputed smoking-history values.

## Stack

Python · NumPy · Pandas · Matplotlib · Seaborn · Scikit-learn

## Files

- `diabetes_project.ipynb` — full analysis and modeling notebook
- `diabetes.pptx` — summary presentation
