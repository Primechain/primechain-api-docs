# Auction of assets

Primechain API can be used to create a transparent, secure and efficient auction ecosystem with blockchain nodes operated by Financial institutions, Auditors, Regulators, Bidders.

1. [Onboarding bidders](#1-onboarding-bidders)   
2. [Signing contracts, inspection reports, terms and conditions](#2-signing-contracts-inspection-reports-terms-and-conditions)
3. [Tokenizing the asset to be auctioned](#3-tokenizing-the-asset-to-be-auctioned)   
4. [Earnest Money Deposit](#4-earnest-money-deposit)   
5. [The auction process](#5-the-auction-process)   

### 1. Onboarding bidders

The relevant API end points for onboarding relevant entities (bidders etc.) are [`create_entity`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity), [`create_keypair`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management) and [`create_entity_rsa`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-creating-a-new-entity-with-rsa-keys) 

### 2. Signing contracts, inspection reports, terms and conditions 
The relevant API end points are [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data) and [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great)

## 3. Tokenizing the asset to be auctioned
The relevant API end points for tokenizing the asset to be auctioned are: [`create_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset).

## 4. Earnest Money Deposit
The relevant API end points for tokenizing fiat currency for Earnest Money Deposit [EMD] are [`create_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset) and [`create_more_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset)

## 5. The auction process
The relevant API end points are [`create_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#6-create-a-targeted-offer), [`read_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#3-read-an-offer), [`reject_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#7-reject-a-targeted-offer) and [`accept_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-accept-an-offer)
