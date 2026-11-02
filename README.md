# SuperKart Sales Forecasting

Predicts next-quarter product sales for a four-outlet supermarket chain using
multiple linear regression, then turns the model into store-level expansion and
inventory recommendations.

- **Notebook (code, analysis and findings):** [`SuperKart_Solution_Notebook_Machine_Learning__Project.ipynb`](SuperKart_Solution_Notebook_Machine_Learning__Project.ipynb)

## Problem

SuperKart runs supermarkets and food marts in Tier 1–3 cities. It shared one
quarter of sales records (8,763 product–store rows, 12 columns) and wanted a
model to forecast total sales for the next quarter, so it could plan operations
and inventory by city tier.

## Approach

1. **Exploratory analysis.** Revenue by outlet, product type, sugar content,
   store size and city tier.
2. **Feature engineering.** Store age derived from the establishment year.
   Sixteen product types grouped into perishables and non-perishables. Product
   ID prefixes used as a category.
3. **Preparation.** Outlier review, one-hot encoding, and a multicollinearity
   check (features with VIF > 5 dropped).
4. **Modeling.** OLS regression (statsmodels). Insignificant variables
   (p > 0.05) were removed and the model refit.
5. **Validation.** Linear-regression assumptions checked (mean residuals,
   homoscedasticity, linearity, normality), plus 10-fold cross-validation.

## Results

| Model | Train RMSE | Test RMSE | Test MAE | Test R² |
|---|---|---|---|---|
| OLS, all features | 446.7 | 446.7 | 266.7 | 0.790 |
| **OLS, significant features only** | **446.7** | **446.8** | **266.8** | **0.790** |

Cross-validated R² was 0.823 (± 0.045). Train and test scores are almost
identical, so the model is not overfitting. The simpler model was kept because
it matches the full model's accuracy with fewer variables.

## Business recommendations

| Outlet | Profile | Quarter revenue | Recommendation |
|---|---|---|---|
| OUT004 | Supermarket Type 2, Tier 2, medium | 15.4M (highest) | Expand the store's size; open stores in comparable cities |
| OUT003 | Departmental store, Tier 1, medium | 6.7M | Premium store: target marketing at the right audience |
| OUT001 | Supermarket Type 1, Tier 2, high | 6.2M | Underperforming for its size: discounts and offers to drive traffic |
| OUT002 | Food mart, Tier 3, small | 2.0M | Strong for its size: upgrade it, or replicate it in similar cities |

Fruits and vegetables and snack foods drive the most revenue across all
outlets, so their inventory should never run short. Customer demographics and
festive-season calendars would improve future forecasts.

## Data

The SuperKart dataset was provided by the course and is not included here.

## Tools

Python, Pandas, NumPy, statsmodels, scikit-learn, Matplotlib, Seaborn
