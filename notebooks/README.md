# Time Series Analysis on OULAD Dataset

## Project Overview

This project demonstrates a comprehensive approach to time series forecasting using the Open University Learning Analytics Dataset (OULAD), incorporating both traditional statistical methods and modern machine learning techniques.

## Authors
- Seyyed Alireza Khoshsolat (D03000041)
- Farshad Farahtaj (D03000028)
- Zahra Jafarinejad (D03000083)

## University
University of Naples Federico II

## Course
Hardware and Software for Big Data (Module B)

## Instructor
Professoressa Flora Amato

## Key Takeaways

1. **Data Preprocessing is Crucial**:
   - Proper handling of anomalies and ensuring data stationarity are foundational steps for accurate forecasting.

2. **Model Selection**:
   - SARIMA and ARIMAX describe the weekly structure through their lag terms, Prophet fits trend and seasonality, and the CNN learns from 30-day windows. Only the CNN was scored on held-out days, so the notebook does not show which model forecasts best.

3. **Feature Engineering**:
   - The lag terms at 7, 14, 21 and 28 days are significant in the SARIMAX fit. No run without lags was made, so the notebook does not measure how much the lags improve forecasts.

4. **Model Evaluation**:
   - MAE and MAPE were computed for every model, but on different data: the CNN on a chronological hold-out, Prophet on its training data, and SARIMA and ARIMAX on mismatched dates (a forecast past the end of the data against the last observed days). Only the CNN number (MAE 0.20 on log clicks) is a real forecast score, and no naive baseline was run.

## Methodology

We used several time series forecasting techniques:

1. **SARIMA (Seasonal AutoRegressive Integrated Moving Average)**
2. **ARIMAX (AutoRegressive Integrated Moving Average with eXogenous variables)**
3. **Prophet (Facebook's forecasting tool)**
4. **CNN (Convolutional Neural Network)**

## Results

The project applies four forecasting models to daily student activity on the virtual learning environment. The CNN reached a mean absolute error of 0.20 on log daily clicks over the last 20% of days, held out in time order. The other models were not scored on the same hold-out, so they are not ranked against the CNN, and no naive baseline (for example the value from the same weekday last week) was run. See the main [README](../README.md) for the full list of limits.

## GitHub Repository

For the full project including code, data instructions, and complete documentation, please visit:
[github.com/Alirezakhoshsolat/time-series-OULAD](https://github.com/Alirezakhoshsolat/time-series-OULAD)
