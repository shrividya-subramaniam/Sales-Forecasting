# Sales-Forecasting
Solution to Analytics Vidhya Job-a-thon September 2021. This notebook achieved 15th rank in the private leaderboard.

![image](https://user-images.githubusercontent.com/58010969/143678814-6ee912c8-1eac-4e08-90eb-76ab74d56da1.png)



## Problem Statement
WOMart is a leading nutrition and supplement retail chain that offers a comprehensive range of products for all your wellness and fitness needs. The retail chain follows a multi-channel distribution strategy with 350+ retail stores spread across 100+ cities.

Effective forecasting for store sales gives essential insight into upcoming cash flow, meaning WOMart can more accurately plan the cashflow at the store level. Sales data for 18 months from 365 stores of WOMart is available along with information on Store Type, Location Type for each store, Region Code for every store, Discount provided by the store on every day, Number of Orders everyday etc.

Your task is to predict the store sales for each store in the test set for the next two months.

## Data Dictionary

### Train Data
Variable | Definition
--- | ---
ID | Unique identifier for a row
Store_Id | Unique id for each store
Store_Type | Type of the store  
Location_Type | Type of the location where the store is located
Region_Code | Code of the region where the store is located
Date | Information about the date
Holiday | If there is holiday on the given date, 1: Yes, 0: No
Discount | If discount is offered by the store on the given date, Yes/No
#Orders | Number of orders received by the store on the given date
Sales| Total sale for the store on the given date

### Test Data
Variable | Definition
--- | ---
ID | Unique identifier for a row
Store_Id | Unique id for each store
Store_Type | Type of the store  
Location_Type | Type of the location where the store is located
Region_Code | Code of the region where the store is located
Date | Information about the date
Holiday | If there is holiday on the given date, 1: Yes, 0: No
Discount | If discount is offered by the store on the given date, Yes/No

## Data Pre-processing
- Day, day of the week, month, year and weekend features are extracted from the Date column. 
- Categorical Columns like Store Type, Location Type, Region Code and Discount are encoding using one-hot encoding (pd.get_dummies). 
- The Store Id is a column with high cardinality with 365 unique values. Hence, it is encoded with target encoding as label encoding and one-hot encoding are unsuitable. 

### Feature Generation
The following features are generated.
1. 'Holiday_weekend’ and 'Holiday_weekday’-for holiday on a weekend and holiday on a weekday. These are useful as sales tends to be higher on holidays. 
2. 'Dateinbetween25and5’- whether the day of sale falls between 25th of the previous month and 5th of the following month. This is the time period when people receive their salaries. Therefore, buying will be higher in this period. 


## Evaluation Metric
The competition evaluation metric used is (**mean squared log error**) MSLE*1000. 

## Approach
To predict the total sale for each store, linear regression, XGBoost and LightGBM models are tried. However, XGBoost model outperforms the linear regression and LightGBM model with a better MSLE value during model evaluation. Therefore, XGBoost model is used to predict the sales values in the test data. 

## Leaderboard
!Public Leaderboard(https://datahack.analyticsvidhya.com/contest/job-a-thon-september-2021/#LeaderBoard):19th Rank
!Private Leaderboard(https://datahack.analyticsvidhya.com/contest/job-a-thon-september-2021/#LeaderBoard):15th Rank

