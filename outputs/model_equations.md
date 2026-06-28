# Business Drivers: Model Equations & Explanations

## 1. Simple Regression Models (Single Drivers)
These models look at a single operational lever in isolation to see its raw impact on monthly sales.

**Model A: Marketing Spend**
`Expected Monthly Sales = $429,623.51 + ($4.89 × Marketing Spend)`
* *Meaning:* For every $1 we put into marketing, we generate roughly $4.89 in top-line sales, before factoring in any other operational realities.

**Model B: Footfall**
`Expected Monthly Sales = $446,410.58 + ($35.68 × Footfall)`
* *Meaning:* For every single person who walks through our doors, we generate an average of $35.68 in revenue.

---

## 2. The Comprehensive Multiple Regression Model
Because our business doesn't operate in a vacuum, we need a model that evaluates multiple levers working at the same time. 

**Full Equation:**
`Expected Monthly Sales = $146,200 + ($1.18 × Marketing Spend) + ($33.68 × Footfall) + ($3,062.93 × Inventory Availability %) - ($22,960 if High Street) - ($39,650 if Residential) - ($11,310 if Mall)`

---

## 3. Breaking Down the Business Levers (Coefficients)
The "coefficients" are simply the multipliers that show the estimated dollar-value impact of changing an operational lever by one unit.

* **Marketing Spend ($1.18):** When we account for the fact that marketing's main job is driving footfall, the *direct* bonus of marketing drops to $1.18 per dollar spent. This implies that while marketing is profitable, its true power lies in getting people through the door.
* **Footfall ($33.68):** Even when adjusting for marketing and location, the value of a single visitor remains extremely stable at ~$33.68. This is our core conversion/basket size metric.
* **Inventory Availability ($3,062.93):** For every 1% improvement in keeping items fully stocked, a store makes an extra $3,062. This highlights that out-of-stocks are severely hurting our revenue. 

---

## 4. Understanding Store Locations (Dummy Variables)
In data modeling, we cannot plug words like "High Street" into a math equation. We convert them into "Dummy Variables"—which are essentially on/off switches (1 or 0) for each location type. 

**The Reference Category: "Airport"**
To make the math work, we must leave one category out of the equation to act as our baseline. We used **Airport** stores as our reference category. Therefore, all other store types are evaluated *in comparison to Airport stores*.

* **Residential (-$39,650):** Compared to an Airport store with the exact same footfall and inventory, a Residential store will make about $39,650 less per month.
* **High Street (-$22,960):** Compared to an Airport store, a High Street location brings in roughly $23k less per month. 
* **Mall (-$11,310):** While Malls appear to make $11k less than Airport stores, this specific metric lacked statistical significance. From a business perspective, Mall and Airport locations perform relatively similarly when traffic is equalized.

---

## 5. Final Model Selection & Recommendation
**Final Selection:** The Multiple Regression Model.

**Reasoning:** We must base our business strategy on the Multiple Regression model because the simple models are misleading. If we only looked at the Simple Marketing model, leadership might assume marketing alone guarantees a 5x return ($4.89 per $1). However, the Multiple Regression reveals the operational truth: marketing primarily drives *footfall*, and if we don't have the **inventory availability** on the shelves when that footfall arrives, the sales won't materialize. 

The Multiple Regression model provides a 360-degree view, proving that our strongest growth strategy requires a balanced approach: using marketing to drive traffic, while heavily investing in our supply chain to ensure a 99%+ inventory availability rate.