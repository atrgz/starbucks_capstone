# Starbucks Capstone Project

## Table of contents

- [Installations](#installations)
- [Project Motivations](#project-motivations)
- [File Descriptions](#file-descriptions)
- [Licensing, Authors and Acknowledgments](#licensing-authors-and-acknowledgments)

## Installations

This project is written in Python 3.13.2 using the following libraries:

- pandas 2.2.3
- numpy 2.2.2
- matplotlib 3.10.0
- seaborn 0.13.2
- scikit-learn 1.6.1
- statsmodels 0.14.4
- Python 3.13.2

## Project Motivations

This is the capstone project for [Udacity's Data Scientist Nanodgree](https://www.udacity.com/course/data-scientist-nanodegree--nd025?promo=year_end&coupon=SAVE40&utm_source=gsem_brand&utm_source=gsem_brand&utm_medium=ads_r&utm_medium=ads_r&utm_campaign=19167921312_c_individuals&utm_campaign=19167921312_c_individuals&utm_term=143524475679&utm_term=143524475679&utm_keyword=udacity%20data%20science_e&utm_keyword=udacity%20data%20science_e&gad_source=1&gclid=EAIaIQobChMImKz0y_e0gwMVfj4GAB1FgAEHEAAYASAAEgI-h_D_BwE).

This README file includes a brief summary of the project, for the full report on methodoly, findings and conclusions, please visit this [Medium Article](medium_link).

### 1. Business motivations and data description

Every few days Starbucks sends an offer to the users of its mobile app. There are three different types of offers:

- Informational, with any reward linked to it
- Discount, after spending certain amount of money, the user is entitled to a discount
- BOGO (Buy One, Get One), if the user spends the amount of money specified by the offer, will get a coupon for the same amount

Three sets of data are provided:

- portfolio.json, describes each type of offer with a unique id and their characteristics (time, discount and difficulty)
- profile.json, with all the users registered in the mobile app and some demographic traits of each
- transcript.json, a log of all transactions linked to the app. This log records when a person receives, view and complete (spends the difficulty amount) an offer as well as all transactions made by a person.

It's worth noticing that the records in these files are generated, not real data. But for the purpose of this project, that suffices.

The goal of this project is to answer two questions:

1. What type of offer affects each demographic profile?
2. Is it possible to predict the amount of money spend by a person given an offer?

### 2. Data Cleaning

The key aspect of this project is to figure out the offers that drive transactions. To achieve this goal, the three datasets are cleaned and merged to find out which offers are active when a transaction is made. It's assumed that:

- An offer received but not yet viewed in the moment of the transaction is not affecting the purchase
- Transactions can be influenced by multiple offers at any given time
- Offer completion don't affect transactions

For the scope of this project, the channel used to convey the offers to users is not considered.

### 3. Modelling:

Two different models are used.

First, to evaluate the influencing offers, Ordinary Least Squares (OLS) is used to do a regression of the active offers at any given time and how those offers explain the amount spent. Then each p-value is evaluated to check if that offer is statistically significant to the amount spent.

Then, to answer the second question, a Machine Learning model is used to perform a Linnear Regression model and R-Square is used to evaluate the performance of the model in training a test sets.

### 4. Summary of findings

A set of significant offers is provided for each demographic group. Although some groups don't have any significant offer.

Then a model to predict the amount spect is also provided, but the results of the R-square are not promising. (For test set 7.1% and for train set 6.8%).

## File Descriptions

Data folder:
The three datasets are stored in this folder in JSON format
**profile.json**
Rewards program users (17000 users x 5 fields)

- gender: (categorical) M, F, O, or null
- age: (numeric) missing value encoded as 118
- id: (string/hash)
- became_member_on: (date) format YYYYMMDD
- income: (numeric)

**portfolio.json**
Offers sent during 30-day test period (10 offers x 6 fields)

- reward: (numeric) money awarded for the amount spent
- channels: (list) web, email, mobile, social
- difficulty: (numeric) money required to be spent to receive reward
- duration: (numeric) time for offer to be open, in days
- offer_type: (string) bogo, discount, informational
- id: (string/hash)

**transcript.json**
Event log (306648 events x 4 fields)

- person: (string/hash)
- event: (string) offer received, offer viewed, transaction, offer completed
- value: (dictionary) different values depending on event type
- offer id: (string/hash) not associated with any "transaction"
- amount: (numeric) money spent in "transaction"
- reward: (numeric) money gained from "offer completed"
- time: (numeric) hours after start of test

## Licensing, Authors and Acknowledgments

This project has no specific license, but makes extensive use of the templates, data and guidelines provided in the Udacity course.
