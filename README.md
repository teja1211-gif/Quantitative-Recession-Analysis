# Quantitative Recession Analysis

A data-driven study of U.S. recession indicators using macroeconomic, labor-market, financial-market, and yield-curve data.

---

## 1. Project Overview

### Objective

Can historical macroeconomic and financial indicators be used to identify and forecast U.S. recession periods?

This project builds a quarterly dataset and applies **Logistic Regression** to estimate the probability of recession using indicators such as:

- Real GDP growth
- Unemployment rate and changes
- Inflation
- S&P 500 returns
- Treasury yield-curve spreads
- Federal Funds Rate

The project focuses not only on predictive performance, but also on understanding **which economic indicators are most informative for recession risk**.

---

## 2. Research Questions

The project will investigate:

1. Which macroeconomic and financial indicators are most strongly associated with U.S. recessions?
2. How accurately can Logistic Regression classify recession vs. non-recession quarters?
3. Which indicators contribute most to the model's recession probability?
4. Can information available in quarter `t` be used to forecast recession conditions in quarter `t+1`?
5. How does a time-aware evaluation differ from a conventional random train/test split?

---

## 3. Data

The initial study period is:

**1958 Q1 – 2009 Q3**

The final number of usable observations will be determined after merging the source datasets, engineering lagged/percentage-change features, and handling missing observations.

### Primary sources

