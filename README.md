# Trader Behavior & Market Sentiment Analysis

## Project Overview
This project analyzes how trader behavior and performance vary across different market sentiment regimes. By combining transaction-level trading data with the Fear & Greed Index, the analysis identifies behavioral patterns, evaluates profitability drivers, segments traders, and translates findings into actionable trading rules.

The objective is to move beyond descriptive analytics and uncover decision-relevant insights related to risk-taking, trading activity, and performance consistency.

---

## Dataset
The analysis integrates two datasets:

- **Historical Trading Data:** Contains transaction-level details such as execution price, position size, trade direction, and realized PnL.
- **Fear & Greed Index:** Provides daily market sentiment classifications (Extreme Fear → Extreme Greed).

Both datasets were cleaned, timestamp-aligned, and merged at the daily level to enable sentiment-aware behavioral analysis.

---

## Methodology

The project follows a structured analytics workflow:

1. **Data Preparation**
   - Cleaned datasets and handled formatting inconsistencies.
   - Converted timestamps and aligned data by trading date.
   - Validated merges to ensure no unintended row inflation.

2. **Feature Engineering**
   - Win rate  
   - Average position size (used as a proxy for risk exposure)  
   - Trading frequency  
   - Average profitability  
   - Loss magnitude  

3. **Behavioral Analysis**
   - Compared trader performance across sentiment regimes.
   - Evaluated how volatility influences trading activity and capital deployment.

4. **Trader Segmentation**
   - Frequent vs. infrequent traders  
   - Consistent vs. inconsistent traders  

5. **Unsupervised Learning**
   - Applied **K-Means clustering** on trader-level behavioral metrics.
   - Used **PCA (Principal Component Analysis)** to reduce dimensionality and improve cluster visualization.

---

## Key Insights

### 1. Greed Improves Performance but Introduces Tail Risk
Average trader profitability increases as sentiment moves toward Extreme Greed. However, the largest loss in the dataset also occurs during this regime, indicating elevated reversal risk.

### 2. Fear Drives Market Participation
Fear-driven markets exhibit the highest trading activity and larger average position sizes, suggesting that traders often interpret volatility as an opportunity rather than a threat.

### 3. Loss Control Is a Primary Driver of Long-Term Profitability
Frequent and consistent traders outperform primarily due to smaller average losses, while high-variance traders generate larger profits but experience substantially greater return volatility.

---

## Behavioral Clustering

Clustering analysis reveals three distinct trader archetypes:

- **High-Conviction Traders:** Deploy larger capital with strong win rates and superior average profitability.
- **High-Frequency Traders:** Execute many small trades with moderate returns.
- **Moderate / Underperforming Traders:** Exhibit weaker profitability and lower execution consistency.

The PCA projection confirms structural separation between these behavioral groups, suggesting that trader behavior naturally organizes into identifiable risk-return profiles rather than forming a homogeneous population.

---

## Strategy Recommendations

### Rule 1 — Controlled Participation During Fear Regimes
**If sentiment = Fear or Extreme Fear → increase trading participation but enforce stricter loss limits and position caps, particularly for high-variance traders.**

Rationale: Volatility creates opportunity, but unmanaged exposure increases drawdown risk.

---

### Rule 2 — Reduce Position Aggression During Extreme Greed
**If sentiment = Extreme Greed → scale down position sizes and avoid concentrated bets.**

Rationale: While profitability peaks in optimistic markets, tail-risk events become more pronounced.

---

## Technical Stack
- Python  
- Pandas / NumPy  
- Matplotlib / Seaborn  
- Scikit-learn (K-Means, PCA)

---
### Setup
```bash
pip install -r requirements.txt
```
### Run
Open and execute the notebook:

```bash
notebook/trader_behavior_analysis.ipynb
```
---
## Project Structure
``` bash
trader-behavior-sentiment-analysis/
│
├── data/                # Raw datasets
├── notebook/            # Analysis notebook
├── images/              # Exported charts
├── requirements.txt
└── README.md
```
---
## Limitations
- The dataset does not include an explicit leverage variable; therefore, **average position size was used as a proxy for risk exposure.**
- The analysis is based on historical behavioral patterns and should be interpreted as directional insight rather than causal evidence.
- Trader-level aggregation may mask intra-trader strategy variations across different market conditions.

---

## Conclusion
This analysis demonstrates that trader performance is influenced not only by market sentiment but also by behavioral discipline. Fear-driven markets tend to increase trading participation, while greed-driven regimes improve profitability but introduce elevated tail risk. 

The findings suggest that sustained trading success is more closely associated with effective loss control and consistent execution than with occasional high-return trades. Aligning trading behavior with market conditions while maintaining disciplined risk management may help improve risk-adjusted performance.
