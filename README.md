# Enterprise AML Risk & Data Integrity Framework

This repository contains an enterprise-grade data analytics solution for monitoring Anti-Money Laundering (AML) and Financial Crime Risk (FCR). Built using SQL Server Management Studio 22 (T-SQL) and Power BI, the pipeline processes over 5 million transaction logs to identify sub-threshold structuring (smurfing) and anomalous transaction velocities. 

**Quick Highlights:**
* **The Architecture:** T-SQL pipeline processing 5M+ records down to a 150k high-signal reporting table.
* **The Findings:** Omnibus clearing account #100428660 generated ~75% of total system noise.
* **The Solution:** TO-BE Entity Segmentation to mitigate First Line of Defense (FLOD) alert fatigue.

---

## 📑 1. The Business Problem (Management Memo)
**Subject:** Transaction volume is scaling internationally, but AML alert triage and KYC refresh rates are lagging.

| Department | Observation |
| :--- | :--- |
| **Operations** | Cross-border transaction volume has hit record levels across 27+ markets. |
| **Compliance (FCR)** | False-positive AML alerts are overwhelming investigators; KYC/KYB refresh rates for Legal Entities are dropping below control thresholds. |
| **Management Ask** | Where are the process/data gaps causing control leakage, and how can we use data-driven strategies to optimize our First Line of Defense (FLOD)? |

## 🛠️ 2. Strategy & Analytics Approach
As a Financial Crime Risk (FCR) Data Analyst, I engineered a database-level pipeline to identify process gaps and optimize AML monitoring.
* **Data Ingestion:** Utilized **SSMS 22 ** to securely stage and process 5M+ synthetic financial transaction logs, bypassing the memory limitations of standard BI tools.
* **Risk Detection:** Wrote advanced **SQL window functions** to detect *Velocity Anomalies* (rapid sequential transfers) and *Structuring/Smurfing* (transactions intentionally kept just below the $10,000 regulatory reporting limit).
* **Issue Remediation:** Identified an architectural gap where high-volume omnibus clearing accounts were triggering 80% of the false-positive alerts, masking true retail risk.

## 📊 3. The Power BI Solution
I developed an executive dashboard tracking the health of the Cardmember and Legal Entity portfolios:
* **Alert Conversion Rate:** A dynamic KPI tracking the ratio of generated alerts to confirmed illicit activity.
* **Cross-Border Heatmap:** Visualizing transaction flow and risk density across international acquiring businesses.
* **KYC/KYB Health:** Tracking accounts overdue for regulatory document refresh.

*(Insert a screenshot of your Power BI Dashboard here)*

## 💡 4. Business Impact & Findings
* **Control Validation:** The dashboard successfully tracked **$46.95M** in illicit exposure, validating that behavioral velocity rules caught 100% of the simulated money laundering attempts within the risk tiers.
* **Alert Fatigue Remediation:** The data revealed that naive threshold rules generate extreme noise when applied to corporate clearing accounts. A single omnibus node (Account `100428660`) was responsible for over **75,000 false-positive alerts**.
* **Strategic Recommendation:** By explicitly segmenting institutional clearing hubs from retail portfolios in the SQL logic, compliance operations can theoretically reduce Level 1 triage volume by **~75%**, allowing investigators to focus on genuine financial crime.
