# EV_Adoption_Forecasting
EV Adoption Forecasting


Overview

This project presents an end-to-end workflow for forecasting electric vehicle (EV) adoption using historical registration data. It provides insights for urban planners and policymakers to anticipate EV infrastructure demand, such as charging stations, aiding in smart and sustainable city planning.

Objective: Build a regression model to forecast county-level EV adoption for the next three years.

Dataset: Monthly vehicle registration counts (2017-01-31 to 2024-02-29) from the Washington State Department of Licensing, including BEVs, PHEVs, non-EVs, and total vehicles, categorized by county and primary vehicle use.

1. Dataset Description
   

  <img width="725" height="361" alt="image" src="https://github.com/user-attachments/assets/0bf979ac-0015-4098-b089-32daba7e0618" />




2. Data Exploration & Preprocessing

Data inspected for nulls and converted all count columns to numeric.

Missing County and State values imputed as 'Unknown'.

Outliers in Percent Electric Vehicles capped using the interquartile range (IQR) method.

All date strings parsed to datetime objects.

Counties encoded numerically for modeling.

Sample Data

<img width="671" height="204" alt="image" src="https://github.com/user-attachments/assets/549db647-7b44-4952-98d8-14553c5e5a70" />



Date	County	State	EV Total	Non-EV Total	Percent EVs
2022-09-30	Riverside	CA	7	460	1.50
2020-01-31	Dakota	MN	1	32	3.03
2022-06-30	Ferry	WA	0	3,575	0.00


3. Feature Engineering
Temporal: Extracted year, month, numeric date, and months since first registration per county.

Lags/Rolling Metrics: Added 1–3 month lags and 3-month rolling averages for EV totals.

Growth Rates: Calculated month-over-month and 3-month percentage change in EV totals.

Trend: Computed 6-month rolling linear slope (ev_growth_slope) for cumulative EV adoption.

4. Modeling & Evaluation
Model Used: Random Forest Regressor (sklearn)

Tuning: Hyperparameters optimized using RandomizedSearchCV with cross-validation.

Train/Test Split: 90% train, 10% test — no data shuffling to maintain time series order.

Metrics:

Mean Absolute Error (MAE)

Root Mean Squared Error (RMSE)

R² Score

Performance

<img width="611" height="204" alt="image" src="https://github.com/user-attachments/assets/9d096069-5744-44ee-99d5-c5815b831c25" />


5. Forecasting
Single County Forecast
Generates a 3-year monthly forecast for any specified county, using the last 6 months of historical data as input lags.

Example: Kings County showed a doubling trend in cumulative EVs from 2024–2027, supporting the need for increased charging infrastructure.

Top-5 County Forecast
Model automatically forecasts the next 36 months for all counties.

Identifies and visualizes the top 5 counties by projected cumulative EV adoption (e.g., Santa Clara, Fairfax, Orange, Honolulu, Los Angeles).

Reveals varied growth rates—some counties plateau, while others accelerate, depending on historical adoption patterns.

6. Model Insights
Top Predictors: 2-month lag of EV total, 1-month lag, and the growth slope—highlighting the importance of recent trends and momentum.

Moderate Predictors: Percent changes and 3-month lag.

Lesser Features: Pure time index, county encoding, and short-term rolling averages were less influential.

7. Usage
Dependencies

<img width="640" height="339" alt="image" src="https://github.com/user-attachments/assets/dc5395c3-4edd-46fa-89ad-49e62d702c2f" />


Training and Inference
Training: Run end-to-end data cleaning, feature engineering, model training, and evaluation.

Saving/Loading: Save the trained model with joblib.dump() and reload with joblib.load().

Prediction: Provide the required features (including lags and rolling metrics) for future periods to receive adoption forecasts.

8. Planning Implications
Consistent, rapid EV growth in leading counties underscores urgent needs for charging stations, electricity grid upgrades, and support services.

Forecasts enable proactive and data-driven infrastructure planning for maximum user satisfaction and sustainability progress.

9. Reproducibility
Ensure all dependencies are installed as listed above.

Download the dataset from the provided Kaggle link and place it in your project directory.

Follow the cell order outlined above for proper preprocessing, modeling, and forecasting.
