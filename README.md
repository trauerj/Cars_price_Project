# Car price estimator: Project Overview
* Created a [tool](https://github.com/trauerj/Cars_price_Project/blob/main/cars_project_model_building(preprocessing)%20(1).ipynb) that estimates car prices (MAE ~461K HUF) to help customers.
* Scraped over 1000 car descriptions from an online (used) car market(place) using python.
* Optimized Linear, Random Forest and Gradient Boosting Regressor using GridsearchCV to reach the best model.

## Code
* Python 3 (ipykernel)
* Packages: pandas, numpy, sklearn, matplotlib, seaborn, plotly, json, bs4, requests, csv, re, io

## Web Scraping
Write a web scraper to scrape thousands of car postings(/advertisments) from an online (used) car market(place). With each car, we got the following:
* Brand and model
* Type
* Dealerships' name
* Dealerships' location
* Dealerships' evaluation
* Production year
* km
* Price
* Horsepower
* Engine volume
* Condition
* Fuel type
* Transmission type
* etc.

## [Data cleaning](https://github.com/trauerj/Cars_price_Project/blob/main/cars_data_project_v1(cleaning).ipynb)
After scraping the data, I needed to clean it up so it was usable for our models. I made the following changes:
* Removed rows with Nan values
* Converted strings to numerics by removing words or letters
* Transformed production year to age of car
* Made a new column for brand, without model
* Made a new column for dealership location if (based on) its in the capital or not.
* Created a column for Yearly usage in km (Km/age)

## EDA
I checked the distribution of the data and looked for outliers with boxplot. I made further analysis using Excel.

## Model Building
First, I transformed the categorical variables into dummy variables. Second, I removed the outliers using the interquartile range (iqr) $`(q1 -1.5*iqr) < data < (q3 + 1.5*iqr)`$

After that i looked for the 21 most correlated features and made the models using just these features.

I also split the data into train and test sets with a test size 20% in both scenario.

I tried three different models:
* Linear Regression - Baseline for the model
* Random Forest Regressor
* Gradient Boosting Regressor

## Model performance
The Random Forest and the Gradient Boosting model performed as well on the test as on the validation sets. I got the following MAE values when the models used every features:

* Linear Regression: MAE = 575600
* Random Forest: MAE = 439177
* Gradient Boosting: MAE = 449898

I got the following MAE values when the models used the 21 most correlated features:

* Linear Regression: MAE = 601768
* Random Forest: MAE = 461680
* Gradient Boosting: MAE = 464518

### Comparison
As we can see from the table, the usage of the 21 most correlated features was reducing the average "accuracy" around 3-5%.

|      Model      | MAE with all features | MAE with most corralated features | Difference in HUF| Difference in %|
|----------------:|:-----:|:----:|:----:|:----:|
|Linear Regression|       575600          | 601768 | 26168 | + 4.5%|
|Random Forest    |       439177          | 461680 | 22503 | + 5.1%|
|Gradient Boosting|       449898          | 464518 | 14620 | + 3.2%|
