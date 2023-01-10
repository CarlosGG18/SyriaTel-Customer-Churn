# SyriaTel-Customer-Churn
<img src='https://user-images.githubusercontent.com/117116368/211051057-e43267cd-dd3e-4743-947b-7588d186557f.png' width="400" height="300">

## Table of Contents
* [Overview](#Overview)
* [Method](#Process)
* [Analysis](#Exploritory-Data-Analysis)
* [Recommendations](#SyriaTel-Recommendaton)


## Notebooks
* CLEANING.ipynb: Cleaning of the database
* EDA.ipynb : Exploritory Data Analysis
* Modeling.ipynb : All models made (GradientBoost, LogisticRegression, KNNClassifier, RandomForest, DecisionTree)

## Overview

SyriaTel is a telecommunication company based in Syria, whose dataset of 20 features and 3,333 rows I used to create a predictive model to help lower their churn rate of 15% (Customers who decided to end their subscription). Through the modeling section I incorporated 5 models including (LogisticRegression(Base Model) , DecisionTreeClassifier, GradeintBoost, RandomForestClassifier, and K-Nearest Neighbors)

## Process
* Data Cleaning 
* EDA 
* Modeling 
* Recommendation
## Data Cleaning

As any amazing, perfect, and great data scientist I immediately dove into the data set to look out for:

* Null/ NaNs, which there had not been any in the entire dataset, which initially should ring some bells but after searching through the unique values within the columns there wasn’t any value of concern.

* I also checked for duplicated values or rows that can be eliminated under the circumstance that one may have accidently slipped through, but alas none of those either

![thumbs_up](https://user-images.githubusercontent.com/117116368/211057010-268c80c6-24e8-4f08-a0ad-c244f4e5b7c4.gif)

# Exploratory Data Analysis (EDA)

*  Checked the normalized distribution of my target variable ('Churn') come to find out a severe imbalance (85% of retained customers **15% of Customers Churned**)
* Conducting `Pearsons Correlation Matrix` I was able to identify several features of importance:
* `customer_service_calls` : Amount of times a customer calls customer service
* `international_plan` : Binary value that shows whether customer has an international plan or not
* `total_charges` : This column I created myself by combining `day_charge` , `evening_charge`, and `night_charge`

# Customer Service Calls
![churn%2](https://user-images.githubusercontent.com/117116368/211065323-d191da3d-4130-42bc-9881-e7d5f9a47a3f.png)
As seen above if the amount of customer service calls moves beyond 3, the likeliness for churning increasing from **10% to 46%** and if the calls get to 9, 100% of the customers are ending their services. Through my EDA I was able to see that 80% of customers have made at least 1 call to customer service, which is already a bad sign.

# International Plan

No Plan       | Active Plan
:-------------------------:|:-------------------------:
![NoIntPlanChurn2](https://user-images.githubusercontent.com/117116368/211063258-6019938f-80fb-4b00-8110-b35c292c6ae1.png)|![IntPlanChurn2](https://user-images.githubusercontent.com/117116368/211062620-3d5b51b1-0e13-49a8-99b2-c1978a3d92ec.png)

Creating two separate data frames of customer with no international plan and those with one, individuals with an active international plan are **churning at 42%** ALMOST HALF! Emphasizing the need for a restructure if that plan, although data needs additional details on respective plans.
# Total Charges
![Totalcharges](https://user-images.githubusercontent.com/117116368/211065025-f30c3b5d-b5a9-419b-895c-93c190b9af60.jpg)

Despite the churn in customers being right skewed this feature had the strongest impact on whether a customer churned or not, with charges above $70 nearly 80% of the customers were likely to churn.
# Model
Train Set   |   Test Set
:-------------------------:|:-------------------------:
<img width="363" alt="Screenshot 2023-01-06 at 12 59 45 PM" src="https://user-images.githubusercontent.com/117116368/211071595-f702bf22-de85-4aec-9767-adcdc371255d.png">|<img width="358" alt="Screenshot 2023-01-06 at 1 00 44 PM" src="https://user-images.githubusercontent.com/117116368/211071612-7f2bf4f1-5155-4ca8-a73e-f90bfc3d85d5.png">

My best performing model was the `GradientBoostingClassifier` with hyperparameter tuning to learning rate and max depth. The cost benefit of this model with the guidance of my confusion matrix would be that when SyriaTel implements a retention plan, they would lose more money focusing on customers that they believed churned but didn’t as opposed to those they believe didn’t churn but actually did.
# Post-model Feature Importance
![features](https://user-images.githubusercontent.com/117116368/211086788-0175264f-e889-453b-8b47-44299caa7865.png)

This feature list was made after by best model was constructed and further emphasizes the heaviest correlated variables to churn rate

# SyriaTel Recommendaton
* Individuals with international plans will churn at 42% which should immediately suggest a pricing restructuring
* Customer service calls is a difficult feature to directly account for but needs to be monitored after the 2nd call as well as categories for reason of call
* Total Charges is the largest contributor to churn rate with 80% of customers churning after $75, there needs to be a cap on `day_charges` as total charges is heavily influenced by the prices during those times.
