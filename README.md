# Predicting Heart Disease Risk with Statistical Analysis and Machine Learning

CS 746 PDS course project by Pranu Manandhar.

This project uses the UCI Heart Disease dataset to find which clinical and demographic factors are most closely linked to the presence of heart disease. It then tests whether simple statistical and machine learning methods can predict whether a patient has heart disease.

## Project status

| Stage | Status |
|---|---|
| 1. Data cleaning | Done |
| 2. Exploratory data analysis | Done |
| 3. Statistical testing (t-tests, chi-square) | Next |
| 4. Modelling (logistic regression vs. baseline and tree-based models) | Planned |
| 5. Final report | Planned |

## Repository structure

```
.
├── data/
│   ├── heart_disease_uci.csv      # raw data (920 patients, 4 hospitals)
│   └── cleveland_clean.csv        # cleaned Cleveland subset (304 patients), created by the notebook
├── figures/                       # all figures, created by the notebook
├── notebooks/
│   └── 01_data_cleaning_and_eda.ipynb
├── requirements.txt
└── README.md
```

## Dataset

The data is the UCI Heart Disease dataset, collected at the Cleveland Clinic Foundation, the Hungarian Institute of Cardiology (Budapest), the V.A. Medical Center (Long Beach) and University Hospital Zurich (Janosi et al., 1988). This repository uses the CSV version published on Kaggle by R. Karim Sony, which combines all four sites into one file with 16 columns.

- **Main analysis:** the Cleveland subset (304 patients), which has almost no missing values.
- **Target:** `num` is turned into a binary label: 0 means no disease, and 1–4 means disease present.

## How to reproduce

You need Python 3.10 or later.

```bash
pip install -r requirements.txt
cd notebooks
jupyter notebook 01_data_cleaning_and_eda.ipynb   # then Run All
```

Or run it without opening Jupyter:

```bash
cd notebooks
jupyter nbconvert --to notebook --execute --inplace 01_data_cleaning_and_eda.ipynb
```

Running the notebook recreates `data/cleveland_clean.csv` and every figure in `figures/`.

## Cleaning steps

1. Cholesterol and resting blood pressure values of 0 are physiologically impossible, so they are recoded as missing: 172 cholesterol values and 1 blood-pressure value.
2. Two exact duplicate rows are removed.
3. The Cleveland subset is selected. The other three sites are missing most values for `ca`, `thal` and `slope`.
4. The 9 missing values in Cleveland (`ca` 5, `thal` 3, `slope` 1) are filled with the most common value, and a flag column records which rows were changed.
5. Data types are fixed: `fbs` and `exang` become 0/1, `ca` becomes an integer, and the categorical columns get an explicit order.
6. Outliers are checked with the 1.5 × IQR rule. All flagged values are clinically plausible, so none are removed.

## References

- Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1988). *Heart Disease* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C52P4X
- Karim Sony, R. (n.d.). *Heart Disease Data* [Data set]. Kaggle. https://www.kaggle.com/datasets/redwankarimsony/heart-disease-data
