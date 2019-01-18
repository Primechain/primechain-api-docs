# Trade Chain

[![Primechain Technologies](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)
[![TRADE-Chain brochure](https://img.shields.io/badge/Download-Brochure-green.svg)](http://www.primechaintech.com/docs/brochures/Trade_Chain.pdf)

TRADE-Chain is the global trade finance blockchain for the US$ 12 trillion trade finance sector.

![TRADE-Chain](http://www.primechaintech.com/img/tradechain/tradechain_top.jpg)

### Table of contents   

[1. Executive summary](#1-executive-summary)

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

![Components of TRADE-Chain
](http://www.primechaintech.com/img/api_documentation/trade_chain_components.png)

***1. Blockchain layer:***  
This holds the trade channels, encrypted and unencrypted data relating to trade documents & KYC records, and handles the asset lifecycle management – invoices, fiat backed tokens, goods & cargo contract, loyalty programs.

***2. Database layer:***  
This powers the API key management and rating function.

***3. Electronic Signature Engine:***  
This provides electronic signature functions for data and documents without the need to disclose the actual content being signed – secure key generation, signing and verification.

***4. File Storage Layer:***  
This provides a dedicated blockchain powered storage service for encrypted and un-encrypted data and document storage.

***5. Encryption Engine:***  
This provides symmetric (AES) and asymmetric (RSA) encryption functions – secure key generation, encryption and decryption.

***6. Blockchain based authentication:***  
This combines the power of blockchain technology and public key cryptography for secure authentication and identification of people and devices.

***7. Primechain® API layer:***  
The above-mentioned layers and engines interact with the user systems though the Primechain® API layer.

### TRADE-Chain APIs can be easily and securely integrated with legacy and mobile applications ###

![Integration](http://www.primechaintech.com/img/api_documentation/trade_chain_integration.png)

### Information Security & TRADE-Chain

![Information Security & TRADE-Chain](http://www.primechaintech.com/img/api_documentation/trade_chain_infosec.png)



### 1.2 TRADE-Chain nodes
TRADE-Chain is a permissioned blockchain powered by Primechain APIs. The following types of TRADE-Chain nodes are available:
1. Importer and Exporters nodes
2. Bank nodes
3. Financer and investor nodes
4. Insurer nodes
5. Export credit agency nodes
6. Freight company nodes
7. Regulator nodes
8. Service provider nodes

To access the TRADE-Chain sandbox, email us on info@primechain.in

***System requirements for nodes***   
2 virtual machines / physical servers with the following details are required:   
* Ubuntu 16.04 machine with 32 GB RAM, 4 core processor, 100 GB SSD disk with ports 22, 15590 and 61172 open.   
* Ubuntu 16.04 machine with 32 GB RAM, 8 core processor, 25 GB SSD disk with ports 22 and 2512 open.   

### 1.3 API keys for sandbox
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

### 1.4 Creating addresses
If required, additional addresses can be created on a node using `get /api/v1/create_entity`. The following are generated:
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



---
Have a query? Email us on info@primechain.in
