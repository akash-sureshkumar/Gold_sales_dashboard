# Gold_sales_dashboard
##GOLD_ML IS THE FINAL FILE

 1. Importing Required Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from xgboost  import XGBRegressor
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import joblib
import plotly.express as px
pandas and numpy: Data processing and arrays

matplotlib.pyplot: Static visualizations

plotly.express: Interactive charts

XGBRegressor and LinearRegression: For model training

mean_squared_error: To evaluate prediction errors

joblib: For saving the model

 2. Load the CSV Dataset from GitHub
df = pd.read_csv('https://raw.githubusercontent.com/akash-sureshkumar/Gold_sales_dashboard/.../gold_sales_2023_2024.csv')
Loads your gold sales data for 2023 & 2024.

3. View Basic Dataset Info
print(" here is the dataset: ")
print(df.head())
print("\n info:")
print(df.info())
Shows first few rows and structure: columns, types, nulls.

 4. Convert 'Date' column to datetime
df['date'] = pd.to_datetime(df['Date'])
Creates a proper datetime column for analysis.

 5. Compare Product Sales Between Years
df['year'] = df['date'].dt.year
product_summary = df.groupby(['Product', 'year'])['Units_Sold'].sum().reset_index()
Groups sales by Product and Year → gets total units sold.

product_pivot = product_summary.pivot(index='Product', columns='year', values='Units_Sold').fillna(0)
Pivots the table to compare 2023 vs 2024 side-by-side.
 6. Plot Bar Chart Using Matplotlib
product_pivot.plot(kind='bar', figsize=(10,6))
...
plt.show()
Simple static bar chart of sales per product (2023 vs 2024).

7. Plot Bar Chart Using Plotly (Interactive)
fig = px.bar(product_summary,
             x='Product',
             y='Units_Sold',
             color='year',
             barmode='group',
             title="product sales 2023 vs 2024 (Interactive)")
fig.show()
Same as above, but allows interaction on hover, zoom, etc.

8. Save Cleaned Data (Optional)
df.to_csv("cleaned gold datasets", index=False)
Exports your cleaned version locally.

 9. Monthly Sales Analysis
df['Month'] = df['Date'].dt.to_period('M').dt.to_timestamp()
monthly_total=df.groupby('Month')['Units_Sold'].sum().reset_index()
monthly_by_prod=df.groupby(['Month','Product'])['Units_Sold'].sum().unstack()
This creates:

monthly_total: Total units sold each month

monthly_by_prod: Monthly product-wise breakdown

 10. Line Plot – Monthly Total Units Sold
plt.figure(figsize=(10, 5))
plt.plot(monthly_total['Month'], monthly_total['Units_Sold'], marker='o')
plt.title('Monthly Total Units Sold')
plt.show()
Shows overall sales trend month-by-month.

11. Prepare Data for ML Models
monthly_total['Month_Num'] = np.arange(1, len(monthly_total) + 1)
x=monthly_total[['Month_Num']]
y=monthly_total['Units_Sold']
Creates X & Y:

X = month number (1, 2, 3, ..., n)

Y = units sold

split=int(0.8*len(x))
x_train,x_test=x[:split],x[split:]
y_train,y_test=y[:split],y[split:]
Splits 80% training and 20% testing
 12. Train & Evaluate Models
lr=LinearRegression()
lr.fit(x_train,y_train)
...
print('LinearRegression Mean Squared Error:',mse)
Basic model (baseline).

xgb=XGBRegressor()
xgb.fit(x_train,y_train)
...
print(' XGB Mean Squared Error:',mse)
Powerful model for trend forecasting.

 13. Forecast Future Sales
future_nums = np.array([[len(x)+i] for i in range(1,4)])
future_preds = xgb.predict(future_nums)
Predict next 3 months based on the XGBoost model.

future_months = pd.date_range(start=monthly_total['Month'].max() + pd.offsets.MonthBegin(), periods=3, freq='M')
df_forecast = pd.DataFrame({'Month': future_months, 'Predicted_Sales': future_preds})
print(df_forecast)
Creates date labels for forecast months + predicted values.

 14. Plot Forecast vs Actual
plt.plot(monthly_total['Month'], monthly_total['Units_Sold'], ...)
plt.plot(df_forecast['Month'], df_forecast['Predicted_Sales'], ...)
plt.legend()
plt.show()
Shows:

Actual sales (solid line)

Forecast (dashed line)

 15. Save the Model
joblib.dump(xgb,'goldsales.joblib')
Stores model locally so it can be reused later.


