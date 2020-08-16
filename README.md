# Starbuck Capstone Challenge

### Problem Statement / Overview

This project is focused on the topic over offer recommendations on the Starbucks rewards mobile app. Nowadays, members are more and more willingly to spend through online order and offer could play a big role in user's engagement and transactions. With the data on customers' profile, offers'characteristic, all transaction details, it could help the business understand the current offer mechanism,
- Who are the cusomters active on Starbuck rewards mobile app? Who spent more frequently through offers?
- Which offer are more popular with higher usage? Which offer are more effective with impact on customers' spent behavior?

At the same time, with the interactions between users and offer, it enpower us to build up a recommendation system which could help to realize more revenues through the Starbucks rewards mobile app, basically enable us to uncover the user-offer pair with highest posibility of transactions and provided the answer for the question below,
- Who are the users we need to send the offer and what type of offer we need to send?

In addtion, the analysis on the current situation would help us to uncover our new potential customers who would be involved in the recommendation system once they registed in the app. The offer insight on the other hand could help to review the current offer designing, provision any potentials on offer adjustment or new offer design.

### 1. Introduction / Background

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

