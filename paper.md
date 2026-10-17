# DSE-RegimeLens: Classifying Bullish, Neutral, and Bearish Market Regimes in the Dhaka Stock Exchange

## Abstract

This study investigates whether historical price- and volume-derived features can classify future market movements of Dhaka Stock Exchange (DSE) stocks into bullish, neutral, and bearish regimes. The experiment uses historical OHLCV data and evaluates a machine-learning classifier against a persistence baseline. The final test set contains 862 observations. The main model achieved 93.50% accuracy and a macro F1-score of 0.4876. However, the persistence baseline achieved 94.55% accuracy and a higher macro F1-score of 0.5669. The test set was strongly imbalanced: 818 of 862 observations belonged to the neutral class, while only 30 were bullish and 14 were bearish. These results show that accuracy alone can give a misleading impression of predictive performance. The main model did not outperform the baseline, and its recognition of bullish and bearish observations remained weak. This experiment provides a starting point for evaluating market-regime classification in the DSE and highlights the importance of class imbalance, baseline comparisons, and robust evaluation.

## 1. Introduction

Financial market movements are difficult to predict because prices and trading volumes can change in response to many factors. Machine-learning methods can identify patterns in historical data, but strong evaluation is necessary to determine whether those patterns provide useful predictive information.

The Dhaka Stock Exchange (DSE) provides an important setting for studying market behaviour in Bangladesh. This project asks the following research question:

**Can historical price- and volume-derived features classify the next five-observation movement of DSE stocks into bullish, neutral, and bearish classes?**

Previous research has explored machine learning for financial prediction and asset pricing. Gu, Kelly, and Xiu (2020) examined the use of machine-learning methods in empirical asset pricing, demonstrating the relevance of systematic model evaluation in financial research. Research on the DSE also motivates investigating local-market data rather than assuming that findings from other markets will transfer directly.

This study evaluates a classification model using historical stock observations and compares it with a persistence baseline. The goal is not to claim that the model is ready for trading, but to examine its performance and identify limitations that should guide future experiments.

## 2. Methodology

### 2.1 Dataset

The project uses historical DSE data containing the fields Trading_Code, Date, Open, High, Low, Close, and Volume. The dataset examined in the notebook contains 1,523,921 rows and seven columns, covering 2 January 1999 to 8 April 2025, with 534 distinct trading codes before subsequent filtering.

The notebook's initial data-quality checks identified duplicate stock-date records, invalid OHLC observations, non-positive prices, and two missing volume values. These issues matter because repeated or invalid observations can affect feature calculation and evaluation. The exact impact of each cleaning operation should be interpreted according to the executed notebook.

### 2.2 Features and target

The project investigates price- and volume-derived information, including returns over different observation windows, rolling volatility, closing-price relationships to moving averages, and relative trading volume. Such features aim to represent recent price direction, variability, and trading activity.

The intended prediction target has three classes: bullish, neutral, and bearish, based on the movement over the next five observations. The project design uses thresholds of above +2% for bullish and below −2% for bearish, with movements between those thresholds classified as neutral.

### 2.3 Evaluation

The experiment evaluates predictions on a test set of 862 observations. Accuracy is reported alongside macro F1 because the class distribution is imbalanced. Macro F1 gives each class equal weight when averaging class-level F1 scores, making it more informative than accuracy alone when minority classes are important.

The main model is compared with a persistence baseline. This comparison helps determine whether the machine-learning approach improves on a simpler reference method. The reported results are descriptive of this experiment and do not establish future trading profitability.

## 3. Results

### Table 1. Test-set performance comparison

| Evaluation metric | Main model | Persistence baseline |
|---|---:|---:|
| Accuracy | 0.9350 | 0.9455 |
| Macro F1-score | 0.4876 | 0.5669 |

The persistence baseline outperformed the main model on both reported metrics. The main model achieved high overall accuracy, but its macro F1-score was substantially lower. This difference indicates that aggregate accuracy does not adequately describe performance across all three classes.

### Table 2. Main model classification report

| Class | Precision | Recall | F1-score | Support |
|---|---:|---:|---:|---:|
| Bullish | 0.2500 | 0.2667 | 0.2581 | 30 |
| Neutral | 0.9815 | 0.9707 | 0.9760 | 818 |
| Bearish | 0.1905 | 0.2857 | 0.2286 | 14 |
| Macro average | 0.4740 | 0.5077 | 0.4876 | 862 |
| Weighted average | 0.9432 | 0.9350 | 0.9389 | 862 |

The model performed much better on neutral observations than on bullish and bearish observations. Its F1-scores for bullish and bearish classes were 0.2581 and 0.2286, respectively. These minority-class results are important because the research question concerns all three market regimes, not only the dominant neutral class.

### Table 3. Main model confusion matrix

Rows represent actual classes and columns represent predicted classes. Class order is Bullish, Neutral, Bearish.

| Actual \ Predicted | Bullish | Neutral | Bearish |
|---|---:|---:|---:|
| Bullish | 8 | 11 | 11 |
| Neutral | 18 | 794 | 6 |
| Bearish | 6 | 4 | 4 |

The confusion matrix shows that the model correctly classified 794 neutral observations. However, it correctly classified only 8 bullish observations and 4 bearish observations. Many non-neutral observations were incorrectly assigned to another class, indicating that detecting directional market movements remains challenging.

## 4. Discussion

The results do not support the claim that the main model is better than the persistence baseline in this experiment. Although the main model achieved 93.50% accuracy, the baseline reached 94.55% accuracy and a higher macro F1-score. Therefore, the model's overall accuracy should not be interpreted as evidence of superior predictive performance.

The main limitation is class imbalance. Neutral observations account for 818 of the 862 test samples, while bullish and bearish observations account for only 30 and 14 samples, respectively. Strong performance on the neutral class therefore contributes heavily to overall accuracy. The weak bullish and bearish F1-scores show that performance on the less frequent classes needs improvement.

Data quality is another consideration. The notebook identified duplicate stock-date records, invalid OHLC observations, non-positive prices, and missing volume values during initial checks. Future work should document each cleaning decision and verify that rolling features and forward targets are calculated without leakage across dates or stocks.

Further experiments could compare additional baseline and machine-learning models, use class-weighted training, examine alternative target thresholds, and report per-class metrics across multiple chronological test periods. Any such changes should be evaluated on data that was not used to select the model or its parameters. Transaction costs and trading feasibility would also need separate analysis before drawing conclusions about practical investment use.

## 5. Conclusion

This study evaluated three-class market-regime classification for historical DSE stock observations using price- and volume-derived information. The main model achieved 93.50% test accuracy and a macro F1-score of 0.4876, while the persistence baseline performed better with 94.55% accuracy and a macro F1-score of 0.5669. The large neutral-class majority and weak bullish and bearish performance show why accuracy alone is insufficient. The findings do not establish that the model can reliably predict market direction or generate profitable trades. Future work should prioritize class imbalance, leakage-safe evaluation, transparent data cleaning, and stronger comparisons against simple baselines.

## References

1. Gu, S., Kelly, B., & Xiu, D. (2020). Empirical asset pricing via machine learning. *The Review of Financial Studies, 33*(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009

2. David, M. (2019). Research on financial prediction using machine-learning methods. https://doi.org/10.3233/AF-190900

3. *An Interpretable Machine Learning Framework for Predicting Next-Day Firm-Level Market Stress in the Dhaka Stock Exchange*. (2026). *Discover AI*. https://link.springer.com/article/10.1007/s44163-026-02065-7
