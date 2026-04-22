# A Study on S&P 500 Predictability using Classification Models

## Objective
This project investigates whether short-term predictability exists in the S&P 500 using machine learning classification models. The goal is to identify periods where returns are both directional and sufficiently large to be considered predictable.

## Data
- Source: Yahoo Finance (SPY ETF)
- Period: 2005–2025
- Frequency: Daily data
- Variables: Price, volume, and derived features

## Target Definition
The target is designed to capture **economically meaningful predictability**:

- Positive return the next day
- Absolute return above a rolling volatility threshold (60th percentile)

This avoids trivial predictions of small, noisy movements.

## Feature Engineering
A wide set of features is constructed to capture different market dynamics:

- Autocorrelation (lags 1–5)
- Higher moments (skewness, kurtosis)
- Realized volatility
- Price range
- Volume changes
- Rolling entropy
- RSI (momentum proxy)
- Distance from 200-day moving average

All features are lagged to prevent look-ahead bias.

## Models
Three models are implemented:

- Logistic Regression (baseline)
- Random Forest
- Gradient Boosting

Evaluation is performed using **TimeSeriesSplit cross-validation** and **ROC-AUC**.

## Results (Model Performance)

- Logistic Regression: ~0.61 ROC-AUC  
- Random Forest: ~0.62 ROC-AUC  
- Gradient Boosting: ~0.60 ROC-AUC  

Results suggest **weak but non-random predictive signal**.

## Strategy Construction
A trading strategy is built using:

- Calibrated probabilities
- Dynamic threshold (85th percentile)
- Additional RSI filter to avoid overbought conditions

## Backtesting

### In-Sample
- Strategy Sharpe: ~0.50  
- Buy & Hold Sharpe: ~0.78  

### Walk-Forward (Out-of-Sample)
- Strategy Sharpe: ~0.38  
- Includes transaction costs

## Key Insight
While some predictive structure exists, it is **not strong enough to outperform a simple buy-and-hold strategy** after realistic constraints.

This highlights the difficulty of extracting robust signals from financial time series.

## Tools & Libraries
- Python
- NumPy, Pandas
- scikit-learn
- yfinance
- matplotlib

## Disclaimer
This project is for research and educational purposes only and does not constitute financial advice.
## Notes
This project focuses on predictability analysis rather than alpha generation. It emphasizes robustness, proper validation, and avoidance of look-ahead bias.
