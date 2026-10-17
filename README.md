# DSE-RegimeLens: Classifying Market Regimes in the Dhaka Stock Exchange

**DSE-RegimeLens** is a machine learning project that investigates the classification of bullish, neutral, and bearish market regimes in the Dhaka Stock Exchange (DSE) using historical stock price and trading volume data.

The project evaluates a three-class classification approach and compares its performance against a persistence baseline, with particular attention to class imbalance and minority-class prediction.

## Research Objective

Can historical price and volume features classify the market's future movement into bullish, neutral, and bearish regimes over the next five observations?

## Dataset

- **Source:** Dhaka Stock Exchange Historical Data (1999–2025)
- **Original records:** 1,523,921
- **Original columns:** 7
- **Trading codes:** 534 before filtering
- **Date range:** January 1999 – April 2025
- **Data type:** Historical OHLCV data

The dataset includes trading code, date, open, high, low, close, and volume.

## Methodology

The project workflow includes:

1. Data inspection and cleaning
2. Feature engineering using historical returns, rolling volatility, moving-average relationships, and relative volume
3. Construction of bullish, neutral, and bearish target labels
4. Model evaluation using a chronological test split
5. Comparison against a persistence baseline
6. Analysis of class imbalance and classification errors

The target labels are based on predefined positive and negative movement thresholds of 2%. See the paper and implementation for the exact target construction.

## Results

Evaluation on **862 test observations** produced the following results:

| Metric | Main Model | Persistence Baseline |
|---|---:|---:|
| Accuracy | 93.50% | 94.55% |
| Macro F1-score | 0.4876 | 0.5669 |

Although the main model achieved 93.50% accuracy, it did not outperform the persistence baseline.

The test set was heavily imbalanced, with 818 neutral, 30 bullish, and 14 bearish observations. The results highlight why accuracy alone can be misleading in imbalanced financial classification tasks.

**Key finding:** The baseline outperformed the main model on both accuracy and macro F1-score. The results do not establish a profitable trading strategy.

## Research Paper

Read the full research paper:

- [DSE-RegimeLens Research Paper](paper.md)

## Presentation

- [View Presentation (PDF)](DSE-RegimeLens_Presentation.pdf)
- [Download PowerPoint (PPTX)](DSE-RegimeLens_Presentation.pptx)

*The presentation links will work after the corresponding files have been uploaded to this repository using these exact filenames.*

## Limitations

- Strong class imbalance, particularly for bullish and bearish regimes
- Limited predictive performance for minority classes
- The persistence baseline outperformed the main model
- Classification results do not directly measure trading profitability
- Further validation is needed across multiple chronological test periods

## Future Work

- Explore class weighting and resampling methods
- Investigate alternative target thresholds
- Evaluate additional machine learning models
- Conduct multi-period chronological validation
- Report per-class performance and confusion matrices
- Evaluate potential trading strategies with transaction costs and realistic assumptions

## References

1. Gu, S., Kelly, B., & Xiu, D. (2020). *Empirical asset pricing via machine learning*. The Review of Financial Studies, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009

2. David, M. (2019). *Research on financial prediction using machine-learning methods*. https://doi.org/10.3233/AF-190900

3. *An Interpretable Machine Learning Framework for Predicting Next-Day Firm-Level Market Stress in the Dhaka Stock Exchange*. (2026). Discover AI. https://link.springer.com/article/10.1007/s44163-026-02065-7

