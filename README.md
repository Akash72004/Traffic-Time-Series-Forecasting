# Traffic-Time-Series-Forecasting
Developed a time series forecasting model using ARIMA, SARIMA, Prophet (RMSE: 5.03–13.20), ARCH, and LSTM to predict hourly traffic at major junctions, achieving high accuracy with LSTM and Prophet in capturing seasonal patterns.


## 1.Introduction 
Traffic congestion is something we all experience, whether it’s during our daily commute or while running errands. It not only wastes time but also increases fuel consumption and contributes to air pollution. Accurate traffic forecasting can help address these challenges by enabling smarter urban planning and better traffic management.
In this project, we focus on predicting hourly traffic at four major junctions using historical data. The dataset spans over 14 months(November 2015 to December 2016), capturing vehicle counts at different times of the day. By analyzing this data, we aim to uncover patterns like daily rush hours, weekend dips, and unusual traffic spikes.
To achieve this, we’ve applied various time series models, including ARIMA, SARIMA, Prophet, and ARCH, each designed to handle specific aspects of time-dependent data. These models help us identify trends, seasonality, and irregularities, enabling us to generate accurate forecasts.
The ultimate goal of this project is to not only build reliable forecasting models but also provide insights that could be used to improve daily traffic flow, optimize signal timings, and reduce congestion. This isn’t just about numbers and predictions—it’s about making life easier for everyone on the road.

## 2.Data Description 
Dataset Overview
• DateTime: The date and time of each traffic record, essential for time-based analysis.
• Junction: ID of the junction where data was recorded, allowing analysis across multiple locations.
• Vehicles: The number of vehicles counted at each time interval, used as the main variable for traffic volume analysis.
• ID: A unique identifier for each row, created by combining date and time elements.

## 3.Data Cleaning
#### Handling Missing Values:
Checked for missing data, particularly in DateTime and Vehicles columns. For minor gaps, we used forward or backward fill, while larger gaps were either interpolated or, if excessive, dropped.
#### DateTime Formatting:
The DateTime column was converted to a datetime object, enabling easy extraction of time-based features like hour, day, and month, which are useful for capturing seasonal patterns.
#### Removing Duplicates:
Duplicate records were identified and removed based on DateTime and Junction to prevent distortion in traffic patterns.
#### Outlier Detection:
Used statistical methods like Interquartile Range (IQR) to identify and evaluate outliers in Vehicles, treating them based on whether they reflected genuine anomalies or noise.
#### Encoding Junctions:
The Junction column was one-hot encoded, allowing the model to recognize each junction distinctly and capture location-specific traffic patterns.

## 4. Data Decomposition 
Seasonal decomposition was applied to the dataset using an additive model with a period of 12, corresponding to monthly data. The decomposition plot shows the observed data along with its trend, seasonal, and residual components, allowing for a clearer understanding of the underlying patterns.

## 5. Testing Stationarity
The ADF test was conducted on the Vehicles column to evaluate stationarity. This test checks for the presence of a unit root in the series, indicating non-stationarity. The test outputs a p-value (should be < 0.05 for stationarity), ADF Statistic, and critical values at different significance levels (1%, 5%, 10%).
Initial results showed a p-value of 3.0889e-28, confirming that the data is stationary. The ADF statistic of -15.4148 was below the critical value for 1% significance, further reinforcing stationarity.
#### First-Order Differencing:
• To ensure strong stationarity and eliminate any residual trends, the first-order differencing was
applied to the Vehicles column, creating a new column Vehicle_diff.
• Differencing removes trends and seasonality, stabilizing the mean.

## 6. Model Forecasting and Analysis
#### 1. ARIMA (AutoRegressive Integrated Moving Average):
o ARIMA struggled to accurately predict traffic patterns across all junctions, especially during significant variations in the actual data.
o It performed better for smooth trends but lacked the ability to capture seasonality or sudden changes effectively.
Performance: Moderate, limited by the absence of seasonality handling.
#### 2. SARIMAX (Seasonal ARIMA with Exogenous Factors):
o SARIMAX consistently outperformed ARIMA by capturing both seasonal and trend components.
o It provided closer approximations to actual values during recurring patterns like hourly or daily peaks, making it effective for seasonal data.
o Performance: Strong, particularly for junctions with clear seasonality. 
#### 3. Prophet (Additive Model for Seasonality and Trend):
o Prophet showed high accuracy in capturing trends and seasonality.
o However, it sometimes overpredicted values during extreme variations, particularly for
Junctions 1 and 3.
o Prophet's flexibility and ease of implementation make it suitable for long-term traffic forecasting.
o Performance: Very strong, especially for datasets with clear seasonality and trends. 
#### 4. ARCH (Autoregressive Conditional Heteroskedasticity):
o ARCH performed poorly across all junctions, as it focuses on modeling volatility rather than trends or seasonality.
o While useful for datasets with high variance, it failed to predict actual traffic patterns effectively in this context.
o Performance: Weak, unsuitable for traffic forecasting in this project. Conclusion: Best Model
#### 5. LSTM (Long Short-Term Memory Neural Network):
• LSTM effectively captured complex temporal dependencies and performed well in modeling long-term trends and seasonal variations.
• It adapted well to non-linear patterns and outperformed traditional statistical models on volatile junctions.
• Performance: Very strong, especially in forecasting variable traffic flows with higher accuracy and stability.

## 7.Conclusion
Based on the comparison of actual and predicted values, SARIMAX, Prophet, and LSTM emerged as the best-performing models.
• SARIMAX excelled due to its ability to model both seasonality and trends, producing predictions that closely aligned with the actual traffic patterns.
• Prophet demonstrated strong performance with its intuitive handling of seasonal components and trends, though it slightly overpredicted in some cases.
• LSTM proved highly effective in capturing both short- and long-term dependencies, delivering robust results even in volatile traffic conditions.
