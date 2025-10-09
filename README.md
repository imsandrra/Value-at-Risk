# 📈 Monte Carlo Stock Price Simulation

## 🧩 Overview

This project implements a **Monte Carlo simulation framework** to model and analyze stock price movements using the **Geometric Brownian Motion (GBM)** model.
It focuses on five major technology stocks — **AAPL, GOOGL, NVDA, AMZN, and UBER** — using historical data to simulate their **1-year forward price distributions**, evaluate **downside risk**, and compare **risk–return profiles**.

---

## ⚙️ Methodology

### **Mathematical Model**

The simulation is based on the stochastic differential equation (Wiener process):

$dS_t = μS_t , dt + σS_t , dW_t$

Where:

| Symbol   | Description                                                              |
| :------- | :----------------------------------------------------------------------- |
| $S_t$  | Stock price at time *t*                                                  |
| $μ$    | Annualized drift (expected return)                                       |
| $σ$    | Annualized volatility (standard deviation of returns)                    |
| $dW_t$ | Wiener process increment (random term from standard normal distribution) |

---

### **Process Summary**

1. **Historical Data Processing**

   * Collect and clean price data for target stocks.
   * Compute **log returns** and estimate **drift (μ)** and **volatility (σ)**.

2. **Monte Carlo Simulation**

   * Generate thousands of **randomized price paths** per stock (e.g., 100,000 simulations).
   * Compute confidence intervals (5th–95th percentiles) to visualize uncertainty.

3. **Risk Evaluation**

   * Compute **Value-at-Risk (VaR)** and **Expected Shortfall (CVaR)** at 5% confidence level.
   * Compare downside exposure across all assets.

---

## 📊 Key Insights

### **1. Risk–Return Profile Comparison**

| Stock    | Volatility (σ) | Median Return | Risk Spread | Observation                              |
| -------- | -------------- | ------------- | ----------- | ---------------------------------------- |
| **NVDA** | 52.6%          | +45.1%        | ~190%       | Most volatile, extreme outcomes possible |
| **AAPL** | 28%            | +12%          | ~96%        | Stable, consistent market outperformer   |
| **GOOG** | 31%            | +18%          | ~107%       | Best risk-adjusted performer             |
| **AMZN** | 33%            | +1.8%         | ~123%       | Unfavorable risk–reward ratio            |
| **UBER** | 45%            | +7.4%         | ~170%       | High downside risk, modest returns       |

---

### **2. Downside Risk (5% Worst Scenarios)**

| Stock    | 5th Percentile Return | Interpretation                        |
| -------- | --------------------- | ------------------------------------- |
| **UBER** | -50.3%                | Highest downside exposure             |
| **AMZN** | -43.0%                | Substantial risk, low reward          |
| **NVDA** | -37.6%                | High risk, high potential return      |
| **AAPL** | -29.9%                | Moderate downside, stable performance |
| **GOOG** | -29.0%                | Most resilient under stress           |

---

### **3. Overall Conclusions**

* **GOOG** and **AAPL** deliver the best **risk-adjusted performance**, combining stability with market-beating returns.
* **NVDA** offers **exceptional upside potential** but with substantial volatility — suited for high-risk investors.
* **AMZN** and **UBER** show **unfavorable asymmetries**, with large potential drawdowns and limited expected gains.

---

## 🧠 Project Structure

```
VaR.ipynb              # Main Jupyter notebook
data/                  # Historical price data (if included)
results/               # Generated plots and summary statistics
README.md              # Project documentation
```

---

## 🚀 Getting Started

### **Requirements**

Install dependencies:

```bash
pip install numpy pandas matplotlib yfinance
```

### **Run Simulation**

1. Open `VaR.ipynb` in Jupyter Notebook or VS Code.
2. Execute all cells to reproduce simulations, confidence intervals, and visualizations.

---

## 🧾 License

This project is released under the **MIT License**.
You’re free to use, modify, and distribute it with attribution.
