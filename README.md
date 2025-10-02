# Value at Risk. Monte Carlo Stock Price Simulation Analysis

A Python-based Monte Carlo simulation framework for modeling stock price movements using geometric Brownian motion (Wiener process). This project analyzes five major tech stocks to generate probabilistic price paths and assess risk profiles over a one-year horizon.

## Overview

This simulation implements the Wiener process to model stock price uncertainty, providing insights into potential future outcomes through ensemble analysis. The framework generates 100 simulation paths for each stock, calculating confidence bands and risk metrics to support portfolio management and investment decision-making.

## Features

- **Monte Carlo Simulation Engine**: Implements geometric Brownian motion for realistic stock price modeling
- **Multi-Stock Analysis**: Simultaneous analysis of multiple stocks (AAPL, GOOGL, NVDA, AMZN, UBER)
- **Risk Assessment**: Calculates 90% confidence intervals and risk spread metrics
- **Visualization Suite**: 
  - Single simulation path visualization
  - Ensemble plots with confidence bands
  - Individual stock subplot analysis
- **Statistical Summary**: Comprehensive risk metrics including median projections, confidence intervals, and risk spreads

## Technical Implementation

### Wiener Process Model

The simulation uses the stochastic differential equation:

```
dS = μS*dt + σS*dW
```

Where:
- **S**: Current stock price at time t
- **dS**: Infinitesimal change in stock price
- **μ (mu)**: Drift rate (annualized expected return from historical data)
- **σ (sigma)**: Volatility (annualized standard deviation from historical data)
- **dt**: Time increment (1/252 for daily trading periods)
- **dW**: Random increment from standard normal distribution

### Key Parameters

- **Simulation Period**: ~4.7 years of historical data (2021-01-01 to 2025-09-25)
- **Projection Horizon**: 1 year forward
- **Time Step**: Daily (dt = 1/252)
- **Number of Simulations**: 100 paths per stock
- **Confidence Level**: 90% (5th-95th percentiles)

## Installation

```bash
pip install yfinance numpy pandas matplotlib
```

## Usage

### Basic Simulation

```python
import yfinance as yf
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Define parameters
tickers = ["AAPL", "GOOGL", "NVDA", "AMZN", "UBER"]
start_date = '2021-01-01'
end_date = '2025-09-25'
T = 1.0  # 1 year projection
dt = 1 / 252  # Daily time step

# Run simulation (see full code for implementation)
```

### Key Functions

**`get_stock_data(ticker, start_date, end_date)`**
- Downloads historical stock data using yfinance
- Returns adjusted close prices

**`wiener_process(S0, mu, sigma, T, dt)`**
- Generates a single price path using geometric Brownian motion
- Returns time array and simulated price path

## Results & Insights

### Risk Profile Comparison

| Stock | Volatility (σ) | Initial Price | Median Return | 90% CI Range | Risk Spread |
|-------|----------------|---------------|---------------|--------------|-------------|
| AAPL  | 28.2%         | $260.39       | +9.6%         | $165.58 - $454.86 | 101.4% |
| GOOGL | 31.0%         | $247.72       | +17.3%        | $199.84 - $462.24 | 90.3% |
| NVDA  | 52.6%         | $180.13       | +50.1%        | $123.38 - $623.27 | 184.9% |
| AMZN  | 35.3%         | $213.51       | +1.8%         | $124.00 - $464.16 | 156.5% |
| UBER  | 46.6%         | $96.66        | +8.9%         | $59.02 - $226.66  | 159.3% |

### Key Findings

**Volatility Ranking**: NVDA exhibits the highest volatility and widest risk spread, making it the most unpredictable. AAPL and GOOGL show more moderate volatility with tighter confidence bands.

**Return Expectations**: Median projections vary significantly across stocks, with NVDA showing the highest expected return (+50.1%) but also the greatest uncertainty (5x confidence spread).

**Risk-Reward Trade-offs**: AMZN presents an unfavorable profile with moderate-high volatility (35.3%) but the lowest expected return (+1.8%), suggesting poor risk-reward asymmetry.

**Downside Protection**: UBER shows the tightest downside protection (39% maximum drop in worst 5% scenarios), while NVDA and AAPL face potential 32-36% downside risk.

## Practical Applications

### Portfolio Risk Management
Use the risk spread metric to scale position sizes inversely to volatility, constructing diversified exposure where no single position dominates total portfolio risk.

### Options Strategy Selection
Wide confidence intervals for NVDA and AMZN suggest profitable opportunities for volatility-based strategies (selling strangles, iron condors). Tighter bands for AAPL and GOOGL indicate lower option premiums but more predictable outcomes.

### Stop-Loss Calibration
The 5th percentile values provide statistically-driven floor levels for each position. Setting stops tighter than these levels increases the likelihood of being stopped out during normal market volatility.

## Limitations & Extensions

### Current Limitations
- Constant volatility assumption (reality: volatility clusters and changes over time)
- Fixed drift rate throughout simulation period
- No correlation modeling between stocks
- No jump processes for capturing sudden price movements

### Recommended Extensions

**Stochastic Volatility Models** (e.g., Heston model): Allow volatility itself to fluctuate randomly

**Regime-Switching Dynamics**: Account for different market conditions (bull vs bear markets) with distinct risk-return profiles

**Jump-Diffusion Processes**: Capture sudden price movements from earnings announcements or news events

**Correlation Modeling**: Incorporate dependencies between stocks for portfolio-level analysis

## License

This project is provided for educational and research purposes. Stock market simulations are probabilistic models and should not be the sole basis for investment decisions.

## Contributing

Contributions are welcome! Areas for improvement include:
- Implementation of advanced volatility models
- Multi-asset correlation analysis
- Portfolio optimization integration
- Additional risk metrics (VaR, CVaR, Sharpe ratio)

## Acknowledgments

Built using Python financial libraries including yfinance for data retrieval, NumPy for numerical computation, and Matplotlib for visualization.
