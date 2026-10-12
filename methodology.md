# Methodology: DSE Stock-Movement Regime Classification

## 1. Refined research question
**Can historical price- and volume-derived features classify the next five-observation movement of frequently observed Dhaka Stock Exchange (DSE) stocks into bullish, neutral, and bearish classes?**

This is supervised classification. It tests whether basic technical features contain useful out-of-sample information; it does not claim to predict the DSE index or establish a profitable trading strategy.

## 2. Dataset description
- **Dataset:** Dhaka Stock Exchange Historical Data (1999–2025), provided as a CSV.
- **Expected raw fields:** `Trading Code`, `Date`, `Open`, `High`, `Low`, `Close`, `Volume`.
- **Observation unit:** one stock (trading code) on one date.
- **Raw size:** previously described as about 1.5 million rows and seven columns; exact size is checked when the notebook runs.
- **Features:** 1-day, 5-day and 20-day returns; 5-day rolling volatility; close relative to 5-day and 20-day moving averages; 5-day average volume relative to 20-day average volume.
- **Target:** five-observation forward return within the same ticker. Above +2% = `bullish`; below −2% = `bearish`; otherwise = `neutral`.
- **Practical subset:** the notebook selects the 50 trading codes with the most valid observations to keep runtime manageable. Results therefore do not represent every DSE security.
- **Limitations:** possible corporate-action effects, suspensions, missing dates, outliers, survivorship/coverage bias; no fundamentals, news, macroeconomic variables, transaction costs, or full trading simulation.

## 3. Data cleaning plan
1. Normalize column names and map common variants to expected fields.
2. Parse dates and convert OHLCV fields to numeric.
3. Remove rows with missing ticker/date/close, non-positive prices, and duplicate ticker-date pairs.
4. Remove rows where high is below low.
5. Sort by ticker and date before computing features.
6. Select the 50 tickers with the most observations for feasible runtime.
7. Drop rows where required rolling features or the five-observation future target are unavailable.

## 4. Feature engineering
Within each ticker, calculate daily return, 5-day return, 20-day return, 5-day rolling return volatility, close/MA5 minus one, close/MA20 minus one, and MA5 volume/MA20 volume minus one. Calculate the future five-observation return by shifting close backward within each ticker, and use it only to form the target—not as a predictor. Rolling predictors use current and past observations only. Split by date chronologically, with the earliest 80% of dates for training and the latest 20% for testing.

## 5. Models
1. **Multinomial Logistic Regression:** fast, interpretable baseline. Standardization is fitted on training data through a pipeline.
2. **Random Forest Classifier:** nonlinear tree ensemble that can model feature interactions and does not require standardized features.

Both models use the same features and chronological test set.

## 6. Evaluation metrics
- **Accuracy:** overall fraction of correct predictions, but may hide class imbalance.
- **Macro F1-score:** weights each class equally and reveals performance on less common classes.
- **Balanced accuracy:** averages recall across classes.
- **Confusion matrix/classification report:** show class-wise errors, precision, recall, and F1.

The held-out period is later in time than training. Metrics describe this test period only and do not demonstrate financial profitability.
