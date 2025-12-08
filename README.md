<h1>Aggregated Volume Forecasting ML Model</h1>

<h2>Description</h2>

Developed a Time Series Forecasting pipeline using a Random Forest Regressor to predict aggregated monthly demand. The model focuses on high-level volume trends to support strategic S&OP planning, reducing signal noise found at granular SKU levels.

Unlike standard statistical models (ARIMA/ETS), this engine treats forecasting as a supervised regression problem, utilizing advanced feature engineering (Lags, Rolling Windows, Seasonality) to capture complex patterns in sales data. It employs a Recursive Multi-Step Forecasting strategy to predict 6 months into the future.

Key Features: 

- Automated Aggregation: Converts daily transactional data into monthly time-series data.
- Feature Engineering
- Seasonal Lag: Lag 12 (Year-over-Year seasonality).
- Rolling Statistics: 3-Month Rolling Mean (Smoothing/Trend detection).
- Recursive Forecasting: Uses a "feedback loop" where the model's prediction for Month t becomes an input feature for Month t+1.
- Advanced Evaluation Metrics: Calculates industry-standard metrics for evaluation.
- Business-Ready Reporting: Exports a formatted Excel dashboard with raw historical and forecast data & conditional formatting for performance metrics.
- Embedded Year-Over-Year seasonality plots.


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
   
- When predicting the future (where no actual data exists), the system uses its own previous predictions to fill the gaps.
- Predict Month 1.
- Append prediction to history.
- Re-calculate Lags and Rolling Means based on the new history.
- Predict Month 2.

5. Performance Metrics

The script evaluates accuracy using a comprehensive suite of metrics:

- MASE	Mean Absolute Scaled Error	
- RMSE	Root Mean Squared Error	
- MAPE	Mean Absolute % Error
- Bias	Mean Error
- WAPE   Weighted Absolute % Error
  
6. Automated export of Forecast vs Year-over-Year Actuals Graph & of Performance Metrics to excel, showing with conditional formatting whether model is good (or not) to use.
   
<h2>Tools used in this project:</h2>

- <b>Python</b> 
- <b>Pandas</b>
- <b>Numpy</b>
- <b>Matplotlib</b>
- <b>Seaborn</b>
- <b>sklearn</b>

<h2>Insights</h2>

✅ Bias Detection: In the model Mean Forecast Error was tracked to ensure that the model wasn't systematically over-forecasting or under-forecasting . This protects the organization from setting spending targets based on overly optimistic revenue projections (Preventing Cash Flow Risk).

✅ MASE: In the model was used Mean Absolute Scaled Error to prove that model outperformed the "Naive" baseline of the standard 'Last Year Actuals'. 

✅WAPE: In the model was used Weighted Absolute % Error to evaluate how model predicts the total volume of business. In our case the model achieved a WAPE of ~15% (implies ~85% Weighted Accuracy). This indicates that model successfully captured the main seasonality and trends, leaving only random noise as error.

Top-Down Budget Forecasting vs Actuals Year-Over-Year Graph: <br/>
<img src="https://i.imgur.com/qIA64VF.png" height="80%" width="80%" alt="Top-Down Budget Forecasting Year-Over-Year Graph"/>
<br />
<br />

Perfomance Metrics: <br/>
<img src="https://i.imgur.com/pMSN4pr.png" height="80%" width="80%" alt="Perfomance Metrics"/>
<br />
<br />
