# Invoice discounting

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

Invoice discounting enables suppliers to sell their invoices at a discount to investors. This enables suppliers to get faster access to money they are owed and enables buyers to get more time to pay. Instead of relying on the creditworthiness of suppliers (usually smaller businesses), the investors deal with buyers (usually large businesses). This can lower financing costs, optimize working capital and improve business efficiency.

![Bank guarantees on the blockchain](http://www.primechaintech.com/img/api_documentation/invoice.jpg)

Invoice discounting is also referred to as supply chain finance and factoring. The process involves 4 parties: banks, corporates (payers), vendors (payees) and investors.

***Benefits of using the blockchain for invoice discounting:***   
(1) Fractionalisation of invoice enabling small investors to participate   
(2) Automated reconciliation   
(3) Provably immutable process   

1. [On-boarding entities](#1-on-boarding-entities)   
2. [Token issuance and redemption](#2-token-issuance-and-redemption)   
3. [The invoice discounting process](#3-the-invoice-discounting-process)   
4. [Overview of roles](#4-overview-of-roles)

## 1. On-boarding entities

The relevant API end points for onboarding relevant entities (corporates, vendors and investors etc.) are [`create_entity`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity), [`create_keypair`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management) and [`create_entity_rsa`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-creating-a-new-entity-with-rsa-keys) 

## 2. Token issuance and redemption

The relevant API end points for tokenizing fiat currency for this are: [`create_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset) and [`create_more_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset).

These tokens can be purchased / redeemed by investors, corporates and vendors. 

The relevant API end points for transferring tokenized fiat currency are [`send_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#6-transfer-asset-when-private-key-is-in-the-node), [`transfer_multisign_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#7-transfer-asset-from-multisig-address) and [`transfer_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#8-transfer-asset-when-private-key-is-not-in-the-node)

## 3. The invoice discounting process

### Step 1: Receipt of approved asset by bank
Corporate sends details of an approved invoice to its bank through the online banking system / app.

### Step 2: Publishing of invoice to the blockchain by the bank
The bank publishes the invoice (as an asset) to the blockchain using [`create_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset). This asset is issued to the corporate who is the payer of that particular invoice.

### Step 3: Verification by corporate (payer)
The corporate verifies the details of the asset (invoice). If it is correct, the corporate (payer) transfers the asset (invoice) to the vendor who is the payee for that invoice. This is done using [`send_asset`]()

If it is incorrect, the corporate (payer) transfers the asset (invoice) to the burn address. The relevant API end points for this are [`send_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#6-transfer-asset-when-private-key-is-in-the-node), [`transfer_multisign_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#7-transfer-asset-from-multisig-address) and [`transfer_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#8-transfer-asset-when-private-key-is-not-in-the-node)

### Step 4: Bidding by investors
Investors place bids on the invoice. To place a bid, they must hold sufficient quantity of tokens. They can purchase these tokens from the bank. Once they place a bid, the relevant amount of tokens are ‘locked’ till either (1) the vendor rejects the bid or (2) the investor cancels his bid.

To create the offer, use [`create_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#6-create-a-targeted-offer)

To cancel the offer, use [`cancel_targeted_offer`]()

### Step 5: Acceptance / rejection of bids by vendor
The vendor can view all bids placed on invoices in which he is the payee. The vendor can accept or reject bids. If the vendor accepts the bid, the asset (invoice) is transferred to the relevant investor and the bid amount is transferred to the vendor. The vendor can redeem the tokens from the bank.

To reject the offer, [`reject_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#7-reject-a-targeted-offer)

To accept the offer, [`accept_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-accept-an-offer)

### Step 6: Maturity of invoice
When the invoice matures, the corporate pays the relevant amount to the bank and receives equivalent tokens. 

### Step 7: Payment to investor
The corporate offers to exchange the asset (invoice) for the maturity amount. To create the offer, use [`create_targeted_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-accept-an-offer)

The investor accepts the offer using [`accept_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-accept-an-offer)

### Step 8: 
The corporate then sends the asset (invoice) to the burn address using [`send_asset`]()

## 4. Overview of roles

### Bank
1. Onboard corporates
2. Onboard vendors
3. Onboard investors
4. Distribute tokens against fiat currency held by it
5. Publish verified invoices to the blockchain as assets
6. Redeem tokens for fiat currency

### Corporate (payer)
1. Transfer verified invoices as assets to the vendor who is the payee for that invoice.
2. Pay the invoice amount on maturity.

### Vendor (payee):
1. View all published invoices in which they are payees
2. View offers on all published invoices in which they are payees
3. Accept offers on published invoices in which they are payees
4. Reject offers on published invoices in which they are payees

### Investors: 
1. View all published invoices
2. Bid on published invoices
3. Cancel their own bids (before the vendor has accepted the bid)
4. View their bids that have been accepted by vendors
5. View their bids that have been rejected by vendors
