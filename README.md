
Rewards Reference Domain:
========================
Account and restaurant information are stored in a persistent form inside a relational database. The RewardNetwork implementation delegates to supporting data access components called 'Repositories' to load Account and Restaurant objects from their relational representations.

An AccountRepository is used to find an Account by its credit card number
A RestaurantRepository is used to find a Restaurant by its merchant number.
A RewardRepository is used to track confirmed reward transactions for accounting purposes. It holds the same data as the RewardConfirmation

A Dining record contains:
============================

Customer's credit-card number
Merchant id of the restaurant
Amount paid for the meal
Date the customer dined

The full rewardAccountFor(Dining) sequence incorporating these repositories is:
================================================================================

Fetch the Account from the AccountRepository
Fetch the Restaurant from RestaurantRepository
Determine the Reward contribution (an instance of MonetaryAmount) using Restaurant.calculateBenefitFor(Account, Dining)
Update the account beneficiaries using Account.makeContribution(MonetaryAmount)
Save modified Account information using AccountRepository.updateBeneficiaries(Account)
Create a RewardConfirmation using the RewardRepository

Reward Dining Database Schema: 
==============================

![image](https://github.com/chamunune-30/Reward-Reference/assets/161777927/2d2dd55b-6db9-44e7-9206-282323be7fc4)

There are two scripts:
=======================

schema.sql - creates the necessary tables, and
data.sql - adds test data (several accounts and a single restaurant)
