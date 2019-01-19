# Trade Chain

[![Primechain Technologies](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)
[![TRADE-Chain brochure](https://img.shields.io/badge/Download-Brochure-green.svg)](http://www.primechaintech.com/docs/brochures/Trade_Chain.pdf)

TRADE-Chain is the global trade finance blockchain for the US$ 12 trillion trade finance sector.

![TRADE-Chain](http://www.primechaintech.com/img/tradechain/tradechain_top.jpg)

### Table of contents   

[1. Executive summary](#1-executive-summary)   
[2. System requirements](#2-system-requirements)   
[3. API keys for the sandbox](#3-api-keys-for-the-sandbox)   
[4. Creating addresses](#4-creating-addresses)   
[5. Trade channels](#5-trade-channels)   
[6. Components and modules](#6-components-and-modules)   

# 1. Executive summary

International trade has existed for thousands of years and involves the exchange of capital, goods, and services across international borders. International trade represents a significant share of Gross Domestic Product (GDP) of most countries. 

Trade finance is an umbrella term for all the monetary activities related to commerce and international trade - lending, the issuance of letters of credit, factoring / invoice discounting, export credit and insurance. 

Trade financing protects against the unique risks of international trade - currency fluctuations, political instability, and issues of non-payment & creditworthiness.

The market for trade finance is estimated to be above US$ 12 trillion annually. (Source: World Trade Organization).

### Pain points of today’s trade finance process:

![Pain points of today’s trade finance process](http://www.primechaintech.com/img/api_documentation/trade_chain_pain_points.png)

### TRADE-Chain

Today, the Internet enables the movement of data (videos, text, photos) globally in milliseconds. But try moving value and you will be surprised by the costs, inefficiencies and time delays. Blockchain is a revolutionary technology that enables "internets of value" that can move value in seconds - money, trade documents, financial securities and more.

TRADE-Chain reduces errors, fraud, cost & time in the trade process and increases revenue, transparency, auditability and efficiency of trade operations.

![Components of TRADE-Chain](http://www.primechaintech.com/img/api_documentation/how-trade-chain-works.png)

***1. Blockchain Asset Layer:***  
This handles the asset lifecycle management (issuance, payment, exchange, escrow, retirement) for invoices, fiat backed tokens, goods & cargo contracts, loyalty programs.

***2. Database layer:***  
This powers the API key management and rating function.

***3. Blockchain Signature Engine:***  
This provides electronic signature functions for data and documents without the need to disclose the actual content being signed – secure key generation, signing and verification.

***4. Blockchain Storage Layer:***  
This holds the trade channels, encrypted & unencrypted data and documents.

***5. Blockchain Encryption Engine:***  
This provides symmetric (AES) and asymmetric (RSA) encryption functions – secure key generation, encryption and decryption.

***6. Blockchain-based authentication:***  
This combines the power of blockchain technology and public key cryptography for secure authentication and identification of people and devices.

***7. Primechain® API layer:***  
The above-mentioned layers and engines interact with the user systems through the Primechain® API layer.

### TRADE-Chain APIs can be easily and securely integrated with legacy and mobile applications ###

![Integration](http://www.primechaintech.com/img/api_documentation/trade_chain_integration.png)

### Information Security & TRADE-Chain

![Information Security & TRADE-Chain](http://www.primechaintech.com/img/api_documentation/trade_chain_infosec.png)


# 2. System requirements

The following types of TRADE-Chain nodes are available:
1. Importer and Exporters nodes
2. Bank nodes
3. Financer and investor nodes
4. Insurer nodes
5. Export credit agency nodes
6. Freight company nodes
7. Regulator nodes
8. Service provider nodes

### System requirements for nodes  
2 virtual machines / physical servers with the following details are required:   
* Ubuntu 16.04 machine with 32 GB RAM, 4 core processor, 100 GB SSD disk with ports 22, 15590 and 61172 open.   
* Ubuntu 16.04 machine with 32 GB RAM, 8 core processor, 25 GB SSD disk with ports 22 and 2512 open.   

# 3. API keys for the sandbox
API keys authenticate access to the TRADE-Chain sandbox. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header. ([See example](http://www.primechaintech.com/img/api_documentation/sample_rest_api_client.jpg))

Sample output
```
{
"status": 200,
"api_key": "zA-nTC$sKTn5VyYAhED66w3CVDBvJ7K6!c0Vbu0pMY13QtwCS&YfqIF0!1$qpHVv",
"message": {
14040: "A new API key has been successfully generated"
}
}
```

# 4. Creating addresses

Every node has a default address. If required, additional addresses can be created on a node using `get /api/v1/create_entity`. The following are generated:
1. public key
2. private key
3. primechain address

The output will be the newly created primechain address. The corresponding private key is automatically stored in your node. This will not be visible to other nodes. This address will have permissions to send and receive assets e.g. invoices, fiat currency backed tokens, etc.

Sample output
```
{
  "status": 200,
  "primechain_address": "1VCeqGYXLaqMtAFtxTNeTzfW8T714us2t3uwYM"
}
```

# 5. Trade channels

Storing all the data relating to a transaction, shipment or event in a dedicated trade channel enables quick and efficient data retrieval and processing.

## 5.1 Create a new trade channel
To create a new trade channel use `post /api/v1/create_trade_channel` and provide these 4 parameters:
1. `primechain_address` - your node's default primechain address. This is provided to you when your node connects to TRADE-Chain.
2. `trade_channel_name` - the trade channel name. This must be unique across the blockchain and can contain a maximum of 32 characters including blank spaces.
3. `trade_channel_details` - a short description of the trade channel
4. `open`: `true` or `false` 
    * if set to `true`, write permissions need not be explicitly provided. All addresses can write to the trade channel.
    * If set to `false`, write permissions need to be explicitly provided. 
    
***Note***: It is recommended to keep the set the value to `false` and to provide write permissions on an address basis. 

Sample input
```
{
  "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
  "trade_channel_name": "200_tons_unobtainium_march_2019",
  "trade_channel_details": "This trade channel is for the consignment of 200 tons of unobtainium",
  "open": false
}
```
The output is the transaction id of the transaction creating the trade channel - `tx_id`.

Sample output
```
{
  "status": 200,
  "tx_id": "70b06829af34c04bf13592e97bacd0923ba8bbf538f3621ec040f706f58a9553"
}
```

## 5.2 Grant write permissions to a trade channel
To grant an entity write permission to a trade channel, use `post /api/v1/grant_write_permission_to_trade_channel` and provide 3 parameters:
1. `trade_channel_writer` - the primechain address of the entity to be granted write permission to the trade channel.
2. `trade_channel_name` - the name of the relevant the trade channel.
3. `trade_channel_creator` - the primechain address of the creator of the trade channel.

***Note:*** This must be run on the node containing the private key of the `trade_channel_writer`.

Sample input
```
{
  "trade_channel_writer": "125LHLRKDDdaJSWXbVdaAGG7pGRT9dWPjjF7aG",
  "trade_channel_name": "200_tons_unobtainium_march_2019",
  "trade_channel_creator": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp"
}
```
Sample output
```
{
  "status": 200,
  "tx_id": "e4d05ba3a324c7b8768f4798e94636c018f2d3699d505679b8a2a7d532ebf638"
}
```

### 5.3 Revoke write permissions to a trade channel
To revoke an entity's write permission to a trade channel, use `post /api/v1/revoke_write_permission_to_trade_channel` and provide 3 parameters:
1. `trade_channel_writer` - the primechain address of the entity whose write permission is to be revoked.
2. `trade_channel_name` - the name of the relevant trade channel.
3. `trade_channel_creator` - the primechain address of the creator of the trade channel.

***Note:*** This must be run on the node containing the private key of the `trade_channel_creator`.

Sample input
```
{
  "trade_channel_writer": "125LHLRKDDdaJSWXbVdaAGG7pGRT9dWPjjF7aG",
  "trade_channel_name": "200_tons_unobtainium_march_2019",
  "trade_channel_creator": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp"
}
```
Sample output
```
{
  "status": 200,
  "tx_id": "ceed9a85f58a55543e8d2f6ea70e8507fc13341486acca9c49bee1bfeec03e4b"
}
```



# 6. Components and modules

1. Anti-Money Laundering review

2. Auction of goods and freight contracts

3. [Blockchain based authentication](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Authentication.MD)

4. [Cargo tracking](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/cargo_tracking.md)

5. [Cross border and domestic trade payments](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_payments.md)

6. [Electronic Signature Engine](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/electronic_signature_engine.MD)

7. [Encryption Engine](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/encryption_engine.md)

8. [Factoring / invoice discounting platform](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/invoice_discounting.md)

9. [File and data storage](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD)

10. [KYC and Digital Identity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/kyc_digital_id.md)

11. Loyalty program

12. Rating and review platform

13. Supply chain transparency and counterfeit reduction

14. [Trade documents issuance and sharing](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_documents.md)

---
Have a query? Email us on info@primechain.in
