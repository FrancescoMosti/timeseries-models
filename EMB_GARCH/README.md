# EMB_GARCH - Volatility Modeling on Emerging Market Bonds

This project analyzes and forecasts the volatility of the iShares J.P. Morgan USD Emerging Markets Bond ETF (EMB) using advanced time-series models.\
The goal is to evaluate model performance in capturing volatility clustering, regime shifts, and forecast accuracy, through a combination of traditional econometrics and probabilistic modeling.

## Models Implemented:

- GARCH family models\
- GARCH(1,1), IGARCH\
- GARCH-t(1,2): selected as best performing model (lowest MAE/RMSE)\
- EGARCH for asymmetric effects (benchmark)\
- Hidden Markov Model (HMM)\
- Gaussian HMM with 2 and 3 latent regimes.
  Identifies periods of high vs low volatility based on return distributions

Regime persistence and transition matrix analysis included
Rolling Forecast Framework
1-day, 5-day, 10-day forecasts
Out-of-sample evaluation with realized volatility comparison

## Data:
Primary asset: EMB ETF (2021–2024), fetched via yfinance
Additional macro indices for exploratory analysis:

- ^VIX (implied volatility)
- ^TNX (10-year Treasury yield)
- DX-Y.NYB (USD index)
- SPY (S&P 500)
- HYG, LQD (corporate bond ETFs)
- GLD (gold)

## Findings:
GARCH-t(1,2) with Student’s t-distributed residuals outperformed all other specifications.\
EGARCH did not improve results in this setting despite modeling asymmetries.\
HMMs successfully detected regime switches, with high persistence in low-volatility states.\
Rolling correlations with market indices (e.g., VIX, TNX) revealed weak and unstable linear relationships, highlighting the need for regime-based or nonlinear approaches.

## Project Structure

```
EMB_GARCH/
│
├── data/                      # Holdings data and loadable metadata
│   ├── EMB_holdings_clean.csv
│
├── utils/                     # Utility functions used across the project
│   ├── data_utils.py
│   ├── hmm_utils.py
│   ├── model_utils.py
│   ├── plotting_utils.py
│
├── VolaFitting_GARCH.ipynb    # Main notebook with estimation, plots, and evaluation
├── requirements.txt           # Python dependencies
└── README.md                  # This file
```
## How to Run

1. Clone the repository:
```bash
git clone https://github.com/FrancescoMosti/timeseries-models.git
cd timeseries-models/EMB_GARCH
```

2. Create a virtual environment (optional but recommended):
```bash
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
```

3. Install the required dependencies:
```bash
pip install -r requirements.txt
```

4. Launch the main notebook:
```bash
jupyter notebook VolaFitting_GARCH.ipynb
```

## Limitations and Future Work:
HMM assumes Gaussian emissions – future work could extend to Bayesian HMMs with t-distributions.\
Only univariate models are tested – DCC-GARCH or multivariate HMMs could improve portfolio-level risk modeling.\
Incorporating macro factors or sentiment data may enhance explanatory power.\
Deep learning models (e.g., LSTMs) could be considered for non-linear sequential modeling, with sufficient data and training capacity.

## Author:
Francesco Mosti
francesco.mosti@yahoo.com

