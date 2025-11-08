# Problem Statement: Boston House Price Prediction

## Context

A real estate company in the Boston suburbs is actively working to gain a competitive edge by accurately forecasting the median value of homes. By utilizing historical data from the U.S. Census Bureau, they aim to improve their property valuation and market analysis strategies. The company's current valuation methods are slow and lack the precision needed to quickly identify properties that may be undervalued or overvalued in the market. The company is seeking to take the initiative to build and deploy a predictive regression model that can provide real-time, precise home value estimates based on various socioeconomic and environmental factors.

## Objective

The Data Science & Product Innovation team has successfully developed a **Boston house price prediction model** that estimates housing prices using features such as crime rate, average number of rooms per dwelling, property tax rate, accessibility to highways, and other neighborhood characteristics. The model has already proven valuable by providing real estate professionals, buyers, and policymakers with real-time, data-driven insights through a lightweight web application.

However, as adoption expanded across diverse user groups and real estate platforms, the centralized deployment approach exposed challenges including performance bottlenecks, prediction delays, and environment inconsistencies across systems.

To address these issues, the primary objective is to implement a **robust and scalable model deployment process** that ensures consistent performance, simplifies distribution, and reduces maintenance overhead. The successful deployment of this solution will enable seamless access to accurate housing price predictions, improve user experience across platforms, and strengthen the company’s competitive edge in the real estate market.

## Data Information

Each record in the database provides a description of an boston house price. A detailed data dictionary can be found below.

## Data Dictionary

* CRIM: Per capita crime rate by town.
* ZN: Proportion of residential land zoned for lots over 25,000 sq.ft.
* INDUS: Proportion of non-retail business acres per town.
* CHAS: Charles River dummy variable (1 if tract bounds river, 0 otherwise).
* NOX: Nitric oxides concentration (parts per 10 million).
* RM: Average number of rooms per dwelling.
* AGE: Proportion of owner-occupied units built prior to 1940.
* DIS: Weighted distances to five Boston employment centers.
* RAD: Index of accessibility to radial highways.
* TAX: Full-value property-tax rate per $10,000.
* PTRATIO: Pupil-teacher ratio by town.
* LSTAT: Percentage of lower status population.
* MEDV: Median value of owner-occupied homes in $1000's (target variable).
