
# DSE Stock-Movement Regime Classification

## Overview

This project investigates whether historical price and trading-volume data can be used to classify future price movements of individual stocks listed on the Dhaka Stock Exchange (DSE).

The study uses historical OHLCV data and machine learning models to classify stock movements into three categories: bullish, neutral, and bearish.

## Research Objective

To evaluate whether price- and volume-derived features can classify the five-trading-observation-ahead movement of frequently observed DSE stocks.

## Dataset

The dataset contains historical stock-level trading information:

- Trading Code
- Date
- Open
- High
- Low
- Close
- Volume

For computational efficiency, the experiment selects the 50 trading codes with the most observations.

## Methodology

The workflow includes:

1. Data cleaning and preprocessing
2. Feature engineering using historical prices and trading volume
3. Three-class target construction using five-observation forward returns
4. Chronological training and testing split
5. Training Logistic Regression and Random Forest models
6. Model evaluation using accuracy, macro F1-score, balanced accuracy, classification reports, and confusion matrices

### Target Classes

- **Bullish:** Forward return above +2%
- **Bearish:** Forward return below -2%
- **Neutral:** Forward return between -2% and +2%, inclusive

## Repository Structure

```text
DSE-RegimeLens/
├── README.md
├── DSE_RegimeLens.ipynb
├── literature_review.md
├── methodology.md
└── experiment.ipynb
```

## Tools and Technologies

- Python
- Pandas and NumPy
- Scikit-learn
- Matplotlib and Seaborn
- Google Colab
- Jupyter Notebook

## Limitations

The results depend on historical data quality, selected stocks, engineered features, and target thresholds. This experiment classifies individual-stock movements; it does not predict the DSE index and is not investment advice.
