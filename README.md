<h1>Demand Forecasting Machine Learning Model</h1>

<h2>Description</h2>

This project implements a robust Time Series Forecasting pipeline using Machine Learning (Random Forest Regressor) to predict future monthly sales demand.

Unlike standard statistical models (ARIMA/ETS), this engine treats forecasting as a supervised regression problem, utilizing advanced feature engineering (Lags, Rolling Windows, Seasonality) to capture complex patterns in sales data. It employs a Recursive Multi-Step Forecasting strategy to predict 6 months into the future.

Key Features: 

- Automated Aggregation: Converts daily transactional data into monthly time-series data.
- Feature Engineering: Automatically generates:Lag Features: Lag 1, Lag 2 (Short-term trends).
- Seasonal Lag: Lag 12 (Year-over-Year seasonality).Rolling Statistics: 3-Month Rolling Mean (Smoothing/Trend detection).
- Recursive Forecasting: Uses a "feedback loop" where the model's prediction for Month t becomes an input feature for Month t+1.
- Advanced Evaluation Metrics: Calculates industry-standard metrics including MASE (Mean Absolute Scaled Error) and SMAPE (Symmetric Mean Absolute Percentage Error).
- Business-Ready Reporting: Exports a formatted Excel dashboard with:Raw historical and forecast data.Conditional formatting for performance metrics.Embedded Year-Over-Year seasonality plots.


Methodology & Logic :

- Data Preprocessing: The script accepts raw transactional data, parses dates, and aggregates volume by month end (ME).
- The Model: Random Forest
   
Random Forest is ideal for this application because:

- It handles non-linear relationships well.
- It is robust against overfitting compared to single decision trees.
- It does not require scaling/normalization of data.

3. Feature Engineering
To turn a time-series problem into a supervised learning problem, we create a shifting window of features

4. Recursive Forecasting Loop
   
When predicting the future (where no actual data exists), the system uses its own previous predictions to fill the gaps.
Predict Month 1.
Append prediction to history.
Re-calculate Lags and Rolling Means based on the new history.
Predict Month 2.

5. Performance Metrics

The script evaluates accuracy using a comprehensive suite of metrics:

- MASE	Mean Absolute Scaled Error	
- SMAPE	Symmetric MAPE	
- MAPE	Mean Absolute % Error
- Bias	Mean Error

<h2>Tools used in this project:</h2>

- <b>Python</b> 
- <b>Pandas</b>
- <b>Numpy</b>
- <b>Matplotlib</b>
- <b>Seaborn</b>
- <b>sklearn</b>

<h2>Insights</h2>

✅ Bias Detection: In the model Mean Forecast Error was tracked to ensure that the model wasn't systematically over-forecasting (bloating inventory) or under-forecasting (causing stock-outs).

✅ MASE (Mean Absolute Scaled Error): In the model was used MASE to prove that model outperformed the "Naive" baseline. 

✅ SMAPE: Real-world sales data is messy and sometimes have extreme outliers. In the model thus, was used SMAPE, a robust metric designed specifically to handle intermittent demand and keeping the forecasting engine running smoothly 100% of the time, regardless of whether were sold 1,000 units or 0 units.

Forecasting vs Actuals Year-Over-Year Graph: <br/>
<img src="https://i.imgur.com/qIA64VF.png" height="80%" width="80%" alt="Forecasting vs Actuals Year-Over-Year Graph"/>
<br />
<br />

Perfomance Metrics: <br/>
<img src="https://i.imgur.com/wymo6St.png" height="80%" width="80%" alt="Perfomance Metrics"/>
<br />
<br />
