# Statistical arbitrage on S&P 500 equities

Two notebooks, built along `phases.txt`. Each phase is explained in plain words before the code, and each step ends with a check or a chart.

| Notebook | What it does | Result (2011–2026, net of 5 bps/trade + borrow) |
|---|---|---|
| **`01_pairs_trading.ipynb`** | Walk-forward pairs book. Engle-Granger cointegration (ADF on OLS residuals, Engle-Granger critical values) within GICS sub-industries. The hedge ratio is held fixed out-of-sample, and the spread's half-life sets the z-score window, the time stop and the capital per pair. Includes the tested PnL engine, yearly results, an ablation against the previous rules, sensitivity tables, a random-signal leakage check and an execution-timing check. | **Net Sharpe +0.50** (development 2011–18: +0.44, holdout 2019–26: +0.56), beta 0.04, max drawdown −6.3% |
| **`02_cross_sectional_residual.ipynb`** | Cross-sectional residual model on the same framework. Walk-forward PCA factors, then an out-of-sample residual z-score with a half-life filter. Long and short sector deciles, dollar- and sector-neutral, with a 2% name cap and a rebalance band. Ends with a comparison against the pairs book, a beta check and robustness tests. | Gross Sharpe +0.79; net Sharpe −0.04 at 5 bps, break-even ~5 bps, +0.25 at 3 bps |

Run `01_pairs_trading.ipynb` first. It saves `data/pairs_results.pkl`, which notebook 2 uses for the comparison table.

| Other files | |
|---|---|
| `phases.txt` | The workflow specification. |
| `data/` | `sp500_prices.pkl` and `spy.pkl` (Yahoo closes and opens, split- and dividend-adjusted, 2010–2026), `sp500_list.pkl` (GICS sector and sub-industry), and `pairs_results.pkl` (written by notebook 1). If a cache file is missing, the notebooks download it again. |

To run: `pip install -r requirements.txt`, then execute the notebooks in order. Notebook 1 takes about 6 minutes and notebook 2 about 1 minute.
