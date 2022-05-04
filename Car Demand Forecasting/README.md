# Car Rentals Demand Forecasting ( Analytics Vidhya Job-A-Thon April 2022)
https://datahack.analyticsvidhya.com/contest/job-a-thon-april-2022/

## Problem Statement
ABC is a car rental company based out of Bangalore. It rents cars for both in and out stations at affordable prices. The users can rent different types of cars like Sedans, Hatchbacks, SUVs and MUVs, Minivans and so on.

In recent times, the demand for cars is on the rise. As a result, the company would like to tackle the problem of supply and demand. The ultimate goal of the company is to strike the balance between the supply and demand inorder to meet the user expectations. The company has collected the details of each rental. Based on the past data, the company would like to forecast the demand of car rentals on an hourly basis.

## Objective
The main objective of the problem is to develop the machine learning approach to forecast the demand of car rentals on an hourly basis.
  
## Approach
### Exploratory Data Analysis
  - Training data contains only date, hour & demand columns. We had to create additional features from the given date column.
  - Also, date and hour columns have non continuios data. So, we cannot use regular time series forecasting models like ARIMA, SARIMA etc.,
  - We can convert the panel data (time series) into normal data which is required for traditional regression models
  - Created month, day, week_of_year, day_of_week, quarter & other time related features from the date column
  - Since, car demand will be high during weekends compared to weekdays, we can create a is_weekend column from day_of_week
  - Car data is collected in Karnataka state, Using holidays pacakge loaded Karnataka holidays data for the year 2018 to 2022. As car demand will be in peak, during public holidays
  - Distribution of hour v/s demand confirms that hour has varying impact on demand. Grouped hour into categories like Early Morning, Morning, Afternoon etc.,
  - Applied Sine & Cosine transformations on cyclic features like hour of day, day of week & month of year

### ML Modelling
  - Calculated Variance Inflation factor using statsmodels library and dropped highly collinear features ['month', 'quarter', 'weekofyear', 'hour', 'day_of_week', 'is_weekend'] from the training data
  - Splitted data into Training (70%) & Validation (30%)
  - Fitted ML models Ridge, Linear Regression, LighGBM, CatBoost, XGBoost, RandomForest, DecisionTree on Training data
  - Evaluated the performance of the above ML models on Training & Validation data using regression metrics RMSE, R2 score
  - LightGBM model performed better than the other models (low bias and low variance)
  - Applied all required transformations on Test set and predicted Car demand using LightGBM model
