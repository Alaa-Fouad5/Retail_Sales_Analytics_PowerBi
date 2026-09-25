# Retail Performance & Executive Basket Analytics Dashboard

## Executive Summary

This project delivers an end-to-end commercial analytics dashboard built in Power BI, analyzing retail sales performance, branch basket efficiency, product margins, and return rate dynamics across enterprise sales channels.

The interactive dashboard provides actionable insights into sales revenue trends, high-volume drivers, operational return vulnerabilities, and branch-level performance variations to support executive decision-making.

<p align="center">
  <img src="Images/Excutive Sales Overview.png" alt="Executive Sales Overview" width="90%"><br>
  <em>Executive Sales Overview</em>
</p>

<p align="center">
  <img src="Images/Basket Analytics & Branch Efficiency.png" alt="Basket Analytics & Branch Efficiency" width="90%"><br>
  <em>Basket Analytics & Branch Efficiency</em>
</p>

<p align="center">
  <img src="Images/Profitability & Returns.png" alt="Profitability & Returns" width="90%"><br>
  <em>Profitability & Returns Matrix</em>
</p>

---

## Key Business Insights

* **Revenue Drivers & Concentration:** Over **91%** of overall gross profit is driven by three key product categories: **T-Shirts, Bottoms & Pants, and Outerwear**. The **Jeans** category represents the single largest revenue driver, generating **$256M** (28.66% of category revenue).
* **Store Revenue Dominance:** Top 3 performing branches account for **71.4%** of total revenue, led by **Branch 061** alone contributing **40.01%** ($43.91M out of top stores).
* **Return Rate Diagnostics:** Total business return rate stands at **11.74%**. Returns are disproportionately concentrated in the **Dresses & Sets** category (**18.55%** return rate) and select outlier stores (e.g., **Branch 158** at **26.95%**).
* **Basket Dynamics:** Average Units Per Transaction (UPT) stands at **1.94**, with an Average Order Value (AOV) of **$1.29K**. Cross-selling gaps show up to a **74%** variance in average invoice value between top and bottom-performing store staff.
* **Growth & Seasonality:** Monthly performance peaks significantly during seasonal and holiday periods, led by **May ($210M profit)** and **March ($166M profit)**, reflecting an average **11%** month-over-month sales growth trajectory.

---

## Dashboard Views Breakdown

### 1. Executive Sales Overview
* **Objective:** High-level strategic tracking of revenue, profit, monthly trends, and primary category drivers.
* **Key Visuals & Metrics:** 
  * **Top KPIs:** $1.56bn Total Revenue, $1.41bn Sales PM, $716.08M Total Profit, 46.03% Profit Margin, 1M Total Orders, $1.29K AOV.
  * **Revenue Distribution:** Donut chart highlighting top store shares (Branch 061 at 40.01%, Branch 086 at 16.16%, Branch 053 at 15.21%).
  * **Monthly Profit Trend:** Column chart showing May ($210M), Mar ($166M), Apr ($95M), Jun ($86M), Jan ($85M), and Feb ($74M).
  * **Top Categories Leaderboard:** Horizontal bar chart ranking revenue leaders: Jeans ($256M), Sweatshirts ($219M), T-shirts ($190M), Jackets ($119M), and Polo shirts ($91M).

### 2. Basket Analytics & Branch Efficiency
* **Objective:** Operational store evaluation and transaction basket dynamics.
* **Key Visuals & Metrics:** 
  * **Core KPIs:** Total Units Sold (2.34M), Units Per Transaction (1.94), Return Rate (11.74%).
  * **Store Operational Leaderboards:** Top stores ranked by UPT (Branch 127 at 2.80) and AOV (Branch 101 at 2,116).
  * **Product Scatter Matrix:** Units Sold vs. Profit Margin (%) identifying product clusters and margin outliers ranging from -50% to +150%.

### 3. Profitability & Returns Matrix
* **Objective:** Multi-dimensional root-cause analysis for return mitigation and category profitability optimization.
* **Key Visuals & Metrics:**
  * **Return Rate Leaderboard:** Outlier stores ranked by return rate (Branch 158 at 26.95%, Branch 089 at 25.11%, Branch 136 at 21.60%).
  * **Category Matrix Table:** Complete hierarchical breakdown across Total Revenue ($1.56Bn), Total Profit ($716.08M), and Return Rate (11.74%), calling out high-return risks (Dresses & Sets at 18.55%, Outerwear at 14.24%) and negative-profit categories (Sports Equipment at -$1,247.75).

---

## Data Architecture & Star Schema

The data model is structured using a standard Star Schema designed for optimal DAX query performance and analytical flexibility:

```text
                  +-------------------+
                  |   Dim_Calender    |
                  +-------------------+
                            |
                            | (1:N)
                            v
+------------------+     +-------------------+     +-------------------+
|   Dim_Branches   |---->|    Fact_Sales     |<----|   Dim_Products    |
+------------------+(1:N)+-------------------+(1:N)+-------------------+
                            ^
                            | (1:N)
                  +-------------------+
                  |     Category      |
                  +-------------------+

 Key Calculated DAX Measures

Below are core custom DAX measures implemented in the _Key_Measures table:

1. Average Order Value (AOV)

Average Order Value (AOV) = 
DIVIDE(
    [Total_Revenue], 
    [Total Orders], 
    0
)


2. Return Rate (%)

Return (%) = 
DIVIDE(
    [N_of_Transactions_Return], 
    [Total Orders], 
    0
)


3. Profit Margin (%)

Profit Margin (%) = 
DIVIDE(
    [Total_Profit], 
    [Total_Revenue], 
    0
)


4. Units Per Transaction (UPT)

Units Per Transaction (UPT) = 
DIVIDE(
    [Total Units Sold], 
    [Total Orders], 
    0
)


💡 Strategic Business Recommendations

Size & Quality Audit on High-Return Categories:

Initiate a quality control and sizing accuracy review on Dresses & Sets (18.55% return rate) and Outerwear (14.22% return rate) to reduce return volume and logistical overhead.

Branch Best-Practice Transfer:

Audit branch operational training in low-performing AOV locations to align cross-selling tactics with top-performing branches (e.g., Branch 018).

Low-Margin Product Portfolio Rationalization:

Re-evaluate pricing strategies or supplier costs for negative-margin categories (e.g., Sports Equipment at -1.25K net profit).

 How to Run This Project

Clone this repository:

git clone https://github.com/your-username/retail-performance-powerbi.git


Open the Dashboard:

Open the .pbix file using Power BI Desktop (August 2023 release or newer recommended).

Refresh Connection:

If prompted for data path, refresh connections to point to the local dataset stored in the /Data folder.

Created by Alaa Fouad — Senior Performance Data Analyst