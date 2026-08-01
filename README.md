USD-NGN-REGIME-FORECASTING
[![License](https://shields.io)](https://opensource.org)

### Baseline Model Formulation & Validation Performance (Linear Regression)

To establish a formal predictive benchmark for the USD/NGN daily log returns forecast, a baseline Ordinary Least Squares (OLS) Linear Regression model was executed. This baseline serves as our quantitative floor.

#### Validation Strategy & Experiment Architecture
* **Notebook Context:** Executed within `notebook/03_forecasting_models.ipynb`
* **Data Partitioning:** Chronological split (80% Train / 20% Validation) to completely eliminate look-ahead bias.
* **Training Window:** 2,382 trading days (2015 through early April 2024).
* **Validation Window:** 596 trading days (April 3, 2024, through mid-2026), capturing the modern unified float era.

#### Quantitative Performance Metrics

| Metric | Baseline Score (Linear Regression) | Target Benchmark |
| :--- | :--- | :--- |
| **Mean Absolute Error (MAE)** | **0.005091** | Lower is better |
| **Root Mean Squared Error (RMSE)** | **0.011616** | Lower is better |
| **Directional Accuracy (%)** | **46.48%** | > 50.00% (Random Chance) |

#### Structural Insights from Feature Weights:
* **Volatility Domination:** The feature `Realized_Var_Weekly` returned a massive coefficient of **0.693699**, mathematically validating that variance memory and conditional volatility clustering represent the primary signals captured by the baseline.
* **Short-Term Dynamics:** `Lag_1` exhibited a significant negative coefficient (**-0.107109**), capturing a strong daily mean-reversion tendency within the series.
* **Linear Limitation:** The `Regime` feature returned a negligible coefficient (**-0.000178**) due to OLS's inability to interpret arbitrary integer step-functions as non-linear context switches. This establishes a clear logical threshold for transitioning to tree-based ensemble architectures.

├── data/                  # Raw and processed yfinance extracts
├── notebooks/
│   ├── 01_eda_and_structural_breaks.ipynb
│   ├── 02_regime_detection_ruptures.ipynb
│   └── 03_forecasting_models.ipynb
├── src/                   # Modular pipeline code
│   ├── data_processing.py
│   └── features.py
├── LICENSE
├── NOTICE
├── README.md              # The deep dive explanation of the macro context
└── requirements.txt



## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) and [NOTICE](NOTICE) files for details.
