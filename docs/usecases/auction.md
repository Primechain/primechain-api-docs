# Auction of assets

Primechain API can be used to create a transparent, secure and efficient auction ecosystem with blockchain nodes operated by Financial institutions, Auditors, Regulators, Bidders.

1. [Onboarding bidders](#1-onboarding-bidders)   
2. [Signing contracts, inspection reports, terms and conditions](#2-signing-contracts-inspection-reports-terms-and-conditions)
3. [Tokenizing the asset to be auctioned](#3-tokenizing-the-asset-to-be-auctioned)   
4. [Earnest Money Deposit](#4-earnest-money-deposit)   
5. [The auction process](#5-the-auction-process)   

## 1. Onboarding bidders

The relevant API end points are:

1. Creating a new entity - [`create_entity`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity) or [`create_keypair`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management) or [`create_entity_rsa`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-creating-a-new-entity-with-rsa-keys)   

2. Grant Permission - [`grant_permissions`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#5-grant-permissions-to-an-entity)  

3. Creating multisignature address - [`create_multisig_address`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#4-create-multisig-address)

4. Revoke Permission - [`revoke_permissions`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#6-revoke-permissions-to-an-entity)

## 2. Signing contracts, inspection reports, terms and conditions 
The relevant API end points are:
1. Signing data - [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data)   

2. Verifying a digital signature - [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature)

3. Sign and store signature in GREAT - [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great)

## 3. Tokenizing the asset to be auctioned
The relevant API end point is [`create_new_asset_from`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset)

## 4. Earnest Money Deposit
The relevant API end points for tokenizing fiat currency for Earnest Money Deposit [EMD] are:
1. [`create_new_asset_from`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset)

2. [`asset_create_more_from`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset)

## 5. The auction process
The relevant API end points are:

1. Create targeted offer - [`create_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#6-create-a-targeted-offer)

2. Read an offer - [`read_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#3-read-an-offer)

3. Reject targeted offer - [`reject_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#7-reject-a-targeted-offer) 

4. Accept offer - [`accept_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-accept-an-offer)
