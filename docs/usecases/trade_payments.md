# Trade payments

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

TRADE-Chain provides a platform for real-time cross-border and domestic trade payments.

![Trade documents issuance and sharing](http://www.primechaintech.com/img/api_documentation/trade_payments.jpg)

***Table of contents***

1. [Overview](#1-overview)   
2. [Issuance of a fiat currency backed token](#2-issuance-of-a-fiat-currency-backed-token)   
3. [Transfer token](#3-transfer-token)   
4. [Create additional units of an open token](#4-create-additional-units-of-an-open-token)   
[5. Balances of all tokens](#5-balances-of-all-tokens)   

# 1. Overview

A single TRADE-Chain transaction can perform an asset exchange between two or more parties, e.g. sending a dollar-denominated asset from Sanya to Tanya, while simultaneously sending a rupee-denominated asset from Tanya to Sanya. 

Because the exchange takes place in a single transaction, it comes with a guarantee of atomicity, meaning that all of the asset transfers take place simultaneously, or none take place at all. In the finance world, this type of transaction is termed delivery-versus-payment, or DvP for short.

### Process flow
1. A bank issues a fiat currency-backed token on TRADE-Chain.

2. Participants (exporters, importers, invoice payers, investors etc.) can purchase these tokens from the bank through regular banking channels.

3. Participants can send and receive tokens to / from each other in real-time. Since these transactions are atomic, there is no need for re-conciliation.

4. Participants can redeem these tokens from the issuer bank and receive fiat currency through regular banking channels.

# 2. Issuance of a fiat currency backed token

To create a new fiat currency backed token, use `post /api/v1/create_token`.

***Note:***
*  This may take upto 30 seconds.   
* `from_address` is the entity that creates the asset. It must have `send`, `receive` and `issue` permissions. It must also have permissions to write to TOKEN_MASTERLIST.
* `to_address` is the entity that receives the newly created asset. It must have `receive` permission and ideally also `send` permission.   
*  The `from_address` and `to_address` can be the same.
*  `unit` refers to the minimum divisible quantity of the asset.
* `asset` refers to the name of the asset.
* `quantity` refers to the initial quantity of the asset.
* `details` refers to any details about the asset.
* Setting `"open": "true"` will create an open asset - additional units of the asset CAN be issued in the future. 
* Setting `"open": "false"` will create a closed asset - additional units of the asset CANNOT be issued in the future. 

```
{
  "from_address": "1YYAavvJgKisoTB7sVakqKuMaMVwL5GbKJ1kai",
  "to_address": "1Mjas5NkmuLbumsx4ccmScDatHK7qFzQbHZXYi",
  "asset": 
  	{
    	"name": "National-Bank-USD-Series-B",
    	"open": true
  	},
  "unit": 1,
  "quantity": 19500,
  "details": 
     {
    	"backed_by": "Issued by National Bank against US dollar escrow account number 12345",
    	"redemption_information": "This is information about the redempton of the asset",
       	"contact_person": "These are the details of the contact person for this token"
  	}
}
```
***Output is:***
* `tx_id` - the txid of the transaction in which the token was created.
* `asset_ref` - the reference number of the token.
* `description` - the details relating to the token.
```
{
  "status": 200,
  "tx_id": "51f3569f42c3ffff0972bf6db2c32365afe1d26deabc4b4c0621007b66db38d0",
  "asset_ref": "767-267-21562",
  "description": 
    {
      "details": 
        {
          "backed_by": "Issued by National Bank against US dollar escrow account number 12345",
          "redemption_information": "This is information about the redempton of the asset",
          "contact_person": "These are the details of the contact person for this token"
        }
    }
}
```

# 3. Transfer token
To send tokens use `post /api/v1/send_asset` and pass 5 parameters - 
1. Sender's address
2. Receiver's address
3. Asset name or reference
4. Asset quantity
5. Details of the transaction
```
{
  "from_address": "1Mjas5NkmuLbumsx4ccmScDatHK7qFzQbHZXYi",
  "to_address": "1R1gwFwipsVbJTzoc2MVBwb79FgQ9LPDkpq2p3",
  "asset_name": "National-Bank-USD-Series-B",
  "quantity": 2500,
  "details": "These are the details of this transfer"
}
```
```
{
  "status": 200,
  "tx_id": "16cb1e2995b4d81ae99e59f45267311f6ce6e06babe02933b5c534318802944a"
}
```
The output is the id of the transaction in which the token was transferred.


# 4. Create additional units of an open token

To create additional units of an open token, use `post /api/v1/create_more_token`.

***Note:***
* `from_address` is the entity that creates the asset. It must have `send` permission.
* `to_address` is the entity that receives the newly created asset. It must have `receive` permission.
* The `from_address` and `to_address` can be the same.
* `asset_name` refers to the name of the asset.
* `quantity` refers to the additional quantity of the asset being issued.
```
{
  "from_address": "1YYAavvJgKisoTB7sVakqKuMaMVwL5GbKJ1kai",
  "to_address": "1Mjas5NkmuLbumsx4ccmScDatHK7qFzQbHZXYi",
  "asset_name": "National-Bank-USD-Series-B",
  "quantity": 15000
}
```
```
{
  "status": 200,
  "tx_id": "eb965639e76b06bcd9f4f19caea58ace8f5de83aa71066d88b4ff1d1ae4f85d1"
}
```
Output is the id of the transaction in which the additional units were created.

# 5. Balances of all tokens

To get the name, asset ref and balance of all assets, use `get /api/v1/asset_balances`

Sample output
```
{
"status": 200,
"asset_balance": 
  [
    {
        "name": "National-Bank-USD-Series-A",
        "assetref": "755-266-47872",
        "qty": 19500
     },
     {
        "name": "National-Bank-USD-Series-B",
        "assetref": "767-267-21562",
        "qty": 34500
      },
  ],
}
```

---
Have a query? Email us on info@primechain.in

