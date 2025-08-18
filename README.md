# 📊 Gold Sales Analysis & Forecasting (2023–2024)

This project focuses on analyzing and forecasting **gold product sales** using Python and Machine Learning.  
The goal is to compare sales trends across years, visualize insights, and build forecasting models for both overall and product-specific sales.

---

## 🔹 Project Overview
- Cleaned and prepared gold sales data (2023–2024).
- Created features like **Year** and **Month** for time-based analysis.![Uploading 1st one.png…]()

- Visualized:
  - Product sales comparison (2023 vs 2024)
  - Monthly total sales trends
  - Forecast vs actual sales
- Built forecasting models:
  - **Linear Regression** (baseline)
  - **XGBoost Regressor** (performed better with lower MSE)
- Forecasted:
  - Total sales for the next **3 months**
  - Product-specific sales for the next **6 months**
- Saved trained models using **joblib**.

---

## 🔹 Tech Stack
- Python  
- pandas, numpy  
- matplotlib, plotly  
- scikit-learn  
- XGBoost  
- joblib  

---

## 🔹 Visualizations
Some examples of insights generated:

1. **Product Sales Comparison (2023 vs 2024)**  
  
2. **Monthly Sales Trends**  
   ![Monthly Sales Trends](screenshots/monthly_sales_trend.png)

3. **Actual vs Forecasted Sales**  
   ![Forecasted Sales](screenshots/forecast_vs_actual.png)

*(Create a folder named `screenshots/` and add these plots as `.png` files for better README display.)*
