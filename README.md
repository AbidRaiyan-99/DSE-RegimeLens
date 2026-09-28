# DSE RegimeLens

**Market Regime Detection and Next-Day Regime Prediction using K-Means and XGBoost on Dhaka Stock Exchange data.**

## Overview

DSE RegimeLens is a machine learning project that identifies market regimes in the Dhaka Stock Exchange (DSE) and evaluates whether aggregate market features can predict the next trading day's regime.

The project uses **K-Means clustering** to discover market regimes from historical DSE data and **XGBoost** to predict the next day's regime. A simple **persistence baseline** is also evaluated to determine whether machine learning provides predictive value beyond the tendency of market regimes to persist over time.

The three discovered regimes are descriptively interpreted as:

* **Bull / Expansion**
* **Neutral / Stable**
* **Bear / Contraction**

## Objectives

* Clean and validate historical DSE market data
* Construct daily market-level indicators
* Identify distinct market regimes using unsupervised learning
* Predict the next day's market regime using XGBoost
* Compare XGBoost against a persistence baseline
* Evaluate performance using accuracy and Macro F1
* Investigate the limitations of next-day regime prediction

## Dataset

The project uses the **Dhaka Stock Exchange Historical Data (1999–2025)** dataset.

The original data contains historical observations for DSE-listed securities with the following fields:

* `Trading_Code`
* `Date`
* `Open`
* `High`
* `Low`
* `Close`
* `Volume`

After data validation and cleaning, the working dataset contained approximately **1.43 million observations** with duplicate stock-date records, invalid OHLC records, and zero-trading records removed.

The raw dataset is **not included in this repository** because of its large size.

## Methodology

### 1. Data Cleaning

The dataset was checked for:

* Missing values
* Duplicate stock-date records
* Invalid OHLC relationships
* Zero or non-positive trading values

The cleaned data was sorted chronologically by stock and date.

### 2. Return Calculation

Daily stock returns were calculated using the percentage change in closing price:

`Return = Close_t / Close_(t-1) - 1`

Extreme returns outside the range of **-50% to +50%** were excluded from market-level aggregation to reduce the influence of anomalous observations.

### 3. Market-Level Feature Engineering

Individual stock observations were aggregated into daily market indicators.

Eight features were selected for regime discovery:

| Feature             | Description                                                |
| ------------------- | ---------------------------------------------------------- |
| `Market_Return`     | Daily median stock return                                  |
| `Market_Volatility` | Cross-sectional return volatility                          |
| `Market_Breadth`    | Relative difference between advancing and declining stocks |
| `Return_5D`         | Five-day cumulative market return                          |
| `Return_20D`        | Twenty-day cumulative market return                        |
| `Volatility_5D`     | Five-day rolling volatility                                |
| `Volatility_20D`    | Twenty-day rolling volatility                              |
| `Volume_Relative`   | Daily volume relative to its 20-day moving average         |

A minimum daily coverage threshold of **50 stocks** was applied before regime modeling.

### 4. Regime Discovery with K-Means

The market data was divided chronologically into:

* **70% Training**
* **15% Validation**
* **15% Test**

Standardization was fitted **only on the training data**.

K-Means was evaluated for `K = 2` through `K = 6` using the training set. The best silhouette score was obtained with **K = 3**.

The final K-Means model was therefore trained with three clusters.

The cluster characteristics resulted in the following descriptive interpretation:

| Regime | Interpretation     | General Characteristics                                 |
| ------ | ------------------ | ------------------------------------------------------- |
| 0      | Bull / Expansion   | Positive returns, positive breadth, higher activity     |
| 1      | Neutral / Stable   | Lower volatility and relatively balanced conditions     |
| 2      | Bear / Contraction | Negative returns, negative breadth, elevated volatility |

The numerical cluster IDs are arbitrary; the descriptive labels are based on the characteristics of each cluster.

### 5. Next-Day Regime Prediction

The target was defined as the **next trading day's K-Means regime**.

The prediction problem was evaluated chronologically to avoid using future observations during training.

### 6. XGBoost

An XGBoost multiclass classifier was trained using the eight market features.

Class-balanced sample weights were used during training because the discovered regimes were not equally represented.

The selected configuration was:

* `n_estimators = 300`
* `max_depth = 5`
* `learning_rate = 0.05`
* `subsample = 0.8`
* `colsample_bytree = 0.8`
* `random_state = 42`

Macro F1 was used as the primary model-selection metric because the project aims to evaluate performance across all regimes rather than relying only on the majority class.

## Model Evaluation

Five XGBoost configurations were compared using the validation set.

The baseline configuration achieved the highest validation Macro F1 among the tested configurations and was selected for final testing.

### Final Results

| Model       | Validation Accuracy | Validation Macro F1 | Test Accuracy | Test Macro F1 |
| ----------- | ------------------: | ------------------: | ------------: | ------------: |
| Persistence |              69.22% |              0.5327 |    **94.55%** |    **0.5669** |
| XGBoost     |              68.99% |          **0.5361** |        93.50% |        0.4876 |

### Test Performance

XGBoost achieved:

* **Accuracy:** 93.50%
* **Macro F1:** 0.4876

Persistence achieved:

* **Accuracy:** 94.55%
* **Macro F1:** 0.5669

The XGBoost model therefore did **not** outperform the persistence baseline on the final out-of-sample test period.

## Key Findings

The experiment shows that market regimes in the DSE exhibit strong temporal persistence.

Although XGBoost slightly improved validation Macro F1 compared with persistence, this improvement did not carry over to the final test period.

The test period was also highly imbalanced, with approximately **94.9% of observations belonging to the Neutral regime**. Consequently, the high XGBoost test accuracy should not be interpreted as strong prediction across all three regimes.

The results demonstrate the importance of comparing machine learning models against simple temporal baselines in financial regime prediction.

## Feature Importance

The most influential features in the selected XGBoost model were:

1. `Market_Volatility`
2. `Volatility_5D`
3. `Volatility_20D`
4. `Return_20D`
5. `Return_5D`
6. `Market_Return`
7. `Market_Breadth`
8. `Volume_Relative`

Volatility-related variables were particularly influential in distinguishing the regimes.

## Limitations

* The discovered regimes depend on the selected market features and K-Means configuration.
* Fixed training-period cluster centroids may not represent later market conditions equally well.
* The test period contains a highly imbalanced distribution of regimes.
* The current feature set focuses on aggregate market indicators and does not include richer temporal transition features.
* The persistence baseline is difficult to outperform because regime labels exhibit strong temporal persistence.
* The results should not be interpreted as investment advice or a trading strategy.

## Future Improvements

Potential extensions include:

* Adding richer lagged and transition features
* Investigating regime transition probabilities
* Testing alternative clustering algorithms
* Exploring Hidden Markov Models and other sequential models
* Evaluating longer forecasting horizons
* Testing additional market indicators
* Investigating rolling or adaptive regime models
* Comparing additional machine learning architectures

## Technologies

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib
* Seaborn
* Google Colab
* Jupyter Notebook

## Project Structure

```text
DSE-RegimeLens/
│
├── DSE_RegimeLens.ipynb
└── README.md
```

## Disclaimer

This project is intended for educational and research purposes. It does not provide financial advice, investment recommendations, or guaranteed market predictions.
