<h1 align="center">Tejas Pandya</h1>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com/?lines=NYU+MSFE+(3.8)+%7C+ex-Nomura+Market+Risk;Alpha+research+%E2%80%A2+Derivatives+pricing+%E2%80%A2+Low-latency+C%2B%2B;Seeking+2027+full-time+quant+roles+(North+America);&font=Fira+Code&center=true&width=720&height=45&color=06b6d4&vCenter=true&size=19&pause=1000" alt="headline">
</p>

<p align="center">
  <a href="https://linkedin.com/in/tejaspandya9598"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="mailto:tbp8777@nyu.edu"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
  <a href="https://leetcode.com/u/6ixE11even/"><img src="https://img.shields.io/badge/LeetCode-FFA116?style=for-the-badge&logo=leetcode&logoColor=black" alt="LeetCode"></a>
  <a href="https://codeforces.com/profile/6ixE11even"><img src="https://img.shields.io/badge/Codeforces-1F8ACB?style=for-the-badge&logo=codeforces&logoColor=white" alt="Codeforces"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/CFA-Level%20I-1B365D?style=flat-square" alt="CFA L1">
  <img src="https://img.shields.io/badge/Baruch%20MFE-C%2B%2B%20for%20Financial%20Engineering-2E5E4E?style=flat-square" alt="Baruch C++">
  <img src="https://img.shields.io/badge/Bloomberg-Market%20Concepts-000000?style=flat-square" alt="BMC">
  <img src="https://img.shields.io/badge/CFI-FMVA-4B8BBE?style=flat-square" alt="FMVA">
</p>

I build quant research and trading infrastructure. Three years running market-risk
systems at Nomura (VaR, FRTB, multi-asset) taught me how production breaks; the
projects below are me building the research stack on top of that — signals, pricing,
backtests, and the low-latency plumbing underneath. Every repo ships with tests,
CI, and a README that explains the math, not just the code.

Every number on this page is one I have reproduced on my own machine, and the READMEs
say which command produces it. Several of them are lower than what used to be here:
an audit of all twelve repos in September 2026 found a benchmark that did not
reproduce, a backtest fitting hedge ratios on its own test window, and a
regime strategy reading macro data published after the month it was trading. Those
are fixed, and the numbers moved. The commit history has the details.

---

### 📈 Alpha research & backtesting

| Project | What it does | Stack |
|---|---|---|
| **[equity-xs-alpha](https://github.com/tejaspandya9598/equity-xs-alpha)** | Six signals on 494 S&P names → rank IC with Newey-West t-stats → cost-aware quintile portfolios → LightGBM combo under purged walk-forward CV. OOS net Sharpe **0.77** vs **−0.58** for the naive equal-weight baseline | Python · LightGBM |
| **[stat-arb-backtester](https://github.com/tejaspandya9598/stat-arb-backtester)** | Event-driven pairs backtester on live Deribit crypto. Selection and hedge ratios fitted in-sample only, Benjamini-Hochberg across all 15 pairwise tests — under which **no pair survives**, and the surviving set moves with the training window | Python |
| **[macro-regime-allocation](https://github.com/tejaspandya9598/macro-regime-allocation)** | PCA + two-step K-Means on 120+ FRED-MD indicators feeding mean-variance allocation, every signal lagged by the publication delay. **11.2%/yr vs 5.6%** for equal weight in MSCI developed; the cost-aware convex book holds Sharpe 0.51–0.68 across a 0–100bps sweep | Python · cvxpy |
| **[prediction-markets](https://github.com/tejaspandya9598/prediction-markets)** | Live Polymarket scanner for cross-outcome arbitrage in neg-risk events, netted against the quoted spread. Most of the headline edge on long-dated political baskets turns out to be the discount rate | Python |

### 🧮 Derivatives pricing & rates

| Project | What it does | Stack |
|---|---|---|
| **[sofr-swap-pnl-attribution](https://github.com/tejaspandya9598/sofr-swap-pnl-attribution)** | SOFR curve bootstrap, $255M ten-swap 2–30y book, daily P&L split into carry / roll-down / level / slope / curvature via key-rate durations. Par swaps reprice to **<1e-9**, attribution reconciles to full revaluation | Python |
| **[sabr-vol-calibration](https://github.com/tejaspandya9598/sabr-vol-calibration)** | SABR (Hagan) calibrated to live Deribit BTC smiles: **0.43 vol-pt RMSE** across 21 strikes live, 0.035 on synthetic ground truth. Bounds scale with the forward, so it works on rates and crypto alike | Python |
| **[options-pricing-engine](https://github.com/tejaspandya9598/options-pricing-engine)** | European/American/barrier options via Black-Scholes, Monte Carlo, Crank-Nicolson FDM; projected SOR for early exercise | C++20 |

### ⚡ Market microstructure & low latency

| Project | What it does | Stack |
|---|---|---|
| **[hft-matching-engine](https://github.com/tejaspandya9598/hft-matching-engine)** | Deterministic limit-order-book engine, O(1) insert/cancel/execute, zero-allocation memory pool. **~21M msgs/sec on an Apple M2, ~36M on Linux aarch64** — same silicon, and the gap is the point | C++20 |
| **[lob-market-manipulation-detection](https://github.com/tejaspandya9598/lob-market-manipulation-detection)** | Spoofing/layering detection over 1.4M L2 events, 27 microstructure features, Isolation Forest + ECOD rank-averaged. The two rank at **0.865 Spearman** and overlap on 76% of each other's top 5% | Python · PyOD |
| **[optimal-execution](https://github.com/tejaspandya9598/optimal-execution)** | Almgren-Chriss closed-form liquidation + cost/risk efficient frontier, impact and spread calibrated live from Deribit. A 10%-of-ADV order costs **7.7bps vs TWAP's 4.8** for **38% less variance** | Python |

### 🔬 ML foundations & commodities

| Project | What it does | Stack |
|---|---|---|
| **[ml-algorithms-from-scratch](https://github.com/tejaspandya9598/ml-algorithms-from-scratch)** | GBDT, random forest, SVM (both hinge sub-gradient and SciPy dual QP), logistic regression, PCA from first principles. Matches scikit-learn to four decimals on logistic, SVM and the decision tree; the forest lands 0.937 vs 0.958 | NumPy |
| **[commodity_futures_settlement_price_analysis](https://github.com/tejaspandya9598/commodity_futures_settlement_price_analysis)** | WTI/Henry Hub settlement anomaly detection + term-structure dashboard. Twelve events across 2021–2025, all twelve corroborated by an independent Isolation Forest, over a 60-month front-month roll | Python · Streamlit |

---

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/C%2B%2B20-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++">
  <img src="https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white" alt="SQL">
  <img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="pandas">
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" alt="sklearn">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/CMake-064F8C?style=for-the-badge&logo=cmake&logoColor=white" alt="CMake">
  <img src="https://img.shields.io/badge/Bloomberg-Terminal-000000?style=for-the-badge" alt="Bloomberg">
</p>

<p align="center">
  <i>Risk-desk production rigor + ML research + low-latency C++ — most candidates have one; the combination is the edge.</i>
</p>
