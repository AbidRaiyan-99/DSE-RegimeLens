# Literature Review: DSE Stock-Movement Regime Classification

## 1. An Interpretable Machine Learning Framework for Predicting Next-Day Firm-Level Market Stress in the Dhaka Stock Exchange
**Source:** *Discover Artificial Intelligence* (2026). https://link.springer.com/article/10.1007/s44163-026-02065-7

This study focuses directly on the Dhaka Stock Exchange and examines how machine-learning methods can identify levels of market stress from firm-level market data. It is relevant because it frames DSE market behavior as a classification problem and compares a linear baseline with flexible models such as Random Forest and XGBoost. This assignment is a smaller educational experiment and does not claim to reproduce the paper.

## 2. Information Leakage in Financial Machine Learning Research
**Source:** David, Z. (2019). https://doi.org/10.3233/AF-190900

This article explains how future information can leak into training or evaluation data, especially when financial time series are randomly split. Such leakage can make model performance look better than it would be in a real forecasting setting. This motivates a chronological train-test split and past-only rolling features.

## 3. Empirical Asset Pricing via Machine Learning
**Source:** Gu, S., Kelly, B., & Xiu, D. (2020). *The Review of Financial Studies*, 33(5), 2223–2273. https://doi.org/10.1093/rfs/hhaa009

Gu, Kelly, and Xiu study how machine learning can be applied to financial return prediction and compare methods that capture different relationships in financial data. Their work supports evaluating multiple models on out-of-sample data rather than relying on a single algorithm. This project is a compact DSE classification experiment, not a replication of their asset-pricing study.

## 4. Leakage-Aware ML Comparison for Next-Day Stock-Return Prediction
**Source:** Public reproducibility project. https://github.com/hameedsoyemi/ml-stock-return-prediction

This project demonstrates a practical workflow using lagged features, chronological splitting, and preprocessing fitted on training data only. It highlights why feature timing must be explicit and future prices must not enter predictors. These practices inform the feature-engineering and evaluation design here.

## 5. Machine Learning in Stock Market Forecasting: A Comprehensive Review
**Source:** *Discover Computing* (2026). https://link.springer.com/article/10.1007/s10791-026-10491-5

This review surveys machine-learning and deep-learning methods used in financial forecasting and notes that results are hard to compare when studies use different targets, horizons, datasets, and metrics. It supports defining the prediction horizon and target clearly and reporting more than accuracy alone. This project therefore reports macro F1 and balanced accuracy alongside accuracy.

## Overall takeaway

The sources suggest three principles: define the target precisely, compare a simple baseline with a more flexible model, and preserve time order to reduce information leakage. This is an educational experiment, not investment advice.
