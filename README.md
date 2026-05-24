# Automobiles Dataset Analysis

This project analyzes an automobiles dataset from the 1970s–1980s in order to understand how vehicle characteristics relate to fuel efficiency.

The analysis combines exploratory data analysis, statistical testing, regression modeling, dimensionality reduction with PCA, and clustering.

---

## Project Overview

The goal of this project is to study the relationship between fuel efficiency and technical vehicle characteristics such as horsepower, weight, displacement, number of cylinders, model year and origin.

The project focuses on four main questions:

1. How are the variables distributed?
2. Which technical variables are most strongly related to fuel efficiency?
3. Which regression models best predict miles per gallon?
4. Can PCA and clustering reveal meaningful structure in the dataset?

---

## Dataset

Each row represents one vehicle described by technical and contextual variables.

Main variables:

- `miles_per_gallon`: fuel efficiency
- `cylinders`: number of engine cylinders
- `displacement`: engine displacement
- `horsepower`: engine power
- `weight_lbs`: vehicle weight
- `acceleration`: acceleration time
- `model_year`: production year
- `origin_country`: car origin encoded as USA, Europe or Japan

After preprocessing, the dataset contains **392 complete observations**.

---

## Exploratory Data Analysis

The exploratory analysis includes:

- descriptive statistics,
- comparison of fuel efficiency by origin,
- pairwise relationships between variables,
- correlation matrix,
- normality assessment using Q-Q plots,
- Shapiro-Wilk tests.

Key observations:

- Fuel efficiency is strongly negatively correlated with weight, displacement, horsepower and number of cylinders.
- Japanese and European cars tend to have higher average MPG than American cars.
- Engine-related variables are highly correlated, motivating the use of PCA.
- Most raw variables show departures from normality.

---

## Regression Models

Several regression approaches are used to predict `miles_per_gallon`.

### Univariate Regression

The first models use only `horsepower` as predictor:

- Linear regression with a `sqrt(horsepower)` feature
- Ridge regression
- MLP regressor

The best univariate model is the linear model with the additional square-root feature.

### Multivariate Regression

The multivariate models use several predictors:

- `horsepower`
- `weight_lbs`
- `displacement`
- `cylinders`
- `acceleration`
- `model_year`
- `origin_country`

Models used:

- Ridge regression
- MLP regression

Multivariate models significantly improve prediction performance compared to univariate models.

---

## PCA

Principal Component Analysis is applied to standardized explanatory variables.

The first three principal components explain almost 90% of the total variance.

PCA is used for:

- dimensionality reduction,
- visualization,
- preprocessing before regression.

The PCA representation helps reduce redundancy between highly correlated engine-related variables.

---

## PCA-Based Regression

Regression models are then trained using only the first three principal components.

Models:

- Ridge regression on 3 PCs
- MLP regression on 3 PCs

The MLP trained on the first three principal components achieves the best overall predictive performance in the project.

---

## Clustering

K-means clustering is applied to the standardized variables and visualized in PCA space.

The clustering analysis shows that:

- the dataset contains visible structure in PCA space,
- clusters are not perfectly separated,
- for `k = 3`, clusters mainly reflect different engine configurations, especially the number of cylinders.

---

## Results Summary

| Model | RMSE | R² |
|---|---:|---:|
| Linear + sqrt(horsepower) | 18.81 | 0.63 |
| Ridge, univariate | 22.11 | 0.57 |
| MLP, univariate | 20.32 | 0.60 |
| Ridge, multivariate | 10.77 | 0.79 |
| MLP, multivariate | 9.12 | 0.82 |
| Ridge on 3 PCs | 13.00 | 0.75 |
| MLP on 3 PCs | 8.18 | 0.84 |

The best model is the **MLP trained on the first three PCA components**, with:

- RMSE: `8.18`
- R²: `0.84`

---

## Key Takeaways

- Fuel efficiency is strongly influenced by vehicle weight, horsepower, displacement and number of cylinders.
- More recent cars and cars from Europe or Japan tend to be more fuel-efficient.
- Multivariate models outperform univariate models.
- PCA effectively summarizes redundant technical variables.
- PCA can improve the MLP by providing a compact and orthogonal input representation.
- K-means clustering mainly recovers engine-size related groups rather than entirely new hidden structures.

---

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn
- SciPy
- Scikit-learn

---

## Repository Structure

```bash
.
├── data/
│   └── automobiles.csv
│
├── notebooks/
│   └── data_analysis.ipynb
├── report/
│   └── data_analysis_final_report.pdf
│
├── requirements.txt
└── README.md
```

---

## How to Run

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the analysis notebook:

```bash
jupyter notebook notebooks/automobiles_analysis.ipynb
```

## Author

**Livio Singarin-Solé**

Master MLDM — Data Analysis Project
