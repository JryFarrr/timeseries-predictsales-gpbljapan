## Overview Problem 
Forecasts aren’t just for meteorologists. Governments forecast economic growth. Scientists attempt to predict the future population. And businesses forecast product demand—a common task of professional data scientists. Forecasts are especially relevant to brick-and-mortar grocery stores, which must dance delicately with how much inventory to buy. Predict a little over, and grocers are stuck with overstocked, perishable goods. Guess a little under, and popular items quickly sell out, leading to lost revenue and upset customers. More accurate forecasting, thanks to machine learning, could help ensure retailers please customers by having just enough of the right products at the right time.

Current subjective forecasting methods for retail have little data to back them up and are unlikely to be automated. The problem becomes even more complex as retailers add new locations with unique needs, new products, ever-transitioning seasonal tastes, and unpredictable product marketing.

## Potential Impact
If successful, you'll have flexed some new skills in a real-world example. For grocery stores, more accurate forecasting can decrease food waste related to overstocking and improve customer satisfaction. The results of this ongoing competition, over time, might even ensure your local store has exactly what you need the next time you shop.

## Evaluation
The evaluation metric for this competition is Root Mean Squared Logarithmic Error.

## About Data
Time series data with range
- January 1, 2013, to August 15. 2017 for train data
- August 16, 2017 to August 31, 2018 for test data
The goal is to predict sales for product families sold in data test
Have some additional data like oil, price, holiday/event, and store

## Workflow
1. Data preparation
2. Data Preprocessing
Focussing attention on :
- Events (holiday, oil, etc..)
- Periodic parameters (by week, by month)
Adding and editing variables
- Merge and align the datas
- Fill out the missing oil value using scipy.interpolate (method = linear)
3. Feature engineering
- Make a new feature: Average per Store, Average sales per Month
- The reason is to decrease noise and small fluctuations so the model can easily see the trend of data
- Another reason is to normalize data, so the model can be learned with same scale
- The correlation between the products with promotion and those without is very big. So we make a new feature named
is_promotion
- We use moving averages to identify the trends, reducing noise and outliers so the model can learn easily based on the mean value in past time.
4. Modelling
- RANDOM FOREST
REGRESSION 
Decision Tree: Each Node has question and the answer
connects to another node
Ex. Is it holiday? Is the oil value above 50?  Is the family_mean value above 100? Many branch make regression more accurate. The aim of Preprocessing was to make data fit into decision tree

How it work:
- Step 1: split data into many pieces (120 pieces for this project)
- Step 2: each data of pieces were put into corresponding decision tree
- Step 3: Take mean of decision tree values to predict value For classification, we do majority vote instead of taking mean.
![image](https://github.com/user-attachments/assets/1a108671-6134-48e0-9f18-81e76e6faa6d)
![image](https://github.com/user-attachments/assets/33d8626f-d752-4e32-bc5b-de9d7f3356b5)

Characteristics :
Pros
- Effective to multi-variate data (characteristic of decision tree based model)
- takes less time (than XGBoost)
- Easy to implement using Scikit-Learn
Cons
- Less accurate than XGBoost (still accurate than Linear Regression though)
- Difficult to deal with missing values (Decision Tree Model Problem)

We tried to use linear regression at first, but since the data is multivariate, we decided to use random-forest-regressor as our main model.

## RESULTS
Using RandomForestRegressor
Kaggle : about 0.61974

## Comparison
Using XGBoost (learning rate = 0.1)
In notebook : 1.3250
Kaggle score : 0.98921
Using LightGBM (learning rate = 0.01)
In notebook : 1.5813
