# Election-Driven Asset Allocation under Political Uncertainty

**Minimizing Portfolio Risk Amid U.S. Presidential Uncertainty**  
Duke University – The Fuqua School of Business  
Master of Quantitative Management (MQM) – Finance Track  
Capstone Project – Team 56  
Team Members: Weicheng Wang (FIRST AUTHOR), Qi Deng, Jiaying Sun, Omair Khan, Pavan Kumar Meka

---

## Project Overview

This repository presents our MQM Finance Capstone project, which investigates how U.S. presidential elections influence market volatility and delivers a machine learning–based asset allocation tool that minimizes portfolio risk. The project integrates time-series modeling (ARIMA, GARCH), political scenario encoding, and Random Forest regression to generate optimized investment weights under hypothetical election conditions.

---

## Directory Structure

### `a_DataCleaning/`
Preprocessing of raw volatility data.

**Contents:**
- Raw index files: `GVZ.csv`, `OVX.csv`, `TLT_impliedVol.csv`, `VIX.csv`, `VXEEM.csv`, `VXN.csv`
- `DataCleaning.ipynb`: Cleans and merges daily data into a unified dataset
- **Output:** `Master_Volatility_Index_Daily.csv` used in all subsequent analyses

---

### `b_DataAnalysis/`
Contains all analyses and model development.

**Contents:**
- `Analysis1-4.ipynb`: Long-term volatility trends, election phase risk, event study with ARIMA/GARCH, and political feature engineering
- `Analysis5.ipynb`: Final implementation of the Random Forest-based allocation model
- `Combined_Event_Study_ARIMA_GARCH.csv`: Event study results
- `US_Presidential_Elections_2000–2024.csv`: Political feature dataset
- `final_rf_pipeline.pkl`: Trained Random Forest model
- `Master_Volatility_Index_Daily.csv`: Cleaned dataset from `a_DataCleaning/`

**Instructions:**
Open `Analysis5.ipynb` to input a political scenario and receive recommended asset allocations.

---

### `c_HTML_files_of_DataAnalysis/`
HTML versions of Jupyter notebooks for viewing without code execution.

---
## Objective Function

We define the election-aware portfolio optimization problem as follows:

$$
\min_{\mathbf{w}} \sum_{i=1}^{n} w_i^2 \left( \hat{\sigma}^2_{i,\text{post}} + \lambda \cdot \text{Abnormal}_i^2 \right)
$$

**Where:**

- $w_i$: Weight allocated to asset $i$  
- $\hat{\sigma}_{i,\text{post}}$: GARCH-predicted post-election standard deviation for asset $i$  
- $\text{Abnormal}_i$: Historical abnormal volatility for asset $i$, computed as actual minus predicted post-election volatility  
- $\lambda$: Penalty term to control the influence of election-period shocks  
- $n$: Number of assets (in this case, $n = 6$)

**Constraints:**

$$
\sum_{i=1}^{n} w_i = 1,\quad w_i \geq 0\ \forall i
$$

This function ensures diversification and penalizes allocations toward high-risk or unstable assets during election periods.
$\lambda \$): Penalty term to control the influence of election-period shocks  

---

## Analysis Pipeline Summary

### Analysis 1: Long-Term Volatility Patterns
- File: `Master_Volatility_Index_Daily.csv`
- Computed normalized variance-based weights across six indexes during each 4-year election cycle (2000–2024)

### Analysis 2: Election-Phase Risk Dynamics
- Measured index volatility during Pre-Election, Election Month, and Post-Election windows
- Normalized weights per phase to understand phase-specific risk

### Analysis 3: Event Study with ARIMA and GARCH
- Pre-election model training (ARIMA/GARCH), post-election testing
- Calculated abnormal shocks and assessed significance using t-tests

### Analysis 4: Political Feature Engineering
- Encoded 7 election variables (e.g., Party Switch, Crisis, Electoral Score)
- Produced a structured dataset for ML training (`US_Presidential_Elections_2000–2024.csv`)

### Analysis 5: Machine Learning-Based Allocation
- Trained Random Forest on volatility and political features
- Output: Allocation weights that minimize a composite risk function as our objective function.
- Recommended allocations are inversely proportional to predicted risk.

---

## Tool Usage

1. Open `Analysis5.ipynb`
2. Enter your election scenario variables:
   - Winning Party
   - Incumbent Re-elected
   - Contested/Delayed
   - Party Switch
   - Electoral Score (1–5)
   - First-Term President
   - Crisis Year
3. The notebook will output optimized asset allocations and a pie chart for visualization.

---

## License

This repository is intended for academic, educational, and research purposes. Please contact the authors for permission to reuse any portion for commercial or public dissemination.

---
