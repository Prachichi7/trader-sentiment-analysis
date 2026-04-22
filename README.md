# Trader Sentiment Analysis — Hyperliquid × Bitcoin Fear/Greed Index

An exploratory data analysis project examining how Bitcoin market sentiment (Fear/Greed)
relates to trader behavior and performance on the Hyperliquid decentralized exchange.

## Objective

Uncovers whether market sentiment meaningfully affects:
- Trader profitability (PnL, win rate)
- Trading behavior (position sizing, frequency, long/short bias)
- Performance across different trader segments

## Datasets

| Dataset | Source | Rows | Coverage |
|---|---|---|---|
| Bitcoin Fear/Greed Index | Alternative.me | 2,644 | Feb 2018 – May 2025 |
| Hyperliquid Trader Data | Hyperliquid DEX | 211,224 | 2023 – 2025 |

## Project Structure
├── primetrade.ipynb         # Main notebook that we need to run
├── fear_greed_index.csv   # Sentiment dataset
├── historical_data.csv    # Trader dataset
├── charts/
│   ├── chart1_performance_by_sentiment.png
│   ├── chart2_behavior_by_sentiment.png
│   ├── chart3_heatmaps.png
│   └── chart4_feature_importance.png
├── requirements.txt
└── README.md


## Setup & How to Run
**1. Clone the repo**
```bash
git clone https://github.com/YOUR_USERNAME/trader-sentiment-analysis.git
cd trader-sentiment-analysis
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Add the data files**
Place `fear_greed_index.csv` and `historical_data.csv` in the root directory.

**4. Run the notebook**
```bash
jupyter notebook analysis.ipynb
Or open directly in Google Colab

## Key Findings
1. **Win rate is sentiment-invariant (~0.61)** — traders close winning trades at nearly
   identical rates regardless of Fear or Greed conditions. Sentiment affects magnitude, not direction.

2. **Position sizes increase ~8% on Greed days** — median position size rises from $1,853
   on Fear days to $2,004 on Greed days, indicating traders take on more risk in bullish sentiment.

3. **Segment-level divergence is where the real signal lives** — aggregate averages mask
   significant variation across trader types. High-frequency and large-position traders
   are most exposed to sentiment-driven drawdowns on Fear days.

## Strategy Recommendations
**Rule 1 — Size Down on Fear**
Large-position traders show disproportionate PnL drawdowns on Fear days.
When the Fear/Greed index drops below 40, reduce position size by ~25–30%.

**Rule 2 — Trade Selectively on Fear Days**
High-frequency traders underperform on Fear days relative to selective traders.
Limit activity to highest-conviction setups when sentiment is fearful.

## Methodology
- Sentiment labels collapsed from 5 categories to 3 (Fear, Neutral, Greed)
- Trader data aggregated per account per day: PnL, win rate, trade count, position size, long/short ratio
- Datasets merged on date (daily granularity)
- Traders segmented by frequency, position size, and win rate consistency using tertile splits
- Bonus: Random Forest classifier trained to predict next-day profitability using sentiment + behavior features

## Bonus
- Random Forest model predicting next-day trader profitability (see notebook Section 5)
- Feature importance analysis showing which behavioral signals matter most

