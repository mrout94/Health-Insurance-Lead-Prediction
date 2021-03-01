# Health-Insurance-Lead-Prediction
Top 3% Solution for Analytics Vidhya Hackathon on their website from 26-28 Feb 2021.  
The link for the same can be found [here](https://datahack.analyticsvidhya.com/contest/job-a-thon/)
You can try this notebook on [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mrout94/Health-Insurance-Lead-Prediction/blob/main/Final_Notebook.ipynb)

# Why this Competition?
This competition provides an unique oppertunity for Data Science begiiners to participate in a Hackathon style challenge for Data Science and compete for potentiaql oppertunities in many reputed companies. It also provides the unique oppertunities for beginners to get their hands dirty and indulge is practical application of ML and do one of the basic tasks machine learning algorithms are capable of doing:- **Classification**.

# Problem Statement
Our client (FinMan Company) wishes to cross-sell health insurance to the existing customers who may or may not hold insurance policies with the company. A policy is recommended to a person when they land on their website, and if the person chooses to fill up a form to apply it is considered as a Positive outcome (Classified as lead). All other conditions are considered Zero outcomes.

## Data Description:-
We have the following information regarding the potential-customer and the insurance at any given point in time:
* Demographics (city, age, region etc.)
* Information regarding holding policies of the customer
* Recommended Policy Information

## Expected Outcome:-
* Build a model to predict whether the person will be interested in their proposed Health plan/policy given the information above.
* Grading Metric: **ROC_AUC_SCORE**

## Data Cleaning:-  
1. Missing values in Policy type and Policy duration were considered as a new category since those might be new customers (as there were no allocated classes for new customers specifically in the data).
2. Missing values in Health Indicator was imputed with the mode of the same class.

## EDA findings:-
1. The negative class has a very high count in the training data, thus this is a an imbalanced class problem.
2. The recommended policy premium for negative class is a little bit on the higher side as compared to positive.
3. There are some policies like 3, 13 and 16 where the rejection of the policy can be attributed to high premium.
4. Insurance type has little to no effect on the response on it’s own.
5. There are certain health conditions such as X7, X8 and X9 which when combined with age have a high impact on getting response.
6. There are certain cities like C30, C32, etc whose response rate is higher than others.
7. People having own house have a higher response rate as compared to rented customers.
8. Rented people when asked above a certain price limit have more tendency to reject the offer.
9. Existing customers have a slightly higher response rate as compared to new customers. Which indicates that they trust the company or the company has very attractive deals.
10. Recommended policy premium rises with age.
11. There are more people buying the insurance who have their own house.
12. Most of the insurances in data are individual in nature.
13. Clarifying the above point is that most people take insurance for their own and hence no. of ‘Is_Spouse’ is low.
14. Most of the data points are from Old customers.

## Feature Engineering & Feature selection:-  
1. Age Confidence Interval:- Signifies how much we know about the customer.
2. Long Term Customer:- How old is the customer served by our company and conversely their response talks about how much faith they have in us.
3. Log of Recommended Policy Premium:- As seen earlier, this has a long tail. So took log to centre the data.
4. Mean Age:- To be used as most probable age.
5. Premium to Age Ratio:- How old is the customer and how much paying capacity they have at that point.
6. City Code and Region Combined:- For example saying ‘Bandra in Mumbai’.
7. Customer age buckets:- Categorize customers based on their age.
8. Proposed Policy premium buckets:- Categorize policy premium in discrete classes.
9. Policy Offered for:- Is it offered for the person, or join or for Family members.
10. City and Accommodation type joined:- For example sating ‘Renting in Pune’.
11. Recommended Policy to round number:- To remove trivialities based on noise.

## Model Selection:-  
Various models were tried and selected based on performance on stratified cross validation performance. The approach was limited to classical machine learning algorithms because it were enough to secure a better performance already on the leaderboard.  
  
The models I tried and their scores are compiled below:  
| Model | Score (ROC-AUC) |
| --- | ----------- |
| Logistic Regression | 0.51 |
| K Nearest Neighbours | 0.50 |
| Random Forest | 0.59 |
| XGBoost | 0.64 |
| Light GBM | 0.65 |
| Cat Boost | 0.79 |
| Balanced Random Forest | 0.62 |
| Ensemble of XGBoost, Catboost and LightGBM | 0.80 |  

Thus I chose the custom ensemble (weights balanced by a bayesian optimization function) as my final model for submission.  

## Performance:-  
**ROC: 0.80  
Rank: Top 3%**
