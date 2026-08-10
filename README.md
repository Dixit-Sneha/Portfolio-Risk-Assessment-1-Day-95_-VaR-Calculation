# Portfolio Risk Assessment & 1-Day 95% Value at Risk (VaR)

A Python-based quantitative finance project focused on measuring and evaluating the daily risk associated with a diversified equity portfolio consisting of Apple, Microsoft, Amazon, and Tesla/Google. The project uses statistical modeling, historical simulation, stress analysis, and backtesting techniques to estimate potential portfolio losses under different market conditions.

## Project Overview

Understanding equity market risk requires more than simply measuring price volatility. This project applies different risk assessment methods to a four-stock portfolio to estimate potential losses at the 95% confidence level. Multiple Value at Risk (VaR) approaches are compared with historical market performance to examine downside exposure, diversification effects, and extreme market movements.

### Key Features

* **Market Data Collection & Processing:** Historical stock price data is retrieved using `yfinance`, followed by the calculation of multi-period additive log returns for consistent return analysis.
* **Statistical Distribution Analysis:** Portfolio and asset returns are modeled using both Normal and Student's t-distributions through `SciPy.stats`, allowing comparison of normal and fat-tailed behavior.
* **Value at Risk Calculation:** Estimates 1-day 95% VaR using three different approaches:

  * Parametric VaR using the Normal Distribution
  * Parametric VaR using the Student's t-Distribution
  * Historical Simulation-based VaR
* **Expected Shortfall Analysis:** Calculates Expected Shortfall (ES) to determine the average loss occurring beyond the 95% VaR threshold.
* **Backtesting & Model Validation:** Tests the VaR models across a 1,378-day historical period by examining the frequency of losses exceeding the predicted risk level.
* **Rolling Risk Analysis:** Uses rolling historical VaR calculations to track changes in portfolio risk and identify shifts in market conditions over time.

---

## Technical Stack & Library Selection

* **`yfinance`**: Used to retrieve historical OHLC stock market data from Yahoo Finance.
* **`Pandas`**: Handles data cleaning, transformation, alignment, and rolling-window calculations.
* **`NumPy`**: Supports numerical computations, vectorized operations, portfolio variance calculations, and related metrics.
* **`SciPy (stats)`**: Used for statistical testing, distribution fitting, hypothesis testing, and probability calculations.
* **`Matplotlib` & `Seaborn`**: Used to visualize return distributions, correlations, cumulative performance, drawdowns, and portfolio risk.

---

## Quantitative Findings & Portfolio Metrics

### 1. Asset Characteristics & Returns

* **Return Performance:** **MSFT** recorded the highest average daily return during the selected period, followed by **AAPL**.
* **Volatility:** **AMZN** showed the highest variance at 0.000523, reflecting greater short-term price fluctuations.
* **Return Distribution:** The **Jarque-Bera test** produced a p-value below 0.05, rejecting the assumption of normally distributed returns. The presence of fat tails and high kurtosis indicates that a standard Normal distribution may underestimate extreme losses.

### 2. Portfolio Diversification

* **Correlation Analysis:** **AAPL** and **MSFT** showed the strongest positive correlation, resulting in relatively lower diversification benefits between the two. Tesla and Google showed comparatively lower correlation, offering greater diversification potential.
* **Risk Reduction:** The portfolio's standard deviation was lower than the weighted average volatility of the individual stocks, demonstrating the risk-reduction effect of diversification.

### 3. Tail Risk, Drawdown & Stress Analysis

* **VaR Comparison:** Historical Simulation produced more conservative loss estimates than the Normal parametric approach because it incorporates actual extreme observations from the historical data.
* **Expected Shortfall:** Historical ES was higher than parametric ES, indicating greater exposure to losses in the extreme tail of the return distribution.
* **Historical Stress Metrics:**

  * **Maximum Drawdown:** −51.26
  * **Drawdown / Recovery Duration:** 919 days, demonstrating the impact of prolonged periods of market decline.

### 4. VaR Backtesting

* **Testing Period:** 1,378 trading days.
* **Observed Exceptions:** Approximately 2% of observations exceeded the estimated 95% VaR threshold, which is close to the expected theoretical exception frequency and supports the effectiveness of the historical VaR model as a baseline risk measure.

---

## Strategic Risk Management Recommendations

1. **Use Tail-Aware Risk Models:** Normal-distribution VaR should not be used as the sole risk measure when returns exhibit significant skewness and kurtosis. Student's t-distributions and historical simulation provide better consideration of extreme outcomes.
2. **Optimize Portfolio Allocation:** Consider reducing exposure to highly volatile assets such as AMZN while increasing allocation toward assets with lower correlations to improve overall portfolio risk characteristics.
3. **Maintain Adequate Capital Reserves:** Expected Shortfall estimates can be used to determine appropriate liquidity buffers capable of absorbing significant market losses and prolonged drawdowns.

