# Midcontinent Independent System Operator Load Analysis

## Data Preprocessing Steps
* Checked for missing values
* Handled Date attribute
* Time based interpolation for all attributes
* Analyzed attribute statistics

## Visualizations & Error Metrics
### MISO Load Comparison from 2018-2024
![Untitled](https://github.com/user-attachments/assets/9c1c1a11-ad61-424e-8db5-870c81fdb596)

### Error Metrics for MISO Load from 2018-2024
> Forecasting Error Metrics:

> Mean Absolute Error: 1476.56 MW

> Mean Percentage Error: -0.28%

> Mean Absolute Percentage Error: 1.96%

The Forecasting Error metrics show that the forecasting load overestimates the demand slightly with an average error of 1476.56 MW. The accuracy of the forecasting error is quite good at 1.96%

> Clearing Error Metrics:

> Mean Absolute Error: 1819.54 MW

> Mean Percentage Error: 0.97%

> Mean Absolute Percentage Error: 2.44%

The Clearing error metrics show that the clearing load tends to underestimate the demand. The accuracy for the clearing error is slightly higher at 2.44%, indicating there is more room for improvement in clearing predictions compared to forecasting

### Visualizing Load for the first month of 2018
![Untitled](https://github.com/user-attachments/assets/dad48e75-86e3-43c9-8647-0e0b32c88cf1)

The beginning of the month shows high consumption which is indicative of colder weather. By the end of the month energy consumption slows down to a normal range

### Visualizing Load Prediction Errors for the first month of 2018
![Untitled](https://github.com/user-attachments/assets/e6cbb98d-c5fc-48db-bb84-489b894978e4)

The forecasting error seems to have more descrepancies throughout the month than the clearing error; the differences between the two indicate there may be some unusual conditions taking place during the month

### Analyzing Average Error patters by hour of day for 2018-2024
![Untitled](https://github.com/user-attachments/assets/c44b6c86-714e-4066-9e39-b9c85c367dd1)

During the first four hours and last three hours of the day there is a visible difference between the mean forecasting error and the mean clearing error.
The forecasting error suggests the model is over-predicting demand during these hours. The clearing error suggests the system is underestimating the load during these hours. This misalignment can lead to overproduction & unnecessary costs in ensuring supply matches actual demand

## ARIMA: Model Processing
### Checking Stationarity of Actual Load
> ADF Statistic: -4.557427886008111

> p-value: 0.0001546330460577187

> Critical Values:

>   1%: -3.43320007524933

>   5%: -2.8627990992000947

>   10%: -2.567440275533058

> Conclusion: Actual Load is Stationary (reject H0)

### Checking Stationarity of Differenced Actual Load
> ADF Statistic: -9.593159091612169

> p-value: 2.0107231291480706e-16

> Critical Values:

>   1%: -3.4332075478242547

>   5%: -2.8628023988345044

>   10%: -2.5674420323448883

> Conclusion: Differenced Actual Load is Stationary (reject H0)

### ACF of Differenced Actual Load
![Untitled](https://github.com/user-attachments/assets/a413281d-2833-42cc-9f58-c8373eea0a2c)

### PACF of Differenced Actual Load
![Untitled](https://github.com/user-attachments/assets/16852ae4-5bdb-4210-a8db-2ff3a28137ee)

### ARIMA: SARIMAX Results
![image](https://github.com/user-attachments/assets/8dc9bea0-d5c9-4209-abb4-131f7129a020)

The model fits okay, but there are some issues with residuals. The Ljung-Box tests suggests the model isn't fully capturing the time-series structure. The Jarque-Bera test shows that the residuals aren't normally distributed. Conclusion: It might be better to use a seasonal model like Prophet

## Prophet: Model Performance
> Mean Squared Error: 26457540.21

> Root Mean Squared Error: 5143.69

> Mean Absolute Error: 3855.77

> Mean Absolute Percentage Error: 4.96%

> Root Mean Squared Error as percentage of mean: 6.87%

## MISO Forecast Performance 
> Mean Squared Error: 1195431.86

> Root Mean Squared Error: 1093.35

> Mean Absolute Error: 843.38

> Mean Absolute Percentage Error: 1.11%

> Root Mean Squared Error as percentage of mean: 1.46%

## Comparison of Prophet vs MISO vs Cleared Load Forecast Prediction
![Untitled](https://github.com/user-attachments/assets/5c02a242-2352-4bd7-8036-00b70a395bd9)

## Comparison of Prophet vs MISO vs Cleared Load Mean Absolute Percentage Error
![Untitled](https://github.com/user-attachments/assets/fce9db62-5958-4203-be23-06390d76cf77)

## Tuning Prophet
Best parameters after tuning:
- changepoint scale = 0.005
- seasonality scale = 10
- seasonality mode = additive

## Prophet: Best Parameters Performance
> Mean Squared Error: 23899887.68

> Root Mean Squared Error: 4888.75

> Mean Absolute Error: 3699.41

> Mean Absolute Percentage Error: 4.81%

Very slight decrease in MAPE after tuning the model, this suggests there maybe some data missing or further tuning needs to be done

## Comparison of Best Prophet Model vs MISO 
![Untitled](https://github.com/user-attachments/assets/22f4dba9-b234-40a1-9fe3-4ed03ac5b442)

## RMSE & MAPE Comparison of Prophet vs Best Prophet vs MISO vs Cleared Load
![Untitled](https://github.com/user-attachments/assets/33b806da-e673-40aa-a81d-66d6c5a074d5)

## Seasonality Trends
### Seasonality Trends for January 2023
![Untitled](https://github.com/user-attachments/assets/664fc2ab-b8c0-4b81-b971-ec75699c9126)

### Weekly Trends for January 2023
![Untitled](https://github.com/user-attachments/assets/d14f80ff-fe43-4b0e-a1e5-2f048bfc26be)

### Forecasting Error for January 2023
![Untitled](https://github.com/user-attachments/assets/515a49b5-4e9a-46a5-b9f7-6e0f0363605c)

## Summary of Findings
![image](https://github.com/user-attachments/assets/4b5a8a92-1271-48bd-9cac-156acd4c2623)








