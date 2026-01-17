# Crypto Technical Analysis Toolkit
A lightweight Python toolkit for fetching cryptocurrency price data from CoinGecko and visualizing a wide range of technical indicators on candlestick charts. All code is contained in a single Jupyter notebook (Crypto_Tech_Analysis.ipynb) and can be used as a reference.

## Overview
The notebook demonstrates how to:

1. Retrieve OHLC (Open‑High‑Low‑Close) data for any CoinGecko asset in any fiat or crypto currency.
2. Compute common technical indicators:
- Simple Moving Average (SMA)
- Exponential Moving Average (EMA)
- Bollinger Bands
- Relative Strength Index (RSI)
- Moving Average Convergence Divergence (MACD)
- Bullish Engulfing pattern
3. Visualise the data and indicators using Plotly candlestick charts with multiple sub‑plots.

The code is written in pure Python and relies on the following libraries:

- `pandas` – data manipulation
- `requests` – HTTP requests to CoinGecko
- `plotly` – interactive visualisation
- `plotly.subplots` – for multi‑panel charts

## Features

| Indicator | Description | Plotting |
|---------|------------|----------|
| SMA | Simple moving average of closing prices | Candlestick + SMA line |
| EMA | Exponential moving average of closing prices | Candlestick + EMA line |
| Bollinger Bands | Upper, middle, and lower bands around a moving average | Candlestick + bands |
| RSI | Momentum oscillator (0–100) | Candlestick + RSI panel |
| MACD | Difference of two EMAs + signal line + histogram | Candlestick + RSI + MACD panels |
| Bullish Engulfing | Pattern detection for potential bullish reversal | Candlestick + markers |
| Custom SMA/EMA | User-defined window lengths | Candlestick + custom SMA/EMA |
| Combined Plots | Multi-panel charts (e.g., Candlestick + RSI + MACD) | 3-panel sub-plots |

## Installation

```
# Clone the repo
git clone https://github.com/<your-username>/crypto-technical-analysis.git
cd crypto-technical-analysis

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install dependencies
pip install pandas
pip install plotly
```

## Usage

1. Fetch OHLC data

```
df = get_ohlc_data(
    coin_id='bitcoin',          # CoinGecko ID
    target_curr='usd',          # Currency to quote against
    days='180',                 # Number of days (or 'max')
    precision='2'               # Decimal places for prices
)
```

The returned DataFrame contains:

| Column | Meaning |
|--------|---------|
| timestamp | Unix epoch (ms) |
| open | Opening price |
| high | Highest price |
| low | Lowest price |
| close | Closing price |
| volume | Trading volume |

2. Compute indicators

```
df = add_sma(df, window=20)          # Simple Moving Average
df = add_ema(df, window=20)          # Exponential Moving Average
df = add_bollinger_bands(df, window=20)
df = add_rsi(df, window=14)
df = add_macd(df)
df = add_bullish_engulfing(df)
```

Each function adds a new column to the DataFrame with the indicator values.

3. Plotting

All plotting functions return a Plotly figure and display it inline.

```
plot_candlestick_sma(df, 'usd')
plot_candlestick_ema(df, 'usd')
plot_candlestick_bollinger(df, 'usd')
plot_candlestick_rsi(df, 'usd')
plot_candlestick_macd(df, 'usd')
plot_candlestick_bullish_engulf(df, 'usd')
```

For multi-panel charts:

```
plot_candlestick_rsi_macd('bitcoin', 'usd', 180, '2')
```

| Example | Description |
|--------|-------------|
| plot_candlestick_sma | Candlestick chart with 20-day SMA |
| plot_candlestick_ema | Candlestick chart with 20-day EMA |
| plot_candlestick_boll_bands | Candlestick chart with Bollinger Bands |
| plot_candlestick_rsi_macd | 3-panel chart: Candlestick, RSI, MACD |
| plot_candlestick_bullish_engulf | Candlestick chart highlighting bullish engulfing patterns |

Run the notebook to see interactive visualizations.

## Contributing

Feel free to fork the repository, create a feature branch, and submit a pull request.

Please adhere to the following guidelines:

- Keep functions small and focused.
- Add docstrings and type hints where appropriate.
- Update the README if you add new indicators or visualizations.

## License

This project is licensed under the MIT License – see the LICENSE file for details.