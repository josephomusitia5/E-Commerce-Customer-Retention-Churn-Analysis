# E-Commerce Customer Retention & Churn Analysis

## Business Context
Understanding customer lifecycle dynamics is critical for sustainable e-commerce growth. This project analyzes a dataset of 180 customers and 607 orders to uncover insights into customer retention, churn risks, and lifetime value (LTV). 

The primary objective of this analysis is to move beyond surface-level metrics and deliver **"honest reporting."** This means actively correcting for common data anomalies—such as messy acquisition channel entries, missing time-series gaps, and incomplete current-month data—to provide stakeholders with reliable, actionable business intelligence.

## Technical Stack & Skills Demonstrated
* **SQL Dialect:** SQLite
* **Key Techniques:** 
  * Data cleaning and standardization on the fly using `CASE` statements.
  * Handling time-series data gaps using `WITH RECURSIVE` CTEs.
  * Advanced aggregations, dimensional modeling, and cohort bucketing.

---

## 1. Data Quality & Standardization (Before & After)
Real-world data is rarely clean. The raw acquisition channel data contained fragmented, inconsistent entries (e.g., 'referral', 'Referral ', 'ref'). 

### Before: Raw, Unstandardized Data
![Raw Data](screenshots/01_messy_data.png)

### After: Standardized with SQL CASE WHEN
Using a `CASE WHEN` statement, I cleaned and grouped these fragments into 5 distinct, trackable business categories to ensure accurate LTV and retention calculations.
![Clean Data](screenshots/02_clean_data.png)

---

## 2. Preventing Misleading Trend Reporting
A common reporting trap is graphing a time series where "zero-sales" months simply disappear, or plotting the current, incomplete month as a massive revenue drop. 

### Month-Over-Month Revenue Trend
*(Generated using a recursive CTE to build a continuous calendar sequence, ensuring months with zero sales appear accurately as $0, and explicitly dropping the current incomplete month.)*
![Revenue Trend](screenshots/03_revenue_trend.png)

---

## 3. Churn Analysis & Risk Factors
While tracking revenue is important, understanding *who* is leaving and *why* is where the action happens. By segmenting churn rates across different acquisition channels, a surprising risk factor emerged.

### Churn Rate by Channel
![Churn Analysis](screenshots/05_churn_analysis.png)

**Key Finding:** Customers acquired via Email campaigns exhibited an unusually high churn rate of 80%. This counter-intuitive insight suggests that our current email promotions might be attracting one-time discount hunters rather than building long-term loyalty, signaling a need to rethink our email retention strategy.

---

## 4. Customer Lifetime Value (LTV) by Channel
By joining customer demographic data with their lifetime order totals (and explicitly filtering out "window shoppers"), we can see which acquisition channels bring in the most valuable long-term customers.

### LTV Findings
![LTV by Channel](screenshots/04_ltv_results.png)

**Key Finding:** Referral channels drove an average LTV of $857, compared to just $299 for Social Media. This strongly indicates that future marketing spend should be reallocated to incentivize customer referrals.

---

## Repository Structure
* `data/`: Contains the raw dataset (Orders and Customers CSV files).
* `sql/`: Contains the `.sql` files for each step of the analysis.
* `screenshots/`: Visual assets for documentation.
