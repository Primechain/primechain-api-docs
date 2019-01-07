# Bank guarantee

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

Through a bank guarantee, a bank promises to cover a loss if a borrower defaults. Types of guarantees include Advance Payment Guarantee, Bid Bond Guarantee, Confirmed Payment Order, Credit Security Bond, Deferred Payment Guarantee, Financial Guarantee, Foreign Bank Guarantee, Performance Bond, Performance Guarantee, Rental Guarantee, and Warranty bond.

![Bank guarantees on the blockchain](http://www.primechaintech.com/img/api_documentation/guarantee.jpg)

***Some of the benefits of using blockchain for issuing bank guarantees are:***    
(1) Each bank guarantee is digitally signed by the issuing bank.   
(2) Regulator nodes enable real-time supervision by the authorities.   
(3) The system is API driven and can easily be integrated with the banks' core banking and other legacy systems.   
(4) Each bank guarantee is automatically encrypted and the decryption credentials are only available to the issuing bank.   

### Steps involved

1. [Issuing a bank guarantee](#1-issuing-a-bank-guarantee)   
2. [Retrieving a bank guarantee](#2-retrieving-a-bank-guarantee)

## Issuing a bank guarantee

1. In case the bank guarantee is to be issued directly on the blockchain, the relevant API end-point is [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain). Also see formats for issuing and sharing [`trade documents`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_documents.md) on the blockchain. Also see the suggested format of the bank guarantee at https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_documents.md#4-bank-guarantee

2. In case the bank guarantee is issued off-chain and then stored on the blockchain, the relevant API end-point is [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain) 

3. In case the bank guarantee is issued off-chain and NOT stored on the blockchain, the relevant end-points are [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data), and [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great).

## Retrieving a bank guarantee

1. In case the bank guarantee was issued directly on the blockchain, the relevant API end-point is [`decrypt_download_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#3-decrypt-verify-and-retrieve-data-from-the-blockchain). 

2. In case the bank guarantee was issued off-chain and then stored on the blockchain, the relevant API end-point is [`decrypt_download_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)   

3. In case the bank guarantee was issued off-chain and NOT stored on the blockchain, the relevant end-point is [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature).

Have a query? Email us on info@primechain.in
