**Online Retail Sales Forecasting with PySpark**

This project applies PySpark to analyze daily sales patterns in the Online Retail dataset and forecast product demand for operational planning.
The goal is to support e-commerce Sales & Operations Planning (S&OP) teams by predicting daily quantities sold and estimating expected demand for a specific promotional week in 2011.

The workflow integrates data engineering, feature extraction, machine learning, and forecasting using the PySpark MLlib library.

E-commerce inventory planning heavily depends on accurate demand forecasting.
This project demonstrates how PySpark can be used to:

Process large-scale retail transaction data

Aggregate sales into daily intervals

Build a predictive model for Quantity sold

Evaluate model accuracy using Mean Absolute Error (MAE)

Estimate expected sales volume for Week 39 of 2011

All results are generated from the real Online Retail dataset.

**Dataset**

The dataset used in this project is:

Online Retail (Transactional e-commerce sales data)

It has been hosted externally in the link below:

https://www.kaggle.com/datasets/munemshariarshams/online-retail

Includes the following key fields:

InvoiceNo

StockCode

Description

Quantity

UnitPrice

InvoiceDate

CustomerID

Country

The dataset covers sales from 2010–2011 across multiple international markets.

The file Online Retail.csv may be large; include it in the repo only if desired.
Otherwise, provide a dataset link or request access.

**PySpark Workflow**

**1. Initialize Spark Session**

Used to load the CSV and execute distributed transformations.

**2. Convert and Extract Date Features**

InvoiceDate is converted to a timestamp, and date-related fields are extracted:

Year

Month

Day

Week number

Day of week

**3. Aggregate to Daily Sales**

Transactions are grouped by:

Country
StockCode
InvoiceDate
Year
Month
Day
Week
DayOfWeek

and summed to obtain daily Quantity sold.

**4. Train/Test Split**

Data is split using this rule:

Training set: <= 2011-09-25

Testing set: > 2011-09-25

The training set is exported as:

pd_daily_train_data.csv

**Feature Engineering**

Categorical fields encoded using PySpark MLlib:

Country → CountryIndex

StockCode → StockCodeIndex

**Final feature vector:**

CountryIndex
StockCodeIndex
Month
Year
DayOfWeek
Day
Week

**Model: Random Forest Regressor**

A PySpark RandomForestRegressor is used to predict Quantity.
The model is trained using the prepared training dataset, and predictions are generated for the test period.

**Model Evaluation**

The main evaluation metric is:

Mean Absolute Error (MAE)

Computed over the test data.

Your project’s MAE:

mae = 5.3733223088180875

This value is stored in the repository:

mae.csv

**Forecasting Sales for Week 39 of 2011**

Using the model’s predictions, total units expected to be sold during Week 39 (2011) are calculated.

Your forecasted volume:

quantity_sold_w39 = 87946

Stored in the repository:

quantity_sold_w39.csv

**Files Included**

| File Name | Description |
|----------|-------------|
| `Retail_Forecasting_PySpark.ipynb` | Main PySpark notebook containing data processing, feature engineering, model training, evaluation, and forecasting. |
| `pd_daily_train_data.csv` | Daily-aggregated training dataset (all records up to 2011-09-25). |
| `mae.csv` | Contains the Mean Absolute Error (MAE) calculated on the test predictions. |
| `quantity_sold_w39.csv` | Predicted total units expected to be sold in Week 39 of 2011. |
| `README.md` | Full project documentation and explanation. |


**Key Insights**

Daily sales forecasting helps balance inventory availability and operational cost.

Product demand shows strong variability by country, stock code, and weekday.

The model provides reliable early indicators for promotional planning weeks.

**Final Outputs**

Output	Files:

Training dataset	pd_daily_train_data.csv

Mean Absolute Error (MAE)	mae.csv

Forecast for Week 39 of 2011	quantity_sold_w39.csv

All outputs were generated using the real dataset and saved for reproducibility.
