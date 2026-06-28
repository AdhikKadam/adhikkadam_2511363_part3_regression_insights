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

---

# Retail Store Performance: Regression Analysis Project

## 1. Business Problem Summary
The leadership team of our retail chain wants to understand the primary factors driving monthly sales performance across our store network. By identifying which operational levers (e.g., marketing spend, inventory availability, footfall) and structural factors (e.g., store type) have the strongest association with revenue, the business can optimize its strategy, reallocate resources efficiently, and maximize overall profitability.

## 2. Dataset Description
The analysis utilizes a dataset of monthly store performance metrics (`business_regression_data.xlsx`), containing over 300 observations across 50 stores. The dataset includes a mix of numerical operational metrics (marketing spend, footfall, inventory percentages) and categorical store attributes (region, store type).

## 3. Dependent and Independent Variables
* **Dependent Variable (Target):** `monthly_sales` (The total monthly revenue we are trying to predict and understand).
* **Independent Variables (Predictors):** 
  * *Operational:* `marketing_spend`, `footfall`, `inventory_availability_pct`, `staff_count`, `avg_discount_pct`
  * *Categorical/Structural:* `store_type`, `region`, `holiday_flag`

## 4. Regression Approach
We employed a staged approach to linear regression:
1. **Simple Linear Regression:** We initially tested variables in isolation (e.g., Sales vs. Marketing Spend; Sales vs. Footfall) to understand their raw, unadjusted impact on revenue.
2. **Multiple Linear Regression:** We combined the strongest numerical predictors and categorical factors into a single comprehensive model. This allowed us to isolate the specific impact of one variable while holding all other variables constant (e.g., the value of marketing *assuming* footfall and inventory remain the same).

## 5. Dummy Variable Approach
Machine learning and statistical models require numerical inputs. To include the categorical variable `store_type` (Airport, High Street, Mall, Residential), we used **One-Hot Encoding** to create "Dummy Variables" (1 for yes, 0 for no). 
* **Reference Category:** We dropped the "Airport" category to serve as our mathematical baseline (avoiding the "dummy variable trap" of perfect multicollinearity). Consequently, the coefficients for High Street, Mall, and Residential represent their performance *relative* to an Airport store.

## 6. Model Comparison Summary
* **Simple Model (Marketing Only):** R-squared = 0.704. Showed a $4.89 return on every marketing dollar, but suffered heavily from omitted variable bias.
* **Simple Model (Footfall Only):** R-squared = 0.736. Showed that a single visitor is worth ~$35.68, making it a stronger standalone predictor than marketing.
* **Multiple Regression Model:** R-squared = 0.820. By combining Marketing, Footfall, Inventory, and Store Type, the model's explanatory power jumped to 82%, offering a much more accurate reflection of operational reality.

## 7. Final Model Selected
We selected the **Multiple Regression Model** as our final analytical tool. Relying on the simple models would have been dangerously misleading—for instance, assuming marketing directly creates sales without recognizing that marketing's primary function is to drive footfall, and footfall only converts if inventory is available. The multiple regression model correctly balances these overlapping realities.

## 8. Business Recommendation
1. **Prioritize Supply Chain & Inventory:** Maintaining high `inventory_availability_pct` is critical. Out-of-stocks are bleeding revenue from customers already in the store. We recommend tying manager bonuses to stock availability during peak hours.
2. **Optimize Marketing for Footfall:** Marketing budgets should be evaluated strictly on their ability to drive physical foot traffic, as footfall is the ultimate conversion engine.
3. **Investigate Residential Stores:** Residential locations severely underperform compared to the baseline (-$39.6k penalty). Leadership must investigate the merchandising strategy and basket sizes in these specific locations to close the gap.

## 9. Assumptions and Limitations
* **Association, not Causation:** Regression proves that variables move together, but it does not prove *why*. (e.g., Do high-performing stores get bigger marketing budgets, or does the marketing budget cause the high performance?).
* **Multicollinearity:** Marketing spend and footfall are highly correlated. Including both slightly blurs their isolated mathematical impacts.
* **Omitted Variables:** The model explains 82% of sales variance, leaving 18% unexplained. Uncaptured factors like local macroeconomic health, competitor pricing, or management quality are likely responsible for the remaining variance.
* **Linearity:** The model assumes a straight-line relationship (constant returns to scale), whereas the real world often experiences diminishing returns (e.g., pushing inventory from 98% to 99% might cost more than the revenue it generates).

## 10. Screenshots Included
Evidence of this analysis can be reviewed in the generated image files:
* `simple_regression_output.png`: Scatter plot and line of best fit for Marketing vs. Sales.
* `multiple_regression_output.png`: Actual vs. Predicted sales plot demonstrating the high accuracy of the final model.
* `model_comparison_preview.png`: Bar chart contrasting the explanatory power (R-Squared) of the different models.
* `residuals_preview.png`: Error analysis plot highlighting stores that overperform or underperform our model's expectations.


