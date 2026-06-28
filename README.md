# adhikkadam_2511363_part3_regression_insights
# Retail Store Performance - Regression Analysis Data Assessment

## Project Overview
This project aims to identify the key operational and strategic factors driving `monthly_sales` across our retail network. By understanding these drivers through regression analysis, leadership can optimize resource allocation (marketing, staffing, inventory) and refine store-level strategies.

---

## Data Understanding & Variable Classification

### 1. Dependent Variable (Target)
This is the primary metric we are trying to predict and understand.
* **`monthly_sales`**: The total sales revenue for a store in a given month.

### 2. Potential Independent Variables (Predictors)
These are the operational levers and environmental factors we will test to see how they impact sales.
* `marketing_spend`
* `footfall`
* `avg_discount_pct`
* `staff_count`
* `inventory_availability_pct`
* `competitor_distance_km`
* `holiday_flag`
* `customer_rating`
* `region`
* `store_type`

### 3. Numerical Variables
These represent measurable quantities. In regression, their coefficients will tell us the expected change in sales for a one-unit increase in the variable.
* **Continuous:**
  * `marketing_spend` ($)
  * `competitor_distance_km` (Distance)
  * `avg_discount_pct` (Percentage/Ratio)
  * `inventory_availability_pct` (Percentage/Ratio)
  * `customer_rating` (Scale 1-5)
* **Discrete:**
  * `footfall` (Count of people)
  * `staff_count` (Count of employees)

### 4. Categorical Variables
These represent qualitative groups and will require encoding before they can be used mathematically in a regression model.
* **Nominal (No inherent order):**
  * `region` (e.g., East, South)
  * `store_type` (e.g., Mall, High Street, Residential, Airport)
* **Binary/Boolean:**
  * `holiday_flag` (1 for holiday effect, 0 for none)

### 5. Variables Requiring Cleaning or Transformation
To build an accurate linear regression model, the following transformations should be considered:
* **Categorical Encoding:** `region` and `store_type` must be converted into dummy variables (One-Hot Encoding). We will need to drop one category from each to avoid perfect multicollinearity (the "dummy variable trap").
* **Temporal Feature Engineering (`month`):** The raw `month` date string (e.g., "2025-01-01") cannot be used directly. It should be transformed to extract seasonal features (e.g., a categorical `Quarter` variable or a `Month_of_Year` variable) to capture seasonality that isn't already explained by the `holiday_flag`.
* **Multicollinearity Checks:** We should check the correlation between variables like `marketing_spend` and `footfall`. If they are highly correlated (marketing directly drives footfall), including both might distort their individual coefficient estimates. We may need to interact them or drop one.

### 6. Variables Not Useful for (or detrimental to) the Regression
* **`store_id`**: This is a unique identifier with high cardinality. Unless we are conducting a complex panel data analysis with fixed effects, including it as a standard categorical variable will overfit the model and provide no actionable business insights.
* **`monthly_profit`**: While important, profit is an *outcome* of sales minus costs, not a *predictor* of sales. Including it as an independent variable would cause severe data leakage (endogeneity) and ruin the regression model's ability to explain the actual operational drivers of revenue.