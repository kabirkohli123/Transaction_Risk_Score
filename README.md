# Transaction_Risk_Score

This project implements a wallet risk scoring model for on-chain wallet addresses by analyzing their interaction with the Compound V2/V3 protocol. It provides a data-driven framework to evaluate the riskiness of Ethereum wallets based on their historical transaction patterns.

---

## 📌 Overview

Given a list of Ethereum wallet addresses, the pipeline:
- Retrieves historical transaction data
- Extracts and engineers key features
- Scores each wallet on a risk scale from **0 to 1000**
- Outputs results as a CSV for further analysis or integration

---

## ⚙️ How It Works: The Methodology

### 1. 📥 Data Collection & Preparation
- Transaction data for each wallet was fetched by exporting CSVs from [Etherscan](https://etherscan.io).
- All files were combined into `combined_transactionsNew.csv`.
- Preprocessing steps included:
  - Standardizing timestamps to readable datetime formats
  - Removing irrelevant columns (e.g., status, nonce)
  - Handling missing values and ensuring numeric consistency

### 2. 🔧 Feature Engineering
Key indicators extracted per wallet:

| Category | Feature Examples |
|----------|------------------|
| **Activity Metrics** | Total transaction count, wallet age, first/last activity |
| **Financial Behavior** | Total value_in/out (ETH), net balance, high-value transaction ratio |
| **High-Risk Signals** | Count of failed transactions, liquidations, contract interactions |

A summarized feature set per wallet was then built using grouped aggregates.

### 3. 🧮 Risk Scoring Pipeline

- **Normalization**: All features scaled to [0, 1] using min-max normalization.
- **Weighted Scoring**: A weighted sum is computed. High-value features like `liquidation_count` contribute negatively, while stable features like `wallet_age` contribute positively.
- **Final Scaling**: Score is scaled from [0, 1] to a 0–1000 range where:
  - `0` = Low risk
  - `1000` = High risk

---

## 📄 Files Included

| File | Description |
|------|-------------|
| `combined_transactionsNew.csv` | Raw transaction data for all wallets |
| `RiskScore.ipynb` | Notebook with full scoring pipeline and visualizations |
| `wallet_risk_scores_optimized.csv` | Final output with wallet addresses and risk scores |
| `Combining_CSVs.ipynb` | Script used to concatenate individual Etherscan CSV exports |

---

## 📊 Example Output

| wallet_id | score |
|-----------|-------|
| `0xfaa0768bde629806739c3a4620656c5d26f44ef2` | `732` |
| `0xabc123...` | `421` |

---

## 📈 Visualizations

- **Score Distribution**: Histogram showing how risk is distributed across the wallets
- **Correlation Matrix**: Feature importance and how they influence the score

---

## 🚀 Future Work

- Integrate live fetching via Web3 or The Graph APIs
- Add smart contract interaction risk labels (e.g., Ponzi schemes, mixers)
- Build a real-time dashboard for monitoring wallet risk scores


## 👤 Author

**Kabir Kohli**  
B.Tech Automation & Robotics  
University School of Automation & Robotics  
