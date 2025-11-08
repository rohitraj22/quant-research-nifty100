# Quantitative Research: Factor-Based Equity Strategy

## Overview

This project performs a backtest and analysis of two common factor-based equity strategies—**Momentum** and **Value**—on the Indian market (NIFTY 100 stocks). The goal is to evaluate the performance of long-short, market-neutral portfolios constructed using these factors and compare them against the NIFTY 50 benchmark.

## Methodology

### Data Preparation
- **Source:** Daily OHLCV data for all NIFTY 100 constituents was downloaded from Yahoo Finance (`yfinance`) for the period from January 2022 to November 2025.
- **Cleaning:** The data was cleaned by forward-filling and then backward-filling missing values (NaNs).
- **Resampling:** Daily prices were resampled to month-end frequencies to align with the strategy's monthly rebalancing schedule.

### Factor Definitions
- **Momentum:** Calculated as the 12-month percentage return, skipping the most recent month to account for short-term reversal effects.
- **Value:** A technical proxy for value was used, defined as the ratio of the current price to its 12-month rolling average. A lower ratio indicates a "cheaper" stock.

### Portfolio Construction
- **Ranking:** Stocks were ranked monthly based on their factor scores.
- **Long/Short:** Quintile portfolios were formed. The strategy goes long the top 20% of stocks (best scores) and short the bottom 20% (worst scores).
- **Returns:** The final strategy return is the equal-weighted return of the long basket minus the short basket.

## Results

### Performance Metrics (Jan 2022 - Nov 2025)

| Strategy | CAGR | Sharpe Ratio | Max Drawdown |
| :--- | :--- | :--- | :--- |
| **Momentum** | 4.47% | 0.51 | -27.6% |
| **Value** | 5.93% | 0.54 | -20.4% |
| **Blend (Bonus)** | 4.99% | 0.51 | -24.8% |
| **NIFTY 50** | 10.60% | 0.86 | -14.3% |

### Key Observations
- The **NIFTY 50 benchmark** outperformed all factor strategies on both an absolute and risk-adjusted basis during this period.
- Both **Momentum** and **Value** strategies were profitable but experienced higher volatility and drawdowns compared to the market.
- The **Blended** factor (simple average of Z-scores) did not provide a significant performance boost over the individual factors.

## Assumptions & Limitations
- **No Transaction Costs:** The backtest does not account for brokerage fees, slippage, or market impact.
- **Survivorship Bias:** The analysis uses the current NIFTY 100 constituents, which may introduce survivorship bias as delisted stocks are excluded.
- **Shorting:** Assumes perfect ability to short stocks with no borrowing costs.

## Future Improvements
- Incorporate realistic transaction costs and slippage.
- Use point-in-time historical constituent data to eliminate survivorship bias.
- Explore fundamental data for a more robust Value factor (e.g., P/E, P/B ratios).
- Implement more sophisticated portfolio construction techniques (e.g., optimization, risk parity).
