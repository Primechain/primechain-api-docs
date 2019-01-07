# Letter of Credit

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

A letter of credit is like a promissory note that represents an obligation taken on by a bank to make a payment once certain criteria are met - once the terms are completed and confirmed, the bank will transfer the funds. Simply put, a letter of credit ensures that the payment will be made as long as the services are performed.

![Letter of credit](http://www.primechaintech.com/img/api_documentation/trade-chain.jpg)

***Example:*** An Indian exporter receives an order from an American importer. The exporter is not sure about the importer’s ability and willingness to pay once the order is delivered. The exporter requests for a letter of credit from the importer. The importer then applies for a letter of credit from its bank (where it has adequate funds or credit line). Once the goods are shipped, the bank pays the exporter subject to fulfilment of relevant terms and conditions. 

Letters of credit are especially important in international trade due to the distance involved and potentially differing laws in the countries of the businesses involved. In these transactions, it is not always possible for the parties to meet in person. The bank issuing the letter of credit holds payment on behalf of the buyer until it receives confirmation that the goods in the transaction have been shipped. (Source: Investopedia)

***Table of contents:***   

[Step 1: Agreement to purchase goods](#step-1-agreement-to-purchase-goods)   
[Step 2: Application for a letter of credit](#step-2-application-for-a-letter-of-credit)   
[Step 3: Issue of the letter of cedit](#step-3-issue-of-the-letter-of-cedit)   
[Step 4: Shipping of goods](#step-4-shipping-of-goods)   
[Step 5: Presenting of documents by the seller](#step-5-presenting-of-documents-by-the-seller)   
[Step 6: Examination of documents by the issuing bank](#step-6-examination-of-documents-by-the-issuing-bank)   
[Step 7: Issuing bank obtains payment from the buyer](#step-7-issuing-bank-obtains-payment-from-the-buyer)   
[Step 8: Issuing bank forwards documents to the buyer](#step-8-issuing-bank-forwards-documents-to-the-buyer)   
[Step 9: Buyer picks up the goods](#step-9-buyer-picks-up-the-goods)   
[Step 10: Seller receives the payment](#step-10-seller-receives-the-payment)

## Step 1: Agreement to purchase goods
The buyer agrees to purchase goods from the seller. This agreement may be a purchase order, an accepted pro-forma invoice, a formal contract, or an informal exchange of messages. Agreement is made as to goods being purchased, how and when they are to be shipped and insured, and that a letter of credit will be used as the mechanism of payment.

1. In case the purchase order, invoice, formal contract etc. is to be issued directly on the blockchain, the relevant API end-point is [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain). Also see formats for issuing and sharing [trade documents](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_documents.md) on the blockchain.

2. In case the purchase order, invoice, formal contract etc. is issued off-chain and then stored on the blockchain, the relevant API end-point is [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain) 

3. In case the purchase order, invoice, formal contract etc. is issued off-chain and NOT stored on the blockchain, the relevant end-points are [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data), [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature) and [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great).

## Step 2: Application for a letter of credit
The buyer applies to his bank for a letter of credit, by signing the bank's letter of credit application/agreement form.

1. In case the application for a letter of credit is to be made directly on the blockchain, the relevant API end-point is [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain).

2. In case the application for a letter of credit is to be made off-chain and then stored on the blockchain, the relevant API end-point is [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)   

3. In case the application for a letter of credit is issued off-chain and NOT stored on the blockchain, the relevant end-points are [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data), [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature) and [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great).

## Step 3: Issue of the letter of cedit
After approving the application, the issuing bank issues the actual letter of credit instrument and sends it to the seller (beneficiary).

1. In case the letter of credit is to be issued directly on the blockchain, the relevant API end-point is [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain).

2. In case the letter of credit is to be issued off-chain and then stored on the blockchain, the relevant API end-point is [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)   

3. In case the letter of credit is issued off-chain and NOT stored on the blockchain, the relevant end-points are [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data), [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature) and [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great).

## Step 4: Shipping of goods
Having received the issuing bank's assurance of payment, the seller ships the goods to the buyer.

## Step 5: Presenting of documents by the seller
The seller prepares the documents called for in the letter of credit and presents them to the issuing bank.

1. In case the documents are to be issued directly on the blockchain, the relevant API end-point is [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain). Also see formats for issuing and sharing [trade documents](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_documents.md) on the blockchain.

2. In case the documents are to be issued off-chain and then stored on the blockchain, the relevant API end-point is [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)   

3. In case the documents are issued off-chain and NOT stored on the blockchain, the relevant end-points are [`create_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#1-signing-data), [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature) and [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great).

## Step 6: Examination of documents by the issuing bank
The issuing bank examines the documents. If it determines that the documents comply with the letter of credit, the issuing bank pays the seller.

1. In case the documents were issued directly on the blockchain, the relevant API end-point is [`decrypt_download_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#3-decrypt-verify-and-retrieve-data-from-the-blockchain). 

2. In case the documents were issued off-chain and then stored on the blockchain, the relevant API end-point is [`decrypt_download_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)   

3. In case the documents were issued off-chain and NOT stored on the blockchain, the relevant end-points are [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature).

## Step 7: Issuing bank obtains payment from the buyer
The issuing bank obtains payment from the buyer in accordance with the terms of the letter of credit agreement. 

1. The relevant API end points for tokenizing fiat currency for this are: [`create_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset) and [`create_more_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset).

2. The relevant API end points for onboarding relevant entities (buyer, seller etc.) are [`create_entity`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity), [`create_keypair`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management) and [`create_entity_rsa`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-creating-a-new-entity-with-rsa-keys) 

3. The relevant API end points for transferring tokenized fiat currency are [`send_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#6-transfer-asset-when-private-key-is-in-the-node), [`transfer_multisign_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#7-transfer-asset-from-multisig-address) and [`transfer_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#8-transfer-asset-when-private-key-is-not-in-the-node)

## Step 8: Issuing bank forwards documents to the buyer
The issuing bank forwards the documents to the buyer.

1. In case the documents were issued directly on the blockchain, the relevant API end-point is [`decrypt_download_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#3-decrypt-verify-and-retrieve-data-from-the-blockchain). 

2. In case the documents were issued off-chain and then stored on the blockchain, the relevant API end-point is [`decrypt_download_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)   

3. In case the documents were issued off-chain and NOT stored on the blockchain, the relevant end-points are [`verify_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#2-verifying-a-digital-signature).

## Step 9: Buyer picks up the goods
The buyer uses the documents to pick up the merchandise from the carrier, completing the letter of credit cycle.

## Step 10: Seller receives the payment
The issuing bank pays the seller.

1. The relevant API end points for tokenizing fiat currency for this are: [`create_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset) and [`create_more_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#2-create-additional-units-of-an-open-asset).

2. The relevant API end points for onboarding relevant entities (buyer, seller etc.) are [`create_entity`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#1-creating-a-new-entity), [`create_keypair`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#2-creating-a-new-entity-for-external-key-management) and [`create_entity_rsa`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Entities.MD#3-creating-a-new-entity-with-rsa-keys) 

3. The relevant API end points for transferring tokenized fiat currency are [`send_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#6-transfer-asset-when-private-key-is-in-the-node), [`transfer_multisign_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#7-transfer-asset-from-multisig-address) and [`transfer_asset`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#8-transfer-asset-when-private-key-is-not-in-the-node)

Have a query? Email us on info@primechain.in
