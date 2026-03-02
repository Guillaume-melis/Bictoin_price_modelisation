# Bitcoin Price Modeling - Halving & Offer/Demand Framework

This repository contains Python simulations and analyses for **Bitcoin price dynamics**, exploring two approaches:

1. **Halving-based drift model**  
2. **Offer/Demand fundamental model with stochastic shocks**

---

## 📌 Motivation

Bitcoin differs from traditional assets due to:

- Finite supply (21 million BTC)  
- Halving events every 210,000 blocks, reducing mining rewards  
- Speculative and adoption-driven demand  

We aim to capture both **statistical properties** (heavy tails, volatility clustering) and **fundamental drivers** (supply, mining cost, halvings).

---

## 🛠 Modeling Approaches

### 1️⃣ Halving-based Drift Model (Initial Attempt)

- Introduced an **indicator for halving events** to model temporary drift increases in BTC returns.  
- Drift function:

\[
\mu(t) = \sum_k \mathbf{1}_{0 < t-\tau_k < T_h} \quad \text{or} \quad \mu(t) = \sum_k e^{-\gamma (t-\tau_k)} \mathbf{1}_{t>\tau_k}
\]

where:

- $\tau_k$ = date of k-th halving  
- $T_h$ = effect window (e.g., 500 days)  
- $\gamma$ = exponential decay factor  

- Goal: capture **pump effect post-halving**.  
- Limitation: cannot model **price magnitude or volatility** realistically, only drift.

---

### 2️⃣ Offer/Demand + Stochastic Model (Refined)

- **Supply**: deterministic cumulative BTC supply, halving events slow new supply  
- **Demand**: adoption growth + α-stable stochastic shocks  
- **Price**:

\[
P_t = \max\Big( k \cdot \frac{D_t}{21M - S_t}, \text{Mining cost floor} \Big)
\]

- Add multiplicative stochastic noise for heavy tails and volatility clustering  
- Magnitude calibrated to realistic levels (~$100,000 USD in 2024)  
- Pumps post-halving naturally emerge from supply slowdown

---

## 📈 Stylized Facts Captured

- Heavy-tailed returns (tail index α ~ 1.86)  
- Volatility clustering  
- Post-halving price surges  
- Drift interpretable from supply/demand dynamics

---
## ⚡ Next Steps / Potential Extensions

- Calibrate stochastic model to historical BTC returns  
- Add macro shocks or bull/bear regime switching  
- Rolling correlations with traditional assets  
- Test β calibration using halving-based drift

---

## 📌 References

- Bariviera & Merediz-Solà (2021) – Stylized facts in cryptocurrency markets  
- Urquhart (2016) – Efficiency of Bitcoin markets  
- Cont (2001) – Empirical properties of asset returns  
- Ahmed et al. (2024) – Statistical properties of cryptocurrency returns

---

## 🖥 Requirements

```bash
pip install numpy pandas matplotlib scipy seaborn yfinance
