# Primechain API Documentation

[![Built by Primechain](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

Documentation for [Primechain API](https://github.com/Primechain/primechain-api)

API keys authenticate access to Primechain-API powered blockchains. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header. ([See example](http://www.primechaintech.com/img/api_documentation/sample_rest_api_client.jpg))

## 1. [Blockchain administration](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD)
1. [Blockchain parameters](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#1-blockchain-parameters)
2. [Runtime parameters](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#2-runtime-parameters)
3. [Blockchain information](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#3-blockchain-information)
4. [Memory pool information](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#4-memory-pool-information)
5. [Raw memory pool](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#5-raw-memory-pool)
6. [List blocks](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#6-list-blocks)
7. [Peer info](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#7-peer-info)

## 2. [Entity creation & permissions management](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD)
1. [Creating a new entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity)
2. [Creating a new entity (for external key management)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management)
3. [Creating a new entity (with RSA keys)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-creating-a-new-entity-with-rsa-keys)
4. [Create multisig address](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#4-create-multisig-address)
5. [Grant permissions to an entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#5-grant-permissions-to-an-entity)
6. [Revoke permissions to an entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#6-revoke-permissions-to-an-entity)
7. [List permissions given to all entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#7-list-permissions-given-to-all-entities)
8. [Information about the addresses in the wallet](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#8-information-about-the-addresses-in-the-wallet)
9. [Validate address](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#9-validate-address)
10. [List entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#10-list-entities)

## 3. [Electronic Signatures](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Electronic%20signatures.MD)
1. [Signing data](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data)
2. [Verifying a digital signature](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature)   
3. [Sign and store signature in GREAT](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great)

## 4. [Data Streams](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD)
1. [Create data stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#1-create-data-stream)
2. [List data streams](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#2-list-data-streams)
3. [Grant write permission to a stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#3-grant-write-permission-to-a-stream)
4. [Subscribe node to a data stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#4-subscribe-node-to-a-data-stream)
5. [Unsubscribe node from a data stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#5-unsubscribe-node-from-a-data-stream)
6. [Write to a data stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#6-write-to-a-data-stream)
7. [List stream items by key](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#7-list-stream-items-by-key)
8. [List stream items by publisher](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#8-list-stream-items-by-publisher)
9. [List keys in a specified stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#9-list-keys-in-a-specified-stream)
10. [Retrieve all data from a specified stream](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Data%20streams.MD#10-retrieve-all-data-from-a-specified-stream)

## 5. [Smart Asset Lifecycle Management](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD)
1. [Create a new asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset)
2. [Create additional units of an open asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset)
3. [Details of a specified asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#3-details-of-a-specified-asset)
4. [Balances of all assets](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#4-balances-of-all-assets)
5. [Assets held by specified entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#5-assets-held-by-specified-entities)
6. [Transfer asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#6-transfer-asset)
7. [Transactions by a specified entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#7-transactions-by-a-specified-entity)

## 6. [Offer management](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD)

1. [Create a public offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#1-create-a-public-offer)   
2. [Get list of open public offers](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#2-get-list-of-open-public-offers)   
3. [Read an offer](#3-read-an-offer)   
4. [Accept an offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-accept-an-offer)   
5. [Cancel a public offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#5-cancel-a-public-offer)  
6. [Create a targeted offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#6-create-a-targeted-offer)   
7. [Reject a targeted offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#7-reject-a-targeted-offer)  

## 7. [Encrypted data storage](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD)

1. [Introduction](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#1-introduction)
2. [Sign, encrypt and store data in the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain)
3. [Decrypt, verify and retrieve data from the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#3-decrypt-verify-and-retrieve-data-from-the-blockchain)
4. [Sign, encrypt and store a file in the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)
5. [Decrypt, verify and retrieve a file from the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)

## 8. [Blockchain based authentication](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Authentication.MD)

1. [Onboarding an entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Authentication.MD#1-onboarding-an-entity)   
2. [Authentication](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Authentication.MD#2-authentication)

## 9. [List of data streams](https://github.com/Primechain/primechain-api-docs/blob/master/docs/List%20of%20data%20streams.MD)

## 10. [Use cases](https://github.com/Primechain/primechain-api-docs/blob/master/use-cases.MD)

## 11. [Utilities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Utilities.MD)

1. [Upgrading Primechain-API](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Utilities.MD#1-upgrading-primechain-api)    
2. [Create passwords](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Utilities.MD#2-create-passwords)   
3. [Create UUID](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Utilities.MD#3-create-uuid)   

## 12. [Hyperledger Sawtooth](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD)

1. [Create key pair](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#1-create-key-pair)
2. [Publish data to the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#2-publish-data-to-the-blockchain)
3. [Retrieve data from the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#3-retrieve-data-from-the-blockchain)
4. [Creating a digital signature](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#4-creating-a-digital-signature)   
5. [Verify a digital signature](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#5-verify-a-digital-signature)   
6. [Create, encrypt, sign and publish data to the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#6-create-encrypt-sign-and-publish-data-to-the-blockchain)   
7. [Decrypt, verify and retrieve data from the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#7-decrypt-verify-and-retrieve-data-from-the-blockchain)   
8. [Sign, encrypt and store a file in the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#8-sign-encrypt-and-store-a-file-in-the-blockchain)   
9. [Decrypt, verify and retrieve a file from the blockchain](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Hyperledger%20Sawtooth.MD#9-decrypt-verify-and-retrieve-a-file-from-the-blockchain)  
