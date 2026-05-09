# Global Stock Index Analysis Pipeline

An end-to-end data pipeline for historical stock index data: ingestion, validation, cleaning, feature engineering, and multi-panel technical visualisation.

---

## Overview

This project demonstrates a **production-minded data workflow** applied to financial time-series data. It covers every stage from raw CSV to actionable charts, following software engineering best practices: typed, documented functions; no hardcoded row indices; reusable per-index logic.

| Stage | What happens |
|---|---|
| **Ingestion** | Load CSV, inspect shape, dtypes, nulls, and date ranges |
| **Validation** | Quality checks — nulls, zero prices, duplicates |
| **Cleaning** | Type casting, deduplication, column selection |
| **Feature Engineering** | Daily return, moving averages (MA-20, MA-50), rolling volatility, drawdown |
| **Summary Statistics** | Annualised return, volatility, Sharpe ratio, max drawdown per index |
| **Visualisation** | 3-panel technical chart per index + normalised comparison overlay |

---

## Dataset

**Source:** [`indexData.csv`](https://www.kaggle.com/datasets/mattiuzc/stock-exchange-data) (Kaggle)  
**Coverage:** Multiple global stock indices, 1965–2021  
**Columns:** `Index`, `Date`, `Open`, `High`, `Low`, `Close`, `Adj Close`, `Volume`

---

## Features Engineered

| Feature | Formula | Window |
|---|---|---|
| `daily_return` | `Close.pct_change() × 100` | 1 day |
| `ma_short` | Rolling mean of `Close` | 20 days |
| `ma_long` | Rolling mean of `Close` | 50 days |
| `volatility` | Rolling std of `daily_return` | 20 days |
| `drawdown` | `(Close − cummax) / cummax × 100` | Expanding |

---

## Visualisations

### Technical Chart (per index)

Three-panel chart for each index:
- **Top:** Close price + MA-20 + MA-50
- **Middle:** Rolling volatility (annualised)
- **Bottom:** Drawdown from peak

### Normalised Performance Comparison

All indices rebased to 100 at their first trading date, plotted on a single chart for apples-to-apples comparison.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.12 | Core language |
| Pandas | Data manipulation |
| NumPy | Numerical computations |
| Matplotlib | Visualisation |

---

## How to Run

```bash
# 1. Clone the repo
git clone https://github.com/Eliasmatheussouza/stock-index-analysis.git
cd stock-index-analysis

# 2. Install dependencies
pip install pandas numpy matplotlib jupyter

# 3. Place the dataset
# Download indexData.csv from Kaggle and put it in the project root.

# 4. Launch the notebook
jupyter notebook stock_index_analysis.ipynb
```

---

## Project Structure

```
stock-index-analysis/
├── stock_index_analysis.ipynb   # Main analysis notebook
├── README.md                    # This file
└── indexData.csv                # Raw dataset (not tracked by git)
```

---
