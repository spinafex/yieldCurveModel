# Treasury Yield Forecasting Project

Project Overview
This project aims to forecast the 10-year US Treasury yield (ust10y) and the yield curve slope (slope_10y_2y, defined as the difference between the 10-year and 2-year Treasury yields) over a 20-working-day period starting in late April 2025. Additionally, it classifies daily changes in the yield curve slope as steepening, flattening, or unchanged. The forecasts provide insights into future interest rate trends and yield curve dynamics, which are critical for financial planning, investment strategies, and economic analysis.
Goals:
Generate accurate 20-day forecasts for ust10y and slope_10y_2y using historical Treasury yield and inflation data.

Classify daily slope_10y_2y changes to identify yield curve trends.

Produce a comprehensive report summarizing model performance, forecast results, visualizations, and limitations.

Deliver all outputs (forecasts, models, report, plots) in a structured format for stakeholders.

Approach
The project follows a structured machine learning pipeline implemented in Python, leveraging libraries like pandas, scikit-learn, and matplotlib. The approach consists of 10 steps:
Data Collection: Sourced historical daily data on Treasury yields (1-month to 30-year) and inflation expectations (1-year to 30-year) from reliable financial databases.

Data Preprocessing: Cleaned data, handled missing values, and computed slope_10y_2y as ust10y - ust2y. Created lagged features (e.g., ust10y_lag1, slope_10y_2y_lag5) and differenced features (e.g., ust10y_diff1) to capture temporal dynamics.

Feature Engineering: Generated additional features, including lagged yields, inflation expectations, and their differences, to enhance model predictive power.

Exploratory Data Analysis (EDA): Analyzed correlations, trends, and seasonality in yields and slopes to inform feature selection and model design.

Model Selection: Chose Random Forest models for their robustness to non-linear relationships and feature interactions:
Regression models for ust10y and slope_10y_2y.

Classification model for slope_change (steepening, flattening, unchanged).

Model Training: Trained Random Forests on historical data, using features like slope_10y_2y_lag1 (98.43% importance for slope_10y_2y), lagged yields, and inflation metrics. Applied hyperparameter tuning to optimize performance.

Model Evaluation: Assessed models on a test set, analyzing residuals, RMSE for regression, and accuracy/confusion matrix for classification. Identified inaccuracies in volatile periods (e.g., August–October 2024 for ust10y, August 2024–January 2025 for slope_10y_2y).

Forecasting: Generated 20-day forecasts by iteratively predicting ust10y and slope_10y_2y, updating lagged features with prior predictions, and adding random perturbations to prevent convergence. Produced 90% confidence intervals and classified slope_change.

Report Generation: Created a detailed report summarizing model performance, forecast trends, visualizations (plots of ust10y and slope_10y_2y), and limitations.

Final Output: Consolidated outputs into an output directory, including forecast results (forecast_results.csv), trained models (.pkl files), report (forecast_report.md), and plots (.png files).

Lessons Learned
Feature Importance: The high importance of slope_10y_2y_lag1 (98.43% for slope_10y_2y) led to initial forecast convergence, highlighting the need to balance feature influence with randomization to maintain dynamic predictions.

Model Sensitivity: Random Forests effectively captured non-linear patterns but struggled with volatile periods (e.g., August 2024–January 2025), suggesting time series models might complement the approach.

Data Quality: Accurate preprocessing (e.g., handling missing values, computing lags) was critical to model performance, emphasizing the importance of robust data pipelines.

Iterative Forecasting: Iterative prediction with lagged feature updates required careful implementation to avoid feedback loops, addressed by capping initial jumps and adding perturbations.

Communication: A clear, comprehensive report with visualizations and limitations was essential for stakeholder understanding, reinforcing the value of interpretable outputs.

Final Result
The project successfully generated 20-day forecasts for April 29, 2025, to May 26, 2025:
10-Year Yield (ust10y):
Range: 4.2650% to 4.4259%.

Trend: Fluctuated between 4.26% and 4.43%, reflecting market uncertainty with no clear directional bias.

Confidence Interval: Wide (~4.13%–4.58%), indicating model uncertainty.

Yield Curve Slope (slope_10y_2y):
Range: 0.5130% to 0.5368%.

Trend: Varied between 0.51% and 0.54%, suggesting a stable yield curve with slight fluctuations.

Confidence Interval: Moderately wide (~0.46%–0.59%).

Slope Change Classification:
Distribution: Mostly unchanged (16 days), with 2 days each of steepening and flattening.

Observation: The ±0.01 threshold for classification limited sensitivity to small slope changes.

Outputs:
forecast_results.csv: Forecast table with ust10y, slope_10y_2y, confidence intervals, and slope_change.

rf_ust10y.pkl, rf_slope.pkl, rf_slope_change.pkl: Trained Random Forest models.

forecast_report.md: Comprehensive report with model performance, forecast analysis, visualizations, and recommendations.

ust10y_forecast.png, slope_10y_2y_forecast.png: Plots of forecasted values with confidence intervals.

The results are plausible for financial forecasting, providing actionable insights into yield trends and yield curve dynamics, though wide confidence intervals and classification sensitivity suggest areas for refinement.
Potential Different Approaches
To enhance or explore alternative solutions, consider the following approaches:
Time Series Models:
ARIMA/SARIMA: Use autoregressive integrated moving average models to capture temporal dependencies and seasonality in ust10y and slope_10y_2y, potentially improving performance during volatile periods.

LSTM/GRU: Implement recurrent neural networks to model long-term dependencies, leveraging sequential data for more robust forecasts.

Hybrid Models:
Combine Random Forests with ARIMA residuals to capture both non-linear feature interactions and time series trends, balancing complexity and interpretability.

Feature Expansion:
Incorporate macroeconomic indicators (e.g., GDP growth, unemployment rates, Fed policy signals) or market sentiment data (e.g., VIX, equity indices) to enrich feature sets and improve forecast accuracy.

Dynamic Confidence Intervals:
Compute rolling variance-based confidence intervals instead of static tree-based intervals to reflect changing uncertainty across the forecast horizon.

Ensemble Methods:
Use gradient boosting (e.g., XGBoost, LightGBM) or stacking to combine multiple models, potentially reducing reliance on slope_10y_2y_lag1 and improving generalization.

Alternative Classification Thresholds:
Lower the slope_change threshold (e.g., ±0.005) or use probabilistic outputs to capture subtler yield curve dynamics, enhancing classification sensitivity.

These approaches could address limitations like wide confidence intervals, model sensitivity to specific features, and inaccuracies during volatile periods, offering more robust and precise forecasts.
Notes








