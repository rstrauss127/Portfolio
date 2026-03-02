# Election Cycle Market Analysis (LSTM Forecasting)

This project uses deep learning (LSTM time-series models) to predict **closing prices** for major market assets during a U.S. presidential election window. The core motivation was to test whether “unusual historical eras” (like a major election cycle) show predictable structure that challenges a strict interpretation of the Efficient Market Hypothesis (EMH).

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
