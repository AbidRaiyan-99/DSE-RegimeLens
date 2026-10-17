<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DSE-RegimeLens Research Paper</title>
  <style>
    body {
      max-width: 900px;
      margin: 40px auto;
      padding: 0 24px;
      font-family: "Times New Roman", serif;
      font-size: 12pt;
      line-height: 1.8;
      color: #222;
      background: #fff;
    }

    h1, h2, h3 {
      text-align: left;
    }

    p {
      text-align: justify;
      text-justify: inter-word;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin: 20px 0;
      font-size: 11pt;
    }

    th, td {
      border: 1px solid #999;
      padding: 8px;
      text-align: left;
    }

    th {
      background: #eee;
    }

    a {
      overflow-wrap: anywhere;
    }

    @media (max-width: 600px) {
      body {
        margin: 20px auto;
        padding: 0 14px;
      }
    }
  </style>
</head>
<body>

  <h1>DSE-RegimeLens: Classifying Bullish, Neutral, and Bearish Market Regimes in the Dhaka Stock Exchange</h1>

  <h2>Abstract</h2>

  <p>
    This study investigates whether historical price- and volume-derived
    features can classify future market movements of Dhaka Stock Exchange
    (DSE) stocks into bullish, neutral, and bearish regimes. The experiment
    uses historical OHLCV data and evaluates a machine-learning classifier
    against a persistence baseline. The final test set contains 862
    observations. The main model achieved 93.50% accuracy and a macro
    F1-score of 0.4876. However, the persistence baseline achieved 94.55%
    accuracy and a higher macro F1-score of 0.5669.
  </p>

  <p>
    The test set was strongly imbalanced: 818 of 862 observations belonged
    to the neutral class, while only 30 were bullish and 14 were bearish.
    These results show that accuracy alone can give a misleading impression
    of predictive performance. The main model did not outperform the
    baseline, and its recognition of bullish and bearish observations
    remained weak.
  </p>

  <h2>1. Introduction</h2>

  <p>
    Financial market movements are difficult to predict because prices and
    trading volumes can change in response to many factors. Machine-learning
    methods can identify patterns in historical data, but strong evaluation
    is necessary to determine whether those patterns provide useful
    predictive information.
  </p>

  <p>
    The Dhaka Stock Exchange (DSE) provides an important setting for
    studying market behaviour in Bangladesh. This project asks whether
    historical price- and volume-derived features can classify the next
    five-observation movement of DSE stocks into bullish, neutral, and
    bearish classes.
  </p>

  <h2>2. Methodology</h2>

  <h3>2.1 Dataset</h3>

  <p>
    The project uses historical DSE data containing Trading_Code, Date,
    Open, High, Low, Close, and Volume. The dataset examined in the notebook
    contains 1,523,921 rows and seven columns, covering 2 January 1999 to
    8 April 2025, with 534 distinct trading codes before subsequent
    filtering.
  </p>

  <h3>2.2 Features and target</h3>

  <p>
    The project investigates price- and volume-derived information,
    including returns over different observation windows, rolling
    volatility, closing-price relationships to moving averages, and
    relative trading volume. The intended prediction target has three
    classes: bullish, neutral, and bearish, based on movement over the
    next five observations.
  </p>

  <h2>3. Results</h2>

  <h3>Table 1. Test-set performance comparison</h3>

  <table>
    <thead>
      <tr>
        <th>Evaluation metric</th>
        <th>Main model</th>
        <th>Persistence baseline</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Accuracy</td>
        <td>0.9350</td>
        <td>0.9455</td>
      </tr>
      <tr>
        <td>Macro F1-score</td>
        <td>0.4876</td>
        <td>0.5669</td>
      </tr>
    </tbody>
  </table>

  <p>
    The persistence baseline outperformed the main model on both reported
    metrics. The main model achieved high overall accuracy, but its macro
    F1-score was substantially lower.
  </p>

  <h2>4. Discussion</h2>

  <p>
    The results do not support the claim that the main model is better than
    the persistence baseline in this experiment. Although the main model
    achieved 93.50% accuracy, the baseline reached 94.55% accuracy and a
    higher macro F1-score.
  </p>

  <h2>5. Conclusion</h2>

  <p>
    This study evaluated three-class market-regime classification for
    historical DSE stock observations using price- and volume-derived
    information. The findings do not establish that the model can reliably
    predict market direction or generate profitable trades.
  </p>

  <h2>References</h2>

  <ol>
    <li>
      Gu, S., Kelly, B., &amp; Xiu, D. (2020).
      Empirical asset pricing via machine learning.
      <i>The Review of Financial Studies, 33</i>(5), 2223–2273.
      <a href="https://doi.org/10.1093/rfs/hhaa009">
        https://doi.org/10.1093/rfs/hhaa009
      </a>
    </li>
    <li>
      David, M. (2019). Research on financial prediction using
      machine-learning methods.
      <a href="https://doi.org/10.3233/AF-190900">
        https://doi.org/10.3233/AF-190900
      </a>
    </li>
    <li>
      An Interpretable Machine Learning Framework for Predicting Next-Day
      Firm-Level Market Stress in the Dhaka Stock Exchange (2026).
      <i>Discover AI</i>.
      <a href="https://link.springer.com/article/10.1007/s44163-026-02065-7">
        Read publication
      </a>
    </li>
  </ol>

</body>
</html>
