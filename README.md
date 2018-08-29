# Primechain API Documentation

[![Primechain-API](https://img.shields.io/badge/Built%20on-Primechain--API-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

Documentation for [Primechain API](https://github.com/Primechain/primechain-api)

***Note:*** Remember to pass the [API key](https://github.com/Primechain/primechain-api-docs/blob/master/docs/API%20key%20management.MD#2-passing-the-api-key) in the Authorization header. 

## 1. [Blockchain administration](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD)
1. [Blockchain parameters](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#1-blockchain-parameters)
2. [Runtime parameters](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#2-runtime-parameters)
3. [Blockchain information](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#3-blockchain-information)
4. [Memory pool information](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#4-memory-pool-information)
5. [Raw memory pool](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#5-raw-memory-pool)
6. [List blocks](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#6-list-blocks)
7. [Peer info](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Blockchain%20administration.MD#7-peer-info)

## 2. [Entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD)
1. [Creating a new entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity)
2. [Creating a new entity (for external key management)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management)
3. [List entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-list-entities)
4. [Create multisig address](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#4-create-multisig-address)
5. [Grant permissions to an entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#5-grant-permissions-to-an-entity)
6. [Revoke permissions to an entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#6-revoke-permissions-to-an-entity)
7. [List permissions given to all entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#7-list-permissions-given-to-all-entities)
8. [Information about the addresses in the wallet](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#8-information-about-the-addresses-in-the-wallet)
9. [Validate address](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#9-validate-address)

## 3. [Digital Signatures](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD)
1. [Signing data](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data)
2. [Verifying a digital signature](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature)

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

## 5. [Smart Asset Lifecycle Management](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD)
1. [Create a new asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset)
2. [Create additional units of an open asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset)
3. [Details of a specified asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#3-details-of-a-specified-asset)
4. [Balances of all assets](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#4-balances-of-all-assets)
5. [Assets held by specified entities](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#5-assets-held-by-specified-entities)
6. [Transfer asset](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#6-transfer-asset)
7. [Transactions by a specified entity](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#7-transactions-by-a-specified-entity)

## 6. [Offer management](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD)
1. [Create an offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#1-create-an-offer)
2. [Read an offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#2-read-an-offer)
3. [Accept an offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#3-accept-an-offer)
4. [Reject an offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#4-reject-an-offer)
5. [Cancel an offer](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#5-cancel-an-offer)

## Others
[Changing an end-point](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Changing%20an%20end-point.MD)
