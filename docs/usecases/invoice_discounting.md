# Invoice discounting

![Bank guarantees on the blockchain](http://www.primechaintech.com/img/api_documentation/invoice.jpg)

Invoice discounting enables suppliers to sell their invoices at a discount to investors. This enables suppliers to get faster access to money they are owed and enables buyers to get more time to pay. Instead of relying on the creditworthiness of suppliers (usually smaller businesses), the investors deal with buyers (usually large businesses). This can lower financing costs, optimize working capital and improve business efficiency.

Invoice discounting is also referred to as supply chain finance and factoring. The process involves 4 parties: banks, corporates (payers), vendors (payees) and investors.

***Benefits of using the blockchain for invoice discounting:***   
(1) Fractionalisation of invoice enabling small investors to participate   
(2) Automated reconciliation   
(3) Provably immutable process   


1. [On-boarding corporates, vendors and investors](#1-on-boarding)   
2. [Token issuance and redemption](#2-token-issuance-and-redemption)   
3. [The invoice discounting process](#3-the-invoice-discounting-process)   
4. [Overview of roles](#4-overview-of-roles)


## 1. On-boarding
The bank on-boards corporates, vendors and investors using `post /api/v1/onboard_user`   

Sample input
```
{
  "user_identifier": "23792387",
  "user_description": "Noodle Ltd. is a company registered under the laws of the Republic of India"
}
```
Sample output:   
```
{
"status": 200,
"response": {
"primechain_address": "16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA",
"primechain_private_key": "VECSuwoYmF8LHpBy67eV6NbHqBYBuG74dEaE7435xUcS9FGQ48WdXfjc",
"primechain_public_key": "021c2d2e89d68a7cd4505f2464c26d2ace9ced3433f57ac619a9c52fc907042309",
"tx_id": "ef3f1cde044f0a16382230d4e700143da3ef5138a2bfb60791c05461a0ff1de2",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiB49uOAIfw2nGsueboVL +CWPYqiYS/+pYrUjoCe3owwn395o68IPmYDm2NCYk17Dwx2bDW5/B4OFgznw+eSe Hg1K2RrCQbwArKssjez04VtVBODowv/h8usq6R/g1zsA/YtZTLHMR0tdr9Ton0Op GBbc/qsgAo76OJvGcy7dwCXcbzVkscjURiVQ8Grn+yvpS5DQW0fsklUoX6UO8esT lF1u+TFDaizMu5i1bl/CibiRzc5iT/E907ynBc2PZApcices8Eera8Ye8kGG2cz5 LIuf49OfTlq5zRQQLzrHSF5Tg4cVmxOH4XU3sbfPNxnvTVCBONq59LYvGsNBXuDH hQIDAQAB -----END PUBLIC KEY-----",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCIHj244Ah/Daca y55uhUv4JY9iqJhL/6litSOgJ7ejDCff3mjrwg+ZgObY0JiTXsPDHZsNbn8Hg4WD OfD55J4eDUrZGsJBvACsqyyN7PThW1UE4OjC/+Hy6yrpH+DXOwD9i1lMscxHS12v 1OifQ6kYFtz+qyACjvo4m8ZzLt3AJdxvNWSxyNRGJVDwauf7K+lLkNBbR+ySVShf pQ7x6xOUXW75MUNqLMy7mLVuX8KJuJHNzmJP8T3TvKcFzY9kClyJx6zwR6trxh7y QYbZzPksi5/j059OWrnNFBAvOsdIXlODhxWbE4fhdText883Ge9NUIE42rn0ti8a w0Fe4MeFAgMBAAECggEAJvWw6OeGxwbbW3oIYM3aTq5BehWTcb09eDksdzym/Q4P o63/Deu/l0ojyM77vMKU+ZXRuWh1B2uHnWXKKVxcPXHEiJt2GmZ7MvDTkdPOy2ne zcSqGpYuz96rq4oqSrBiui9WYfNJ6uYRbLBd3Kf7ECALJQFJ6jGOQQGlLXaulb5U n5aYSsoEh+LcAgouI2Hu9AC+OCv3owynKL8HiWlLbR8yJJ5zaE9egiGWn/VbFu1g EA1wzVXyG2bIFghzt6bexg7DIDqsBOwLHD1lLE3WTgPCmDM2zoOxX5PlDKdFDVG8 Mnt/18FO5xiCpAC7ZMFA2Vd8udKvQd0LSxOVA8MZSQKBgQDVyKyXhLvt8KxepGhs /VmXn+AHLLL6w69Z3Vb1gj/oF8nZjJmN3ETcXKt861UqM23Q4WDhmDhRduWE1hXh elw3jVHkDMQn4Ke5Kv/rZ8aszm+fZKgCjB2AF7nUaJ+cU/oSWHFpk+/S/KZWiHWc mVkDxoBhXCi/6QyLLB8WJGwaewKBgQCi/1zwo/9z3CCKEn8baQkReUDmifaG4PVs ZEAsz0WQ/bphRBQllwoL6xXTTuGAczfoEonSyH+jfm2sLcysMRpyAAPI2Q//d+b2 AFm+eBH/45TGKvfD7klYj830sSzYaA6i/Z2DziG7fmC/auJmgtT1wQ5UMjD3Oghk lCxzn6oF/wKBgGyR/Gz6wQJG/xMVhd8MD2r8i6a5IbBOnwgRa69FVbVGF4G/cOBl pCcRfRn03gyPj87MFwqa5scgjdGXdAdNv/WKdLNPdHMYGbXlS5E+49ww/ulBEj4w 8G50HjDsbVrUHyUf+4D1248YNlWt+aTtEBLlxZ8sUZmc/nzTjHoPR0NvAoGAFSKr uIBrdWiLx5uSY8mA5YUlhz9IekDdUgrFz4mo6Z4c9tPPEPi+0sDO+bF2yCMokq0k tfJNqrOQIQ1nRsSvOy0JUJfk3Sl9B1UQTgRfwSCPgAq+SeeyFwu+lwYKXJ1RmIzu SdMGyLsgbHG9nbFFUACSjRRdCRG7WN9lzDBd6Z0CgYAeg3Be/Kox+anF2pRulDa3 Ro9UiVPrsJQv/0qKO8vLsJyDyCFmaut2v1XPQm1c50gaQ5Crn/a1IavgVyoU5Kl8 RQJsaS/5ZgA5Hm1XIdv6edCNn8bvFw6927aC5BsRuwFzPzplplfJ2fQRQpBtpJN+ E4ZylXnYyCN1ar3WSp6/eQ== -----END PRIVATE KEY-----"
}
}
```

## 2. Token issuance and redemption
The bank issues tokens on the blockchain against fiat currency held by it in an escrow account. These tokens can be purchased / redeemed by investors, corporates and vendors. 

### 2.1 Creating a new token
To create a new token, the bank uses `post /api/v1/create_asset`

Sample input
```
```
Sample input
```
```

### 2.2 Creating additional units of a token
To create additional units of an open asset, use `post /api/v1/create_more_asset`

Sample input
```
```
Sample input
```
```
## 3. The invoice discounting process

### Step 1: Receipt of approved asset by bank
Corporate sends details of an approved invoice to its bank through the online banking system / app.

### Step 2: Publishing of invoice to the blockchain by the bank
The bank publishes the invoice (as an asset) to the blockchain using `post /api/v1/create_asset`. This asset is issued to the corporate who is the payer of that particular invoice.

Sample input
```
```
Sample input
```
```

### Step 3: Verification by corporate (payer)
The corporate verifies the details of the asset (invoice). 

If it is correct, the corporate (payer) transfers the asset (invoice) to the vendor who is the payee for that invoice. This is done using `post /api/v1/send_asset`

Sample input
```
```
Sample input
```
```

If it is incorrect, the corporate (payer) transfers the asset (invoice) to the burn address. This is done using `post /api/v1/send_asset`

Sample input
```
```
Sample input
```
```

### Step 4: Bidding by investors
Investors place bids on the invoice. To place a bid, they must hold sufficient quantity of tokens. Once they place a bid, the relevant amount of tokens are ‘locked’ till either (1) the vendor rejects the bid or (2) the investor cancels his bid.

To create the offer, use `post /api/v1/create_targeted_offer`

Sample input
```
```
Sample input
```
```
To cancel the offer, use `post /api/v1/cancel_targeted_offer`

Sample input
```
```
Sample input
```
```

### Step 5: Acceptance / rejection of bids by vendor
The vendor can view all bids placed on invoices in which he is the payee. The vendor can accept or reject bids. If the vendor accepts the bid, the asset (invoice) is transferred to the relevant investor and the bid amount is transferred to the vendor. The vendor can redeem the tokens from the bank.

To reject the offer, `post /api/v1/reject_targeted_offer`

Sample input
```
```
Sample input
```
```
To accept the offer, `post /api/v1/accept_offer`

Sample input
```
```
Sample input
```
```

### Step 6: Maturity of invoice
When the invoice matures, the corporate pays the relevant amount to the bank and receives equivalent tokens. 

### Step 7: Payment to investor
The corporate offers to exchange the asset (invoice) for the maturity amount. To create the offer, use `post /api/v1/create_targeted_offer`

Sample input
```
```
Sample input
```
```

The investor accepts the offer using `post /api/v1/accept_offer`

Sample input
```
```
Sample input
```
```

### Step 8: 
The corporate then sends the asset (invoice) to the burn address using `post /api/v1/send_asset`

Sample input
```
```
Sample input
```
```

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
