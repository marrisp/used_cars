# Predicting the factors impacting the used car prices being expensive/low using regression

This project was part of an assignment for a Machine Learning course. The Vehicle Data is included in the repository and was sourced from Kaggle. 

The Jupyter Notebook contains the code used to complete the following regression analysis.
https://github.com/marrisp/used_cars/blob/main/prompt_II.ipynb


# Business Understanding
The car dataset will be used to gain insights into key drivers for used car prices.

The following analysis will clarify which vehicle features positively or negatively impact a car's value (price). Understanding the correlation between the vehicle features and the resulting prices will create a predictive model to price vehicles the dealership lists for sale accurately. Additionally, understanding desirable vehicle traits will allow the dealership to make more informed inventory decisions.



# Understanding the data
The first step of this project was to understand the data. The data set contained nearly 427k records and included the following vehicle features:

Vehicle Features: id, price, year, manufacturer, model, condition, cylinders, fuel, title_status, transmission, VIN, drive, size, type, paint_color, and state

Time was spent looking through the unique values of each feature, particularly the categorical columns such as manufacturer, model, and fuel

A price distribution histogram gave a quick overview of the vehicle pricing and quickly identified outliers. When reviewing the top 50 and bottom 50 vehicles by price, I found a Ford Escape/Dodge/Volvo valued at higher prices which are invalid. Additionally, have restricted the dataset where price ranging between $500 and $175500



# Data Preparation

In addition to outlier cleaning from the data understanding process, converted categorical data into numeric values using the label encoder instead of OneHotEncoder. Once categorical data was enumerated, an additional data type conversion of odometer and year to int64 was completed.

Removed NaN rows, also removed the rows for fuel, transmission, condition having the value as 'other'.

The new, clean data was placed into a new dataframe called "cleansed_copy_df" and inspected for correctness.

After previewing the cleaned car data, the data was scaled using the Standard Scaler. A quick review of the scaled data was conducted, including creating a simple Correlation Matrix for initial data testing.

# Data Modeling
The cleaned data was divided into target and feature (X and y), and then split into test and training data. I began with a simple linear regression model, followed by a ridge regression model, and ended with a Lasso Regression, including cross-validation, created a scatterplot of each model to visualize the results of these models. Below is the scatterplot of predicted vs actual prices for the Lasso Regression model.

predictedvsactual for LinearRegression
<img width="989" alt="Screen Shot 2024-02-20 at 8 54 48 PM" src="https://github.com/marrisp/used_cars/assets/153134781/1ff3acb0-26dc-4d36-9ef2-01d403881570">

Bar Chart for Ridge Regression

<img width="988" alt="Screen Shot 2024-02-20 at 8 56 34 PM" src="https://github.com/marrisp/used_cars/assets/153134781/bc5e7d1d-300e-45c1-9f3a-463b9de5f7d3">

predictedvsactual for Ridge Regression

<img width="1008" alt="Screen Shot 2024-02-20 at 8 57 22 PM" src="https://github.com/marrisp/used_cars/assets/153134781/276f63a6-b0a2-4291-8933-cdcdd5cc73d1">


predictedvsactual for LASSO
<img width="978" alt="Screen Shot 2024-02-20 at 8 58 31 PM" src="https://github.com/marrisp/used_cars/assets/153134781/85f299af-1b14-4e2f-a3ed-723344d0ea38">



Below is a bar chart clearly illustrating the weights of the features:

important features

# Evaluation
I calculated the results of each model and found that all three regression models determined the year, cylinders, odometer and fuel features as most important, although in varying orders of importance. The Lasso Regression model performed the best, although the others performed similarly well.

<img width="400" alt="Screen Shot 2024-02-20 at 9 00 12 PM" src="https://github.com/marrisp/used_cars/assets/153134781/90bf041a-4e7e-450f-949e-5ddeb8481ffa">



# Deployment
Based on the evaluation of the data models, the following features have the greatest importance for predicting value:

Most Important Features

Year
Cylinders (12, 10, 8, 6, 4, 3)
Odometer (mileage)
Fuel (diesel, gas, hybrid, electric)

The graph below has been filtered to only include vehicles from 1995 until the present. Trend lines for the vehicle price by year have poor predictability, as these vehicles fall into one of two extremes: classic collector vehicles or cars that are likely most valuable as scrap.
<img width="990" alt="Screen Shot 2024-02-20 at 9 01 50 PM" src="https://github.com/marrisp/used_cars/assets/153134781/14453b8b-815a-45fe-a56a-f84d48b697e5">


While fuel type impacts price, it is worth noting that most of the vehicles in this dataset were gas-powered.

Price by Fuel

<img width="991" alt="Screen Shot 2024-02-20 at 9 02 48 PM" src="https://github.com/marrisp/used_cars/assets/153134781/cc6a6af3-bda5-44e1-955c-5c349a382885">


The manufacturer was not included as a top correlating factor to price, but knowing the most popular vehicle manufacturers and their associated pricing spread should be another helpful tool for your inventory strategy.

Price by Manufacturer
<img width="981" alt="Screen Shot 2024-02-20 at 9 03 57 PM" src="https://github.com/marrisp/used_cars/assets/153134781/7ae63f9e-eadc-4931-96d6-ae3d30c14bf6">


My recommendations are to take the results of this model and create an app in Streamlit to allow for easier inputs of vehicle data to predict pricing. Based on the analysis, the data could be trimmed down to the following columns:

Year
Cylinders
Odometer
Fuel
Manufacturer

As mentioned previously, we should also consider creating two regression models, one to handle more typical vehicles and another to handle vehicles considered economical or exotic cars
