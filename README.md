# Mean Reversion Strategy with Markowitz Allocator

## Overview
This repository contains a quantitative trading pipeline developed for the YAP-471 Computational Finance course. The project builds a systematic investment strategy focusing on 6 large-cap tech stocks (AAPL, MSFT, AMZN, GOOGL, TSLA, NVDA) over a 5-year historical period. It aims to exploit short-term market overreactions (oversold/overbought conditions) using a mean-reversion signal and optimally allocates capital using a dynamically updated Markowitz model.

## Pipeline Modules
* **Data Module:** Automatically fetches and cleans daily historical prices using the Stooq API. Handles missing data via forward/backward filling to create a robust financial time series.
* **Signal Module:** Calculates a 20-day rolling Z-score for each asset. A negative Z-score indicates an oversold asset (buy signal), while a positive Z-score acts as a low expected return proxy.
* **Portfolio Construction:** Utilizes a dynamic Markowitz optimizer fed by expected return proxies and a rolling covariance matrix. Strictly enforces a no-short constraint (0 <= w_i <= 1) and a budget constraint (Sum of w_i = 1).
* **Risk Control & Backtesting:** Incorporates a 10% stop-loss per asset and a 15% maximum portfolio drawdown limit. Evaluates performance using a rolling out-of-sample design, comparing the strategy's Sharpe ratio and maximum drawdown against an equal-weight (1/N) baseline.

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, SciPy (for optimization), Requests, Matplotlib
* **Data Source:** Stooq API
