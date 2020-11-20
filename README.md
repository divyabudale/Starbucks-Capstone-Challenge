# Starbucks-Capstone-Challenge
## Table of Contents
1. [Installation](#Installation)
2. [Project Motivation](#Motivation)
3. [File Descriptions](#Descriptions)
4. [Results](#Results)
5. [Acknowledgements](#Acknowledgements)

# Installation <a name="Installation"></a>
There should be no necessary libraries to run the code here beyond the Anaconda distribution of Python. The code should run with no issues using Python versions 3.*.

# Project Motivation <a name='Motivation'></a>

Starbucks sends out an offer to users of the mobile app. The task is to combine transaction, demographic, and offer data to determine which demographic groups respond best to which offer type. With this project I intended to gain insights into the following
1. Does the membership age of the customer have a relation to the customer using the offer?
2. What is the relationship of the income and age to the offer completion?
3. Who spends more between Male and Female?
4. Finally,  What are the main drivers of an effective offer on the Starbucks app?


# File Descriptions <a name="Descriptions"></a>
The data is contained in three files:

portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)
profile.json - demographic data for each customer
transcript.json - records for transactions, offers received, offers viewed, and offers completed
Here is the schema and explanation of each variable in the files:

portfolio.json

id (string) - offer id
offer_type (string) - the type of offer ie BOGO, discount, informational
difficulty (int) - the minimum required to spend to complete an offer
reward (int) - the reward is given for completing an offer
duration (int) - time for the offer to be open, in days
channels (list of strings)
profile.json

age (int) - age of the customer
became_member_on (int) - the date when customer created an app account
gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
id (str) - customer id
income (float) - customer's income
transcript.json

event (str) - record description (ie transaction, offer received, offer viewed, etc.)
person (str) - customer id
time (int) - time in hours since the start of the test. The data begins at time t=0
value - (dict of strings) - either an offer id or transaction amount depending on the record


# Results <a name='Results'></a>

I. Data Cleaning and Pre-Processing
The data from the three files were cleaned and merged. The target variable was identified and developed based on the event type and duration.
Feature Engineering was performed to create additional variables.

II. Exploratory Data Analysis
The following insights were gained after performing Exploratory Data Analysis : 
1. The average female income and age is greater the average male income and age of the customer.
2. Male membership is increasing over the past two years
3. The success rate is widely different across the different offers
4. The average spending amount of the female customer is greater than the male customer
5. Apart from the customer and offer, customer spending, membership and social media are the the most important features for the predicting if the offer will be completed

III. Model Implementation
Using k-fold cross validation (with n_splits=5) , Random Forest, Light GBM, XGBoost, AdaBoost, GBM and Decision Tree classifier models were trained. Macro-avg precision, recall, f1-score and accuracy were used to evaluate the performance of the model.

Random Forest classifier resulted in the best performing model with the f1-score of 0.9087, precision 0.9104 and recall 0.9072

IV. Refinement
GridSearchCV was used to fine tune the parameters for a Random Forest Classifier. A 5-fold cross validation test was performed to check if the models are robust in the end.
After fine tuning, Random Forest showed an improvement on the f1-score at 0.9108

V. Model Evaluation
As stated, model was evaluated on precision, recall, f1-score and accuracy

Precision : Number of items correctly identified as positive out of total items identified as positive: True Positives /(True Positives + False Positives) i.e Out of the total 8218 identified positives, 7493 was accurately identified

Recall : Number of items correctly identified as positive out of total true positives: True Positives /(True Positives +False Negatives) i.e Out of total 7900 positives, 7493 was accurately identified as positives
From the confusion matrix, we were also able to show that the model identifies 13 % of false positive i.e the customer did not accept the offer but was predicted as success and 5% of false negatives i.e customer accepted the offer but was predicted as fail.
Since, false negative is less than false positive, our model is classifying accurately as it has low chances of missing an individual who would respond.

The details of the analysis can be found on medium : <a href> https://medium.com/@divyabudale/starbucks-capstone-challenge-6c4438c5a03d </a>

# Acknowledgements <a name='Acknowledgements'></a>

1. Udacity for providing such a complete Data Science Nanodegree Program
2. Starbucks for providing the datasets
