# Letter of credit

TRADE-Chain is a permissioned "global trade finance" blockchain for the world’s banks and financial institutions. TRADE-Chain is operated by [Primechain Technologies Private Limited](http://www.primechaintech.com/). TRADE-Chain enables the issuance and sharing of letters of credit.

![Letter of credit](http://www.primechaintech.com/img/api_documentation/letter_of_credit.jpg)

Table of contents:   

[1. Introduction](#1-introduction)   

[2. Benefits of using blockchain for letters of credit](#2-benefits-of-using-blockchain-for-letters-of-credit)   

[3. TRADE-Chain](#3-trade-chain)   
[3.1 Core features of TRADE-Chain](#31-core-features-of-trade-chain)   
[3.2 Hyperledger Sawtooth](#32-hyperledger-sawtooth)      
[3.3 On-boarding an issuer of Letters of Credit](#33-on-boarding-an-issuer-of-letters-of-credit)   
[3.4 Publishing a letter of credit to TRADE-Chain](#34-publishing-a-letter-of-credit-to-trade-chain)   
[3.5 Retrieving a letter of credit from TRADE-Chain](#35-retrieving-a-letter-of-credit-from-trade-chain)   


# 1. Introduction

A letter of credit is like a promissory note that represents an obligation taken on by a bank to make a payment once certain criteria are met - once the terms are completed and confirmed, the bank will transfer the funds. Simply put, a letter of credit ensures that the payment will be made as long as the services are performed.

***Example:*** An Indian exporter receives an order from an American importer. The exporter is not sure about the importer’s ability and willingness to pay once the order is delivered. The exporter requests for a letter of credit from the importer. The importer then applies for a letter of credit from its bank (where it has adequate funds or credit line). Once the goods are shipped, the bank pays the exporter subject to fulfilment of relevant terms and conditions. 

Letters of credit are especially important in international trade due to the distance involved and potentially differing laws in the countries of the businesses involved. In these transactions, it is not always possible for the parties to meet in person. The bank issuing the letter of credit holds payment on behalf of the buyer until it receives confirmation that the goods in the transaction have been shipped. (Source: Investopedia)

# 2. Benefits of using blockchain for letters of credit

1. A conventional Letter of Credit transaction involves time consuming manual processes such as the transfer of physical copies by post, courier, fax or scans. The use of blockchain offers significant potential to reduce the timelines involved in exchange of export documentation from the extant 7 to 10 days to less than a day. (Source: shippingandfreightresource.com)

2. Use of blockchain in trade finance enhances transparency, security and synergy across all the parties and stakeholders involved. 

3. Blockchain brings efficiency to trade finance and ensures cost effectiveness, quicker turnaround and unlocks liquidity for businesses.

4. Blockchain technology usage for trade finance “enables automation of LC creation, payment against documents...” (Source: Reserve Bank of India’s 2017 Report of the Working Group on FinTech and Digital Banking).

5. Blockchain will have a transformative impact on trade finance transactions, enable greater transparency, and offer simpler and faster transactions. (Source: morethanshipping.com)


# 3. TRADE-Chain

TRADE-Chain is a permissioned global trade finance blockchain for the world’s banks and financial institutions. TRADE-Chain is operated by [Primechain Technologies Private Limited](http://www.primechaintech.com/). 

## 3.1 Core features of TRADE-Chain

1. A complete API driven system that can easily be integrated with legacy systems.

2. Enables real-time supervision by the authorities.

3. All data is automatically encrypted and the decryption credentials are only available to the issuing entity.

4. By storing data across its network, TRADE-Chain eliminates the security risks that come with data being held centrally. 

5. The use of Public key cryptography, symmetric cryptography and cryptographic hash functions makes TRADE-Chain cryptographically secure and provably immutable.

6. TRADE-Chain maximizes efficiency, security & transparency and minimizes fraud.

7. TRADE-Chain greatly improve auditability and streamlines documentation.

## 3.2 Hyperledger Sawtooth

TRADE-Chain is built on Hyperledger Sawtooth.

Hyperledger Sawtooth is an enterprise blockchain platform for building distributed ledger applications and networks. The design philosophy targets keeping ledgers distributed and making smart contracts safe, particularly for enterprise use.

Sawtooth simplifies blockchain application development by separating the core system from the application domain. Application developers can specify the business rules appropriate for their application, using the language of their choice, without needing to know the underlying design of the core system.

Sawtooth is also highly modular. This modularity enables enterprises and consortia to make policy decisions that they are best equipped to make. Sawtooth’s core design allows applications to choose the transaction rules, permissioning, and consensus algorithms that support their unique business needs.

Sawtooth is an open source project under the Hyperledger umbrella. For more information see: https://sawtooth.hyperledger.org/


## 3.3 On-boarding an issuer of Letters of Credit

To on-board an issuer of Letters of Credit, use `get /api/v1/create_user_key_sawtooth`

The output will be the 
1. The private key of the newly created issuer
2. The public key of the newly created issuer

Sample output
```
{
"status": 200,
"primechain_sawtooth_private_key": "89b0d0a7ef410e9dc19907b8d9297ec2239222c2b38d56056964495b517fe6c1",
"primechain_sawtooth_public_key": "02b023ef5ce8f6ef4e3419ebc925060ceb3ed9f80c489e34fb93033956581b4941",
"response": "User keys generated"
}
```

## 3.4 Publishing a letter of credit to TRADE-Chain

To create, encrypt, sign and publish a Letter of Credit to the blockchain, use `post /api/v1/encrypt_sign_store_data_sawtooth` and pass 2 parameters: 
1. the primechain sawtooth private key 
2. the data 

***Sample input***
```
{
  "primechain_sawtooth_private_key": "89b0d0a7ef410e9dc19907b8d9297ec2239222c2b38d56056964495b517fe6c1",
  "data": 
    {
      "LOC_FORM": "IRREVOCABLE",
      "LOC_NUMBER": "32453675864534",
      "LOC_DATE_OF_ISSUE": "17-DECEMBER-2018",
      "LOC_DATE_OF_EXPIRY": "16-MARCH-2019",
      "LOC_PLACE_OF_EXPIRY": "MUMBAI, INDIA",
      "LOC_APPLICANT_BANK": "GLOBAL BANK, GENEVA, SWITZERLAND",
      "LOC_APPLICANT": "NICOLE CORPORATION",
      "LOC_BENEFICIARY": "KIDMAN INC, ADELAIDE, AUSTRALIA",
      "LOC_CURRENCY": "USD",
      "LOC_AMOUNT_WORDS": "TWO MILLION",
      "LOC_AMOUNT_FIGURES": "2,000,000.00",
      "LOC_MAX_CREDIT_AMOUNT": "NOT EXCEEDING",
      "LOC_AVAILABLE_WITH": "ANY BANK",
      "LOC_AVAILABLE_BY": "BY NEGOTIATION",
      "LOC_DRAFTS_AT": "SIGHT",
      "LOC_DRAWEE": "INTERNATIONAL BANK, NEW YORK, USA",
      "LOC_PARTIAL_SHIPMENTS": "ALLOWED",
      "LOC_TRANSHIPMENT": "NOT ALLOWED",
      "LOC_FOR_TRANSPORTATION_TO": "MUMBAI, INDIA",
      "LOC_LATEST_DATE_OF_SHIPMENT": "17-JANUARY-2018",
      "LOC_DESCRIPTION_GOODS_SERVICES": "PLATINUM RODS",
      "LOC_QUANTITY_GOODS_SERVICES": "2000",
      "LOC_UNIT_PRICE_GOODS_SERVICES": "1000",
      "LOC_TRADE_TERMS": "CIF MUMBAI",
      "LOC_ORDER_NUMBER": "435346453",
      "LOC_DOCUMENTS_REQUIRED": "1.BENEFICIARY'S DRAFT AT SIGHT DRAWN ON BUYER'S BANK NAME, ADDRESS, MARKED 'DRAWN UNDER BUYER'S BANK NAME IRREVOCABLE LETTER OF CREDIT NO.XXX DATED XXX'. 2. SIGNED COMMERCIAL INVOICE IN TRIPLICATE. 3. PACKING LIST IN TRIPLICATE, INDICATING WEIGHT AND MEASUREMENT. 4. FULL SET (3 ORIGINALS AND 3 COPIES) OF CLEAN ON BOARD BILLS OF LADING MADE OUT TO ORDER OF SHIPPER AND BLANK ENDORSED MARKED 'FREIGHT PREPAID' AND NOTIFY APPLICANT. 5. INSURANCE POLICY IN DUPLICATE ENDORSED IN BLANK FOR 110 PERCENT OF THE INVOICE VALUE INCLUDING ALL RISKS, WAR CLAUSES AND S.R.C.C. 6. CERTIFICATE OF ORIGIN IN 3 ORIGINALS AND 2 COPIES ISSUED BY CHAMBER OF COMMERCE.",
      "LOC_ADDITIONAL_CONDITIONS": "THE COMPLETE SET OF ORIGINAL DOCUMENTS TO BE SENT IN ONE LOT BY THE COURIER SERVICE TO APPLIANT BANK.",
      "LOC_CHARGES": "ALL BANKING CHARGES ARE FOR BENEFICIARY'S ACCOUNT.",
      "LOC_PERIOD_FOR_PRESENTATION": "DOCUMENTS MUST BE PRESENTED WITHIN THE VALIDITY OF THIS CREDIT.",
      "LOC_CONFIRMATION_INSTRUCTIONS": "CONFIRM",
      "LOC_ADVISING_THROUGH_BANK": "STATE BANK OF ZIMBLIA, WOODFORD, ZIMBLIA",
      "LOC_SENDER_TO_RECEIVER_INFORMATION": "THIS CREDIT IS SUBJECT TO UNIFORM CUSTOMS AND PRACTICE FOR DOCUMENTARY CREDIT, 2007 REVISION, INTERNATIONAL CHAMBER OF COMMERCE PUBLICATIONS NO.600."        
    }
}
```
This is what happens:   

### Step 1: Hash computation
The SHA-512 hash of the Letter of Credit is computed.

### Step 2: Signing the Letter of Credit
The hash is signed using the private key of the signer, using the secp256k1 algorithm.

### Step 3: Encrypting the Letter of Credit
The Letter of Credit is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the Letter of Credit
2. the AES password
3. the Initialization Vector (IV). Initialization Vector is a nonce that is associated with an invocation of authenticated encryption on a particular plaintext and Additional Authenticated Data (AAD).   
4. the Authentication Tag (tag), which is a cryptographic checksum on data that is designed to reveal both accidental errors and the intentional modification of the data.

### Step 4: Storing the encrypted Letter of Credit
The encrypted Letter of Credit and the tag are published to the blockchain.

### Step 5: Output 
The following is the output:
1. the relevant Sawtooth transaction id
2. the digital signature
3. the AES password
4. the Initialization Vector (IV)

***Sample output***
```
{
"status": 200,
"response": {
"primechain_sawtooth_tx_id": "82cde773d6b25b9a48dcb16f602fbcd5ed3649183d595e19ed545650bdfcc8fc2a9316121281910f43c52d3ba5c9e2d0c0eb6fce3ece54b6a257462bc6d395c1",
"signature": "cb36670bc1e53389473f1fcac881bf8c30e3a8b44ea34a8adb8608ab7dd7dec850073c9d2e6e868b1a4fe94603a2a3fa3187dfd506edf26fc7173a64e9c4e699",
"aes_password": "gkSQEaVPI9bHwGM37NmtjNBUad7mwoHm",
"aes_iv": "RaaizYEJvqxg"
}
}
```

## 3.5 Retrieving a letter of credit from TRADE-Chain
To retrieve a Letter of Credit from the blockchain, use `post /api/v1/decrypt_download_data_sawtooth` and pass these values:
1. the relevant Sawtooth transaction id 
2. the sawtooth public key of the signer
3. the AES password
4. the Initialization Vector (IV)
5. the digital signature

***Sample input***
```
{
"primechain_sawtooth_tx_id": "82cde773d6b25b9a48dcb16f602fbcd5ed3649183d595e19ed545650bdfcc8fc2a9316121281910f43c52d3ba5c9e2d0c0eb6fce3ece54b6a257462bc6d395c1",

"primechain_sawtooth_public_key": "02b023ef5ce8f6ef4e3419ebc925060ceb3ed9f80c489e34fb93033956581b4941",
"signature": "cb36670bc1e53389473f1fcac881bf8c30e3a8b44ea34a8adb8608ab7dd7dec850073c9d2e6e868b1a4fe94603a2a3fa3187dfd506edf26fc7173a64e9c4e699",
"aes_password": "gkSQEaVPI9bHwGM37NmtjNBUad7mwoHm",
"aes_iv": "RaaizYEJvqxg"
}
```
This is what happens:   

### Step 1: Retrieval of the encrypted Letter of Credit 
The encrypted Letter of Credit and tag are retrieved from the blockchain.

### Step 2: Decryption
The encrypted Letter of Credit is decrypted.

### Step 3: Verification
The digital signature is verified.

### Step 4: Output
The output will be the Letter of Credit if the signature is verified and valid.

***Sample output***
```
{
"status": 200,
"response": {
      "LOC_FORM": "IRREVOCABLE",
      "LOC_NUMBER": "32453675864534",
      "LOC_DATE_OF_ISSUE": "17-DECEMBER-2018",
      "LOC_DATE_OF_EXPIRY": "16-MARCH-2019",
      "LOC_PLACE_OF_EXPIRY": "MUMBAI, INDIA",
      "LOC_APPLICANT_BANK": "GLOBAL BANK, GENEVA, SWITZERLAND",
      "LOC_APPLICANT": "NICOLE CORPORATION",
      "LOC_BENEFICIARY": "KIDMAN INC, ADELAIDE, AUSTRALIA",
      "LOC_CURRENCY": "USD",
      "LOC_AMOUNT_WORDS": "TWO MILLION",
      "LOC_AMOUNT_FIGURES": "2,000,000.00",
      "LOC_MAX_CREDIT_AMOUNT": "NOT EXCEEDING",
      "LOC_AVAILABLE_WITH": "ANY BANK",
      "LOC_AVAILABLE_BY": "BY NEGOTIATION",
      "LOC_DRAFTS_AT": "SIGHT",
      "LOC_DRAWEE": "INTERNATIONAL BANK, NEW YORK, USA",
      "LOC_PARTIAL_SHIPMENTS": "ALLOWED",
      "LOC_TRANSHIPMENT": "NOT ALLOWED",
      "LOC_FOR_TRANSPORTATION_TO": "MUMBAI, INDIA",
      "LOC_LATEST_DATE_OF_SHIPMENT": "17-JANUARY-2018",
      "LOC_DESCRIPTION_GOODS_SERVICES": "PLATINUM RODS",
      "LOC_QUANTITY_GOODS_SERVICES": "2000",
      "LOC_UNIT_PRICE_GOODS_SERVICES": "1000",
      "LOC_TRADE_TERMS": "CIF MUMBAI",
      "LOC_ORDER_NUMBER": "435346453",
      "LOC_DOCUMENTS_REQUIRED": "1.BENEFICIARY'S DRAFT AT SIGHT DRAWN ON BUYER'S BANK NAME, ADDRESS, MARKED "DRAWN UNDER BUYER'S BANK NAME IRREVOCABLE LETTER OF CREDIT NO.XXX DATED XXX". 2. SIGNED COMMERCIAL INVOICE IN TRIPLICATE. 3. PACKING LIST IN TRIPLICATE, INDICATING WEIGHT AND MEASUREMENT. 4. FULL SET (3 ORIGINALS AND 3 COPIES) OF CLEAN ON BOARD BILLS OF LADING MADE OUT TO ORDER OF SHIPPER AND BLANK ENDORSED MARKED "FREIGHT PREPAID" AND NOTIFY APPLICANT. 5. INSURANCE POLICY IN DUPLICATE ENDORSED IN BLANK FOR 110 PERCENT OF THE INVOICE VALUE INCLUDING ALL RISKS, WAR CLAUSES AND S.R.C.C. 6. CERTIFICATE OF ORIGIN IN 3 ORIGINALS AND 2 COPIES ISSUED BY CHAMBER OF COMMERCE.",
      "LOC_ADDITIONAL_CONDITIONS": "THE COMPLETE SET OF ORIGINAL DOCUMENTS TO BE SENT IN ONE LOT BY THE COURIER SERVICE TO APPLIANT BANK.",
      "LOC_CHARGES": "ALL BANKING CHARGES ARE FOR BENEFICIARY'S ACCOUNT.",
      "LOC_PERIOD_FOR_PRESENTATION": "DOCUMENTS MUST BE PRESENTED WITHIN THE VALIDITY OF THIS CREDIT.",
      "LOC_CONFIRMATION_INSTRUCTIONS": "CONFIRM",
      "LOC_ADVISING_THROUGH_BANK": "STATE BANK OF ZIMBLIA, WOODFORD, ZIMBLIA",
      "LOC_SENDER_TO_RECEIVER_INFORMATION": "THIS CREDIT IS SUBJECT TO UNIFORM CUSTOMS AND PRACTICE FOR DOCUMENTARY CREDIT, 2007 REVISION, INTERNATIONAL CHAMBER OF COMMERCE PUBLICATIONS NO.600."   
}
}
```

## 3.6 Publishing unencrypted data to TRADE-Chain
To publish data to the blockchain, use `post /api/v1/upload_data_sawtooth` and pass 2 parameters:
1. Private_key
2. The data
```
{
  "primechain_sawtooth_private_key": "89b0d0a7ef410e9dc19907b8d9297ec2239222c2b38d56056964495b517fe6c1",
  "data": "Mistakes are always forgivable, if one has the courage to admit them."
}
```
Output will be the Sawtooth transaction id for the transaction.
```
{
"status": 200,
"primechain_sawtooth_tx_id": "a31075ee02e17c73b520c3a379880e936a011a702fe412a5e4da0d02300b90623b442e627774671d542565c642d4aa246545faaedaecde16cfa5d979be231e62"
}
```

## 3.7 Retrieving unencrypted data from TRADE-Chain
To retrieve data from the blockchain, use `post /api/v1/get_data_sawtooth` and pass the Sawtooth transaction id of the  transaction.
```
{
"primechain_sawtooth_tx_id": "a31075ee02e17c73b520c3a379880e936a011a702fe412a5e4da0d02300b90623b442e627774671d542565c642d4aa246545faaedaecde16cfa5d979be231e62"
}
```
Output will be the data.
```
{
"status": 200,
"response": "Mistakes are always forgivable, if one has the courage to admit them."
}
```
## 4. Creating a digital signature using TRADE-Chain

To create a digital signature, use `post /api/v1/create_signature_sawtooth` and pass 2 parameters:
1. Private key
2. the data
```
{
  "primechain_sawtooth_private_key": "89b0d0a7ef410e9dc19907b8d9297ec2239222c2b38d56056964495b517fe6c1",
  "data": "Mistakes are always forgivable, if one has the courage to admit them."
}
```
The output will be the digital signature:
```
{
"status": 200,
"signature": "235de04e222dfcfcc0a2cdec32c1a2aaa56b404dc6b0e4e721eef264ce891e1920ff05ee6345635bd017fca97fef2407b57364a287dd27eddc8a82dec61bb87b"
}
```

## 5. Verify a digital signature using TRADE-Chain
To verify a digital signature, use `post /api/v1/verify_signature_sawtooth` and pass 3 parameters:
1. public key
2. the data
3. the digital signature
```
{
  "primechain_sawtooth_public_key": "02b023ef5ce8f6ef4e3419ebc925060ceb3ed9f80c489e34fb93033956581b4941",
  "data": "Mistakes are always forgivable, if one has the courage to admit them.",
  "signature": "235de04e222dfcfcc0a2cdec32c1a2aaa56b404dc6b0e4e721eef264ce891e1920ff05ee6345635bd017fca97fef2407b57364a287dd27eddc8a82dec61bb87b"
}
```
The output will be:
```
{
"status": 200,
"response": true
}
```
or
```
{
"status": 200,
"response": false
}
``` 

Have a query? Email us on info@primechain.in
