#  Ethereum Gas Spend Analysis (Dune Analytics)

This project analyzes Ethereum blockchain activity using **Dune Analytics**, focusing on the **top gas-spending wallets** over the past 30 days.

---

##  Project Overview

- **Platform**: [Dune Analytics](https://dune.com)
- **Network**: Ethereum Mainnet
- **Query Tool**: PostgreSQL-style SQL
- **Visualization**: Dune dashboards (bar chart, table)

---

##  Objective

To identify the top 50 wallets that spent the most on Ethereum gas fees in the past 30 days, and visualize this data using Dune Analytics.

---

##  Key Query

```sql
SELECT
  tx."from" AS wallet_address,
  SUM(CAST(tx.gas_used AS NUMERIC) * CAST(tx.gas_price AS NUMERIC) / 1e18) AS total_eth_spent,
  COUNT(*) AS txn_count
FROM
  ethereum.transactions tx
WHERE
  tx.block_time >= now() - interval '30 days'
GROUP BY
  wallet_address
ORDER BY
  total_eth_spent DESC
LIMIT 20;
```

##  Visualization

The dashboard includes:

Bar chart of wallet addresses vs total ETH spent on gas

Table of wallet, transaction count, and ETH spent

Line chart of wallet addresses vs tnx count

### Live Dashboard: https://dune.com/ivykhalid/top-gas-spenders-on-ethereum-30-days
