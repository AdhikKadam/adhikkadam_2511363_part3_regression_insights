# Regression Model Comparison

This document compares the simple and multiple regression models developed to analyze the drivers of `monthly_sales`.

## 1. Simple Regression Model (Marketing)
* **Model name:** Simple Linear Regression (Marketing Spend)
* **Variables used:** * Dependent: `monthly_sales`
  * Independent: `marketing_spend`
* **R-squared:** 0.704
* **Significant variables:** `marketing_spend` (p-value < 0.05)
* **Business usefulness:** Provides a quick, high-level estimate of marketing ROI. It is easy to explain to stakeholders ("$4.89 in sales for every $1 spent").
* **Limitations:** Suffers from severe omitted variable bias. It ignores critical operational realities like foot traffic, inventory levels, and location type.

## 2. Simple Regression Model (Footfall)
* **Model name:** Simple Linear Regression (Footfall)
* **Variables used:**
  * Dependent: `monthly_sales`
  * Independent: `footfall`
* **R-squared:** 0.736
* **Significant variables:** `footfall` (p-value < 0.05)
* **Business usefulness:** Extremely useful for setting baseline store targets based on mall or high street traffic expectations.
* **Limitations:** It tells us the value of a customer walking in, but doesn't tell us *how* to get them to walk in (which requires marketing or better locations).

## 3. Multiple Regression Model (Comprehensive)
* **Model name:** Multiple Linear Regression (Operational Drivers)
* **Variables used:**
  * Dependent: `monthly_sales`
  * Independent: `marketing_spend`, `footfall`, `inventory_availability_pct`, `store_type` (Dummy variables)
* **R-squared:** 0.820
* **Significant variables:** `marketing_spend`, `footfall`, `inventory_availability_pct`, `store_type_Residential`, `store_type_High Street`
* **Business usefulness:** Highly actionable for strategic planning. It isolates the effect of keeping shelves stocked (inventory) vs. driving traffic, while normalizing for store location types.
* **Limitations:** Introduces multicollinearity (Marketing and Footfall are correlated), which slightly muddies the pure isolated effect of marketing. 