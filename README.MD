# Primechain API

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

Primechain APIs make it very simple for developers to add blockchain power to their code - smart asset lifecycle management, electronic signatures, encrypted data storage & more.

![Primechain-API](http://www.primechaintech.com/images/projects/api-github.png)

[![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Add%20blockchain%20power%20to%20your%20code%20in%20minutes%20with%20primechain-api&url=https://github.com/Primechain/primechain-api&via=primechain&hashtags=blockchain,api)

1. [Introduction](#1-introduction)
2. [Documentation](#2-documentation)
3. [Sandbox](#3-sandbox)
4. [Availability](#4-availability)
5. [About Primechain Technologies](#5-about-primechain-technologies)
6. [Use cases](#6-use-cases)

## 1. Introduction
Blockchain is a world-changing technology, but it suffers from some pain points:
1.	Installing, configuring, securing, troubleshooting, updating, and maintaining a blockchain ecosystem is a complex and time consuming task.
2.	There are 100+ blockchains and distributed ledger systems to choose from
3.	Building blockchain solutions from the ground up is very expensive and time consuming.
4. There is a severe shortage of skilled blockchain developers.
 
Primechain APIs make it very simple for developers to add blockchain power to their code - smart asset lifecycle management, electronic signatures, encrypted data storage & more.

***A typical Primechain node:***
![Primechain-node](http://www.primechaintech.com/img/api_documentation/node2.png)

***Typical internal setup***
![Typical internal setup](http://www.primechaintech.com/img/api_documentation/b2_internal.png)

![Illustrative layout](http://www.primechaintech.com/img/api_documentation/b2_outline2.png)


## 2. Documentation
Prmechain API documentation is available at:    
https://github.com/Primechain/primechain-api-docs/blob/master/Documentation.md

To try Primechain API, you can use [Advance REST Client](https://install.advancedrestclient.com/install) or a similar tool.

![Primechain-API](http://www.primechaintech.com/img/api_documentation/rest.png)

## 3. Sandbox
Email us on info@primechain.in for details on accessing the Primechain-API sandbox.

To view a sample nodeJS application built on Primechain-API at:
http://169.63.131.117:2206/user/dashboard

## 4. Availability
Primechain-API is available in 2 modes:
* a node on Primechain-MONEY, a multi-framework permissioned blockchain available only to BankChain members. The API runs on your infrastructure (on-cloud / on-premise).
* dedicated service - this is where the API runs on your infrastructure (on-cloud / on-premise) and all the data is stored on your infrastructure (on-cloud / on-premise).

## 5. About Primechain Technologies
Primechain API are developed and maintained by [Primechain™ Technologies Pvt. Ltd.](http://www.primechaintech.com), a blockchain startup with the mission of building blockchains for a better world. We operate the Bankchain community of banks and maintain the Blockchain Security Controls. 

## 6. Use cases
A partial list of Primechain-API use cases is at:   
https://github.com/Primechain/primechain-api-docs/blob/master/use-cases.MD

## 7. Standards and algorithms

[Federal Information Processing Standard (FIPS) 186-4, Digital Signature Standard (DSS)](https://csrc.nist.gov/publications/detail/fips/186/4/final), specifies three NIST-approved digital signature algorithms: DSA, RSA, and ECDSA. All three are used to generate and verify digital signatures, in conjunction with an approved hash function specified in [FIPS 180-4, Secure Hash Standard](https://csrc.nist.gov/publications/detail/fips/180/4/final) or [FIPS 202, SHA-3 Standard: Permutation-Based Hash and Extendable-Output Functions](https://csrc.nist.gov/publications/detail/fips/202/final).

## 8. Glossary of terms
* AAD: Additional Authenticated Data 
* AES: Advanced Encryption Standard.
* Authentication Tag (Tag): A cryptographic checksum on data that is designed to reveal both accidental errors and the intentional modification of the data. 
* GCM: Galois/Counter Mode
* Initialization Vector: A nonce that is associated with an invocation of authenticated encryption on a particular plaintext and AAD.   

For more information, see [NIST Special Publication 800-38D](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-38d.pdf)
