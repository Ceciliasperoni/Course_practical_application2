# Course_practical_application2

What drives the price of a used car? 
README 
Practical Assignment 2 - ML/AI Professional Certificate Berkeley

***Cecilia Speroni*** 

**Overview**

This project uses a dataset of approximately 426,000 used vehicles to understand what drives used-car prices. Following the CRISP-DM (Cross-Industry Standard Process for Data Mining) framework, the notebook moves through the following workflow: defining the business need, understanding and exploring the data, cleaning and preparing the data, modeling and evaluation, and translating the findings into business recommendations.

**Objective** 

The goal is to identify most influential car features, quantify their relationship to price, and choose a preferred model (based on out-of-sample prediction performance) to make business recommendations to a dealership owner. 
- Business problem: Which car characteristics do consumers value most?
- Data science problem: Use observed car characteristics and market prices (customers' revealed preferences when purchasing) to assess which characteristics contribute most to differences in price and predict car prices.
  
**Dataset**
  
The dataset was provided as part of the assignment and contains 426K used car listings, including information on year of the vehicle, manufacturer, model, odometer, among other features. 

**Methodology**

Exploratory Data Analysis
I conducted exploratory data analysis to understand data  quality, and key patterns in the used-car data before modeling. I examined variable distributions, missing values, duplicates, and potential outliers, and explored opportunities to impute missing data using available information. I also used visualizations to explore relationships and identify important determinants of price. Specifically, how price varies with important predictors, including vehicle age, mileage, manufacturer, and vehicle type. These findings informed the data-cleaning decisions, variable selection, and modeling approach used in the analysis.

Modeling
I assess the predictive performance of 5 models (on test data) and a  5-fold cross-validation: 
	- Linear regression — Core
	- Linear regression — Expanded
	- Polynomial regression with age² — Core
	- Ridge regression — Core
	- Lasso regression — Core

where
	- *Core*: Price = age + odometer + manufacturer
	- *Expanded*: Price = age + odometer + manufacturer + paint color + transmission + fuel + vehicle type

I started with a simple parsimonious multiple regression model with core features highly predictive of price (age, odometer, and manufacturer), and then expanded the set of variables to include other features. To illustrate a polynomial regression, I also estimated the core model using a quadratic (polynomial 2) of age given the non-linear nature of the relationship between age and price observed in the explorative data analysis. 

I also estimated Ridge (L2) and Lasso (L1) regression models to assess whether regularization could improve prediction and reduce overfitting. Both methods penalize large coefficients in different ways. Ridge shrinks coefficients toward zero while retaining all predictors. Lasso can shrink some coefficients all the way to zero, effectively removing less useful predictors from the model.  For both models, numeric predictors were standardized so that the penalty would be applied on a comparable scale. I used 5-fold cross-validation with GridSearchCV to test different values of the penalty parameter (alpha) and selected the value that produced the lowest Mean Absolute Error (MAE).

**Results**

I find that the linear regression with expanded set of variables is the best-performing model, with a test MAE (Mean Absolute Error) of $5,590, which means that its predicted vehicle prices differ from observed prices by about $5,590 on average. This is much better than the core linear model (MAE = $6,488), suggesting that color, transmission, fuel, and vehicle type contain meaningful information about used-car prices beyond age, mileage, and manufacturer. The expanded model also has the highest R² (0.63), explaining approximately 63% of the variation in vehicle prices (in the test data). (Adding a quadratic age term moderately improves the core model with 3 features (MAE falls from $6,488 to $6,287 and R² rises from 0.52 to 0.54), providing some evidence that the relationship between vehicle age and price is nonlinear, as we have seen in the figures).

Ridge and Lasso performed very similarly to the standard linear regression, which is not surprising because I applied them to a simple core model containing only three very important predictors—vehicle age, mileage, and manufacturer. Because the model did not include many unnecessary predictors, there was relatively little for Ridge to shrink or Lasso to eliminate.

**Next Steps**

Throughout the notebook, I flag next areas of future work, which include specific ideas for further data cleaning, and expanding models to include more vehicle characteristics. 

**Contact** 
https://www.linkedin.com/in/cecilia-speroni/
