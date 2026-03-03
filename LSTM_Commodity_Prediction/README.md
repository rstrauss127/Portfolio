# Election Cycle Market Analysis (LSTM Forecasting)

This project uses deep learning (LSTM time-series models) to predict **closing prices** for major market assets during a U.S. presidential election window. The motivation was to test whether “unusual historical eras” (like a major election cycle) show predictable structure that challenges a strict interpretation of the Efficient Market Hypothesis (EMH).

## Goal
Predict closing prices for:
- Oil (WTI futures)
- Gold (Gold futures)
- S&P 500
- Chevron (CVX)
- IBM

## Data
- **Source:** `yfinance` API for historical daily closing prices
- **Time period:** Jan 1984 → Jan 2024
- **Forecast focus window:** Election Day 2024 → Inauguration Day 2025
- **Target:** next-day closing price (iterated forward for multi-step forecasting)

## Methodology (high level)
1. Fetch historical data using the `yfinance` API, then clean/format it.
2. Scale the time series and build a **rolling 60-day window** per training sample.
3. Train a separate LSTM model for each asset.
4. Generate predictions for the election-window horizon (Nov 2024 → Jan 2025) using **recursive multi-step forecasting**.
5. Continue collecting daily closes to evaluate and refine post-election performance.

## Model
**Architecture (core LSTM):**
- Input: past **60 days** of prices (windowed sequence)
- LSTM(50, return_sequences=True) → Dropout(0.2)
- LSTM(50, return_sequences=False) → Dropout(0.2)
- Dense(1) output

**Why this setup:**
- LSTMs capture long/short-term temporal dependencies in sequential data.
- Dropout helps reduce overfitting on noisy financial series.
- MSE is appropriate for regression on continuous values like price.

## Results (examples)
The presentation includes example comparisons of actual vs predicted prices for early December 2024 across:
- Oil
- Gold
- S&P 500
- Chevron
- IBM

Key takeaway: recursive LSTM forecasting can track short horizons, but performance is sensitive to regime shifts (e.g., recent “bull market” behavior differs from older historical periods). In this project, using a shorter historical window (e.g., the last ~6 months) was observed to be more effective than training on decades of data.
