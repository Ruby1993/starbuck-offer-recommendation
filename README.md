# Starbuck Capstone Challenge

## Introduction

This data set contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. Once every few days, Starbucks sends out an offer to users of the mobile app. 

- An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). 

- Some users might not receive any offer during certain weeks and not all users receive the same offer.

- Every offer has a validity period before the offer expires. 

> Example A:  a user could receive a discount offer buy 10 dollars get 2 off on Monday. The offer is valid for 10 days from receipt. If the customer accumulates at least 10 dollars in purchases during the validity period, the customer completes the offer.

> Example B:  a BOGO offer might be valid for only 5 days. You'll see in the data set that informational offers have a validity period even though these ads are merely providing information about a product; for example, if an informational offer has 7 days of validity, you can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

- You'll be given transactional data showing user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer. Keep in mind as well that someone using the app might make a purchase through the app without having received an offer or seen an offer.

Your task is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type. This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products. Couple notes keeping in mind:
- Customers do not opt into the offers that they receive; in other words, a user can receive an offer, never actually view the offer, and still complete the offer. 
> For example, a user might receive the "buy 10 dollars get 2 dollars off offer", but the user never opens the offer during the 10 day validity period. The customer spends 15 dollars during those ten days. There will be an offer completion record in the data set; however, the customer was not influenced by the offer because the customer never viewed the offer.

- You'll also want to take into account that some demographic groups will make purchases even if they don't receive an offer. 
> From a business perspective, if a customer is going to make a 10 dollar purchase without an offer anyway, you wouldn't want to send a buy 10 dollars get 2 dollars off offer. You'll want to try to assess what a certain demographic group will buy when not receiving any offers.

## Table of Contents

- [Getting Started](#getting-started)
- [File Description](#file-description)
- [Problem Statement/Overview](#problem-statement)
- [Result](#result)
  - [Customer Analysis](#customer-analysis)
  - [Offer Analysis](#offer-analysis)
  - [User-Offer Recommendation](#user-offer-recommendation )
- [Acknowledgement](#acknowledgement)
  
## Getting Started

If you want to run this analysis by yourself, there are couple libraries need to be installed which are listed below,
```python
library(pandas)
libaray(numpy)
library(math)
library(json)
library(os)
library(datetime)
library(matplotlib)
library(seaborn)
library(pickle)
library(sklearn)
```

## File Description

a. Datasets

- portfolio.json: the offer info with channel, duration, difficulty, and types.
- profile.json: the customers info with age, income, gender etc.
- transcript.json: the original transaction data including all transactions records for each user.

b. Starbucks_Capstone_notebook.ipynb

The python script preprocessed/cleanned/transformed the three datasets, provided offer/customer analysis over the current situation, and recommendation mechanics built up through FunkSVD.

C. user-offer Matrix

- user_item_matrix.p: the user item matrix for all transaction completed through offer
- df_train.p: the user item matrix for transaction completed through offer in the train dataset
- df_test.p: the user item matrix for transaction completed through offer in the test dataset

## Problem Statement

In this project, in order to maximize the data value flowing through the rewards app and the potential revenues through online order, the final goal is to design the recommendation engine that would be able to send the offer to the targeted customers which are most effective.
Here is a list of questions that will be answered in this project:

- Who are the customers active on Starbuck rewards mobile app? Who spent more frequently through offers?
- Which offers are more popular with higher usage? Which offers are more effective with an impact on customers’ spent behavior?
- Recommendation Engine: Who are the targeted customers we need to send the offer and what type of offer we need to send?

## Result

### Customer Analysis

**(1) What group of population is intended to purchase on Starbuck Rewards App?**

Based on the overall customer profiles within Starbuck,
- There are more males enrolled as a member
- Large proportion of customers are distributed between 40 and 60, and there are 2180 (out of 1700) customers with age over 100.
- The income is slightly right-skewly distributed, and most of customers with income between 5000 and 7000.
- Based on the number of days that customer joined the membership, most of members joined 2 - 3 years ago.

On the spent behavior perspective,
- Most customers spent 5-10 times.
- Their total spent is about 0-100.

**(2) Which group of population is intended to purchase through offer?**

If we look at how many offers are used by each customer out of the totoal number of purchaese (we called it as offer purchase percent), we could see:
- The profile for the customers with offer purchase percent > 60%:
    - Females are more preferred to use offer while purchasing;
    - Customers'age are more concentrated between 50 to 70, which is similar to the overall cusomters'profile;
    - The income is mostly distributed between 70k to 100k;
    - Most of users joined 2-3 years ago;
    - The total number of transaction is between 3-9 time.
    
    
- The profile for the customers with offer purchase percent < 30%:
    - Males are more preferred to use offer;
    - there are more young customers within this group ;
    - Lower income group have a higher percentage in this group;
    - Most of users joined 2-3 years ago;
    - The total number of transaction is between 4-35 time, which is broader than the group with higher offer purchase percent.
    
**(3) Which factors behind customers are more correlated with offer transaction?**

- Age, income and female gender have positive impact over the offer purchase percent.
- The length of time member stayed with Starbuck and male gender have negative impact.

### Offer Analysis

**(1) Which offer are more popular within transactions?**

From the offer involved in the transactions,
- Bogo and discount type are the major offer type in the transacions
- Offers are more diversed in channel, and email and mobile are the top 2 channels with most offers.

**(2) Which offer has higher usage through transacion?**

As we could see, 
- 7 offers are evenly distributed among transactions.
- The offer with discount type have the highest percentage of usage with transaction, followed by bogo.
- The one with highest percentage usage is the offer with the id (fafdcd668e3743c1bb461111dcafc2a4)
- The offer available in all channels have the highest percent of usage, followed by the offers in  all three channels email, mobile,and web and offers. The lowest percent fall in the offers with email as the only channel.

**(3) Which attribute behind offer will drive the effectiveness?**

- Mobile, social, web, discount type, informational type have positive impact over the offer effectiveness.
- The difficulty, reward, bogo type have negative impact.

### User Offer Recommendation 

By leveraging the transaction records, we utilize user-offer-matrix that represents how many number of transactions are done through offers for each users. With the FunkSVD algorithm, the lowest mean square error we achieved is 0.00632 with 11 latent features.  
- For the existing user in the test dataset, we could get the estimated number of transactions based on the dot product between the user matrix and the offer matrix. Then we would be able to recommend the offer with the highest estimated number of transactions.
- For the new user as the “Cold Start Problem”, we built the clustering on offers and members and then created the collaborative filter. Any member with potential background info are able to be classified into a specific cluster and the offers will be recommended based on the effectiveness.

**Model Evaluation and Validation**

In order to test the model, we utilize a testing dataset to get the mean squared errors for the prediction. Through the iteration on the number of latent features from 1 to 20, we could uncover the latent features with minimum mean squared error(0.00632), which is about 11. The learning rate and iterations here are constantly the same (learning_rate=0.005, iters=250).

## Acknowledgement


