# Portfolio Tracker & Analyser

A Python tool that pulls historical price data for a basket of stocks and ETFs, then analyses the portfolio's return and risk — including returns, volatility, correlation, and risk-adjusted performance (Sharpe ratio) against a benchmark.

Built to apply portfolio-theory fundamentals to real market data rather than toy examples.

## What it does

- Downloads ~4 years of daily price data via the `yfinance` API (no API key required)
- Calculates daily and cumulative returns for each holding
- Measures annualised volatility (risk) per holding
- Builds a correlation matrix to assess diversification
- Blends holdings into a weighted portfolio and compares it to a benchmark (S&P 500 / VOO)
- Computes the Sharpe ratio to compare return *per unit of risk*

## Tech

Python · pandas · matplotlib · yfinance · NumPy · Jupyter Notebook

## The metrics — what they mean

**Daily / cumulative returns.** Prices on their own aren't comparable across holdings (a €13 stock and a €300 stock can't be compared by price), so the analysis works in returns. Cumulative return shows the growth of €1 invested at the start.

**Annualised volatility.** The standard deviation of daily returns, scaled to a yearly figure (× √252, since there are ~252 trading days a year). It puts a number on how bumpy each holding's ride was — higher volatility means higher risk.

**Correlation matrix.** Measures, for each pair of holdings, how closely they move together (+1 = lockstep, 0 = unrelated, −1 = opposite). Low correlation is what gives a portfolio genuine diversification: when holdings don't all move together, the overall portfolio is steadier than its parts.

**Sharpe ratio.** (Return − risk-free rate) ÷ volatility. It answers "how much return did you earn for the risk you took?" — crediting the portfolio only for return above the risk-free rate (~4%, what you'd earn risk-free) and penalising volatility. A Sharpe near 1 is decent; above 1.5 is strong. It lets you compare portfolios fairly even when one is riskier.

## Example results (AAPL, MSFT, NVDA, VOO — equal weight, 2021–2024)

| Metric | Portfolio | Benchmark (VOO) |
|---|---|---|
| Annual return | 32.0% | 14.5% |
| Annual volatility | 26.5% | 16.4% |
| Sharpe ratio | 1.06 | 0.64 |

Over this period the equal-weight portfolio beat the market on both raw return and risk-adjusted return.

## Interpretation & limitations

The results are **period-specific and backward-looking.** 2021–2024 was an exceptional run for AI/tech, and NVDA especially drove the portfolio's outperformance. The correlation analysis shows all four holdings are positively correlated (0.55–0.78) — this is a concentrated bet on large-cap US tech, not a genuinely diversified portfolio. The same concentration that paid off here is what would be hit hardest in a tech downturn, and the Sharpe ratio could look very different over a different window.

In short: over this period, concentration in tech paid off on a risk-adjusted basis — but that reflects a bet on one theme continuing, not true diversification.

## How to run

```bash
pip install yfinance pandas matplotlib
jupyter notebook
```

Open `Analysis.ipynb` and run the cells top to bottom. Edit the `tickers` list to analyse a different basket.

## Possible extensions

- Optimise portfolio weights (efficient frontier / max Sharpe) rather than equal weight
- Add max drawdown and rolling volatility
- Include uncorrelated asset classes (bonds, gold) to test the diversification effect