| Source | Data |
|---|---|
| [FRED](https://fred.stlouisfed.org/) | GDP, Treasury yields, Federal Funds Rate and other economic indicators |
| [BLS](https://www.bls.gov/) | Unemployment and inflation/labor-market data |
| [Yahoo Finance](https://finance.yahoo.com/) | Historical S&P 500 market data |
| [NBER](https://www.nber.org/research/data/us-business-cycle-expansions-and-contractions) | Historical U.S. business-cycle/recession chronology |

The project uses primary/authoritative sources rather than relying on a pre-built Kaggle dataset.

---

## 4. Planned Features

The initial feature set is expected to include:

| Feature | Description |
|---|---|
| `gdp_growth` | Quarter-over-quarter real GDP growth |
| `unemployment_rate` | Quarterly unemployment rate |
| `unemployment_change` | Change in unemployment rate |
| `inflation` | Year-over-year CPI inflation |
| `sp500_return` | Quarterly S&P 500 return |
| `yield_spread` | Treasury long-term yield minus short-term yield |
| `fed_funds_rate` | Federal Funds Rate |

The exact feature definitions may be refined during exploratory analysis.

---

## 5. Target Variable

The target is:

```text
recession
```

with:

```text
0 = Non-recession
1 = Recession
```

Historical recession periods will be based on the **NBER U.S. business-cycle chronology**.

For the forecasting extension, the target will be shifted so that:

```text
Features at t  →  Recession at t+1
```

This allows the project to evaluate genuine forward-looking recession forecasting rather than simply classifying a period using information from the same period.

---

## 6. Methodology

### Data pipeline

```text
FRED ──────────────┐
                   │
BLS ───────────────┼──> Data Cleaning
                   │
Yahoo Finance ─────┤
                   │
NBER ──────────────┘
                         │
                         ▼
                  Quarterly Alignment
                         │
                         ▼
                  Feature Engineering
                         │
                         ▼
                    EDA / Analysis
                         │
                         ▼
                 Time-Aware Validation
                         │
                         ▼
                  Logistic Regression
                         │
                         ▼
              Evaluation & Interpretation
```

### Planned ML workflow

1. Collect historical data
2. Normalize dates and frequencies
3. Convert monthly/daily observations to quarterly features where appropriate
4. Merge all datasets
5. Construct NBER recession labels
6. Engineer lagged and percentage-change features
7. Remove/handle missing observations
8. Perform exploratory data analysis
9. Split data chronologically
10. Standardize features using training data only
11. Train Logistic Regression
12. Evaluate classification performance
13. Analyze model coefficients
14. Generate recession probabilities
15. Extend the model to `t → t+1` forecasting

---

## 7. Why Time-Aware Validation?

Economic data is inherently ordered in time.

A conventional random split can allow information from later periods to influence model development and produce overly optimistic results.

Therefore, the project will primarily use:

- Chronological train/test splits
- `TimeSeriesSplit` where appropriate
- Training-only fitting for preprocessing/scaling
- Explicit checks for look-ahead bias

The goal is to make the reported performance representative of a realistic historical forecasting setting.

---

## 8. Evaluation

Model performance will not be judged using accuracy alone.

Planned metrics:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix

Probability-based analysis will also be used through:

```python
model.predict_proba(X)
```

This allows the project to examine **recession probability**, rather than only a binary prediction.

---

## 9. Economic Interpretation

A major objective is interpretability.

Because Logistic Regression produces coefficients, the final analysis will examine how variables such as:

- GDP growth
- unemployment
- yield-curve slope
- stock-market returns
- inflation

relate to estimated recession risk.

The analysis will distinguish between **statistical association** and **causal claims**.

---

## 10. Repository Structure

```text
quantitative-recession-analysis/
│
├── data/
│   ├── raw/
│   │   ├── .gitkeep
│   │   └── ...
│   └── processed/
│       ├── .gitkeep
│       └── ...
│
├── notebooks/
│   ├── 01_setup.ipynb
│   ├── 02_data_collection.ipynb
│   ├── 03_data_cleaning.ipynb
│   ├── 04_eda.ipynb
│   ├── 05_logistic_regression.ipynb
│   └── 06_model_evaluation.ipynb
│
├── src/
│   ├── data_collection.py
│   ├── preprocessing.py
│   ├── features.py
│   ├── train.py
│   └── evaluate.py
│
├── figures/
│   └── ...
│
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 11. Technology Stack

### Programming

- Python

### Data

- Pandas
- NumPy
- Requests
- yfinance

### Visualization

- Matplotlib
- Seaborn

### Machine Learning

- Scikit-learn

### Data Sources / APIs

- FRED API
- BLS API
- Yahoo Finance
- NBER historical business-cycle data

---

## 12. Planned Deliverables

The completed project will contain:

- [ ] Reproducible data-collection pipeline
- [ ] Clean quarterly dataset
- [ ] NBER recession labels
- [ ] Exploratory visualizations
- [ ] Correlation analysis
- [ ] Logistic Regression classifier
- [ ] Time-aware train/test evaluation
- [ ] Confusion matrix
- [ ] ROC curve / ROC-AUC
- [ ] Feature coefficient analysis
- [ ] Recession probability visualization
- [ ] Forward-looking `t → t+1` forecasting experiment
- [ ] Final results and conclusions

---

## 13. Project Roadmap

### Phase 1 — Setup
- [x] Create repository structure
- [x] Define research question
- [x] Define initial variables
- [ ] Set up Python environment

### Phase 2 — Data Collection
- [ ] Retrieve FRED data
- [ ] Retrieve BLS data
- [ ] Retrieve S&P 500 data
- [ ] Retrieve NBER recession chronology

### Phase 3 — Data Engineering
- [ ] Normalize dates
- [ ] Convert all sources to quarterly frequency
- [ ] Merge datasets
- [ ] Engineer features
- [ ] Handle missing observations
- [ ] Create target labels

### Phase 4 — Exploratory Data Analysis
- [ ] Plot GDP and recessions
- [ ] Analyze unemployment
- [ ] Analyze inflation
- [ ] Analyze S&P 500 returns
- [ ] Analyze yield curve
- [ ] Create correlation analysis

### Phase 5 — Machine Learning
- [ ] Build baseline Logistic Regression
- [ ] Implement time-aware validation
- [ ] Standardize features correctly
- [ ] Evaluate predictions
- [ ] Analyze coefficients

### Phase 6 — Forecasting Extension
- [ ] Build `t → t+1` target
- [ ] Test forward-looking predictions
- [ ] Check for look-ahead bias
- [ ] Compare results

### Phase 7 — Finalization
- [ ] Clean notebooks
- [ ] Refactor reusable code
- [ ] Add final figures
- [ ] Document findings
- [ ] Update README with verified results

---

## 14. Reproducibility

The project is intended to be reproducible from the raw source data.

API keys and secrets will **never** be committed to GitHub.

Local secrets should be stored in a `.env` file or environment variables.

Example:

```text
FRED_API_KEY=your_api_key_here
```

See `.env.example` for the expected configuration.

---

## License

This project is intended for educational and portfolio purposes.
