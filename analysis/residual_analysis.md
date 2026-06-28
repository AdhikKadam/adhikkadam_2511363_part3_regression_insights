# Residual Analysis

## Overview
Residuals represent the difference between the **actual monthly sales** and the **sales predicted by our multiple regression model** (`Residual = Actual - Predicted`). Analyzing these errors helps us identify stores that are unexpectedly overperforming or underperforming, and reveals potential blind spots in our model.

## Top 5 Positive Residuals (Overperformers)
These records represent stores where actual sales were significantly **higher** than what the model predicted based on their footfall, marketing, inventory, and store type.

| store_id   | month      | store_type   |   monthly_sales |   predicted_sales |   residual |
|:-----------|:-----------|:-------------|----------------:|------------------:|-----------:|
| STR-1073   | 2025-03-01 | Residential  |       813316.71 |         707767.97 |  105548.74 |
| STR-1030   | 2025-02-01 | Residential  |       820519.04 |         715770.95 |  104748.09 |
| STR-1028   | 2025-04-01 | Mall         |       713611.16 |         614751.11 |   98860.05 |
| STR-1032   | 2025-01-01 | High Street  |       914544.17 |         815726.57 |   98817.60 |
| STR-1050   | 2025-04-01 | Residential  |       735786.64 |         642285.15 |   93501.49 |

**Business Meaning:** These stores are generating a massive revenue premium that our operational inputs don't account for. Possible reasons include:
* **Exceptional Management & Conversion:** A highly effective store team converting more visitors or up-selling to much larger basket sizes.
* **Favorable Local Events:** Unrecorded local festivals, sports events, or conventions driving a highly concentrated burst of buying behavior.
* **Weak Local Competition:** These specific stores might enjoy a local monopoly, allowing them to capture outsized market share compared to similar stores.

## Top 5 Negative Residuals (Underperformers)
These records represent stores where actual sales were significantly **lower** than what the model predicted.

| store_id   | month      | store_type   |   monthly_sales |   predicted_sales |   residual |
|:-----------|:-----------|:-------------|----------------:|------------------:|-----------:|
| STR-1017   | 2025-03-01 | High Street  |       685379.08 |         844194.64 | -158815.56 |
| STR-1023   | 2025-02-01 | Mall         |       627171.90 |         749860.67 | -122688.77 |
| STR-1012   | 2025-01-01 | Residential  |       595467.60 |         713439.74 | -117972.14 |
| STR-1007   | 2025-02-01 | Mall         |       800451.94 |         902543.28 | -102091.34 |
| STR-1009   | 2025-01-01 | Residential  |       641865.03 |         743585.50 | -101720.47 |

**Business Meaning:**
Despite having the traffic, marketing, and inventory required to succeed, these stores are failing to convert at expected rates. Potential reasons include:
* **Poor Staff Performance / Understaffing:** The store has traffic, but poor service or long checkout lines are causing walk-outs.
* **External Disruptions:** Road construction blocking parking access, or highly aggressive promotions from a local competitor immediately next door.
* **Shrinkage/Theft:** High foot traffic combined with abnormally low sales could be an indicator of significant inventory loss or unrecorded transactions.

## Model Prediction Bias Evaluation
Looking at the residual distribution (see `residuals_preview.png`), we evaluate whether the model is systematically misjudging certain store profiles.
* **Random Scatter:** A healthy model shows residuals randomly scattered around the zero line, meaning errors are just noise.
* **Over-Predicting/Under-Predicting:** If the model consistently produced negative residuals for High Street stores, it would indicate we are over-predicting their success (perhaps missing a negative factor like declining city-center foot traffic quality). Conversely, if Airport stores consistently showed positive residuals, we might be under-predicting the inelastic purchasing behavior of travelers. 