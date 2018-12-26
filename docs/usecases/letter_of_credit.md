# Letter of credit

![Letter of credit](http://www.primechaintech.com/img/api_documentation/letter_of_credit.jpg)

A letter of credit is like a promissory note that represents an obligation taken on by a bank to make a payment once certain criteria are met - once the terms are completed and confirmed, the bank will transfer the funds. Simply put, a letter of credit ensures that the payment will be made as long as the services are performed.

Example: An Indian exporter receives an order from an American importer. The exporter is not sure about the importer’s ability and willingness to pay once the order is delivered. The exporter requests for a letter of credit from the importer. The importer then applies for a letter of credit from its bank (where it has adequate funds or credit line. Once the goods are shipped, the bank pays the exporter subject to fulfilment of relevant terms and conditions. 

Letters of credit are especially important in international trade due to the distance involved and potentially differing laws in the countries of the businesses involved. In these transactions, it is not always possible for the parties to meet in person. The bank issuing the letter of credit holds payment on behalf of the buyer until it receives confirmation that the goods in the transaction have been shipped. (Source: Investopedia)


***Some of the benefits of using blockchain for letters of credit are:***

1. A conventional Letter of Credit transaction involves time consuming manual processes such as the transfer of physical copies by post, courier, fax or scans. The use of blockchain offers significant potential to reduce the timelines involved in exchange of export documentation from the extant 7 to 10 days to less than a day. (Source: shippingandfreightresource.com)

2. Use of blockchain in trade finance enhances transparency, security and synergy across all the parties and stakeholders involved. 

3. Blockchain brings efficiency to trade finance and ensures cost effectiveness, quicker turnaround and unlocks liquidity for businesses.

4. Blockchain technology usage for trade finance “enables automation of LC creation, payment against documents...” (Source: Reserve Bank of India’s 2017 Report of the Working Group on FinTech and Digital Banking).

5. Blockchain will have a transformative impact on trade finance transactions, enable greater transparency, and offer simpler and faster transactions. (Source: morethanshipping.com)

(2) Regulator nodes enable real-time supervision by the authorities.
(3) The system is API driven and can easily be integrated with the banks' core banking and other legacy systems.
(4) Each LoC is automatically encrypted and the decryption credentials are only available to the issuing bank.

### Steps involved

1. [Create, encrypt, sign and publish a letter of credit to the blockchain](#1-create-encrypt-sign-and-publish-a-letter-of-credit-to-the-blockchain)

2. [Decrypt, verify and retrieve a letter of credit from the blockchain](#2-decrypt-verify-and-retrieve-a-letter-of-credit-from-the-blockchain)


## 1. Create, encrypt, sign and publish a letter of credit to the blockchain
To create a letter of credit on the blockchain, use `post /api/v1/encrypt_sign_store_data` and pass 2 parameters: 
1. the primechain address of the bank issuing the letter of credit
2. the letter of credit data 

***Sample input***
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
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
This is what happens:   

### Step 1: Hash computation
The SHA-512 hash of the letter of credit is computed.

### Step 2: Signing
The hash is signed using the private key of the issuing bank, using the Elliptic Curve Digital Signature Algorithm (ECDSA) algorithm.

### Step 3: Storing the signature
The following are published to the `DATA_SIGNATURE_MASTERLIST` stream:
1. the digital signature
2. the hash
3. the primechain address of the issuing bank 

### Step 4: Encrypting the data
The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the data
2. the AES password
3. the Initialization Vector (IV). Initialization Vector is a nonce that is associated with an invocation of authenticated encryption on a particular plaintext and Additional Authenticated Data (AAD).   
4. the Authentication Tag (tag), which is a cryptographic checksum on data that is designed to reveal both accidental errors and the intentional modification of the data.

### Step 5: Storing the encrypted data
The encrypted data and the tag are published to the `DATA_MASTERLIST` stream.

### Step 6: Output 
The following is the output:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the issuer's primechain address were published to the DATA_SIGNATURE_MASTERLIST stream
3. the digital signature
3. the AES password
4. the Initialization Vector (IV)

***Sample output***
```
{
"status": 200,
"response": 
  {
    "tx_id_enc_data": "a8441a8e8fe52c6f84941fd1f08f774ecbf0dc9edf9fd18e9f9d20f1d2945940",
    "tx_id_signature": "8f15a1b3bc4cbeeae89ea28e77982ac7baa04c45870d9d40086b799ad795487f",
    "signature": "H523zhPwR1gdPn2R0/JlfTJLWB5HaII96vJcDx4qy8f2StF1AE6Qfft8lqE2IoDd2czj5cW8i9ZJLaWXu7KkEyE=",
    "aes_password": "5M1qnsYeRmSvlwNtZ8oJiHC0g9ucVrgc",
    "aes_iv": "zNc59qnYapAw"
  }
}
```

## 2. Decrypt, verify and retrieve a letter of credit from the blockchain
To retrieve a letter of credit from the blockchain, use `post /api/v1/decrypt_download_data` and pass these values:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the issuers's primechain address were published to the DATA_SIGNATURE_MASTERLIST stream
3. the AES password
4. the Initialization Vector (IV)

***Sample input***
```
{
    "tx_id_enc_data": "b40cb6e4b95e72510413cd20030c3ea7052ef1dea8deb9340efb5e39d05f8394",
    "tx_id_signature": "3f06f98af6b7acbb9b7ec26f7c692bf39b999fc645cce5f969ca5467470fc235",
    "aes_password": "R1E3GYxjAc0Gfa8xEqRNtOdJfWErOBz7",
    "aes_iv": "VioxHPgIDj7F"
}
```
This is what happens:   

### Step 1: Retrieval of signing data 
The digital signature, hash and the primechain address of the issuing bank are retrieved from the DATA_SIGNATURE_MASTERLIST stream.

### Step 2: Retrieval of encrypted data 
The encrypted data and tag are retrieved from the DATA_MASTERLIST stream.

### Step 3: Decryption
The encrypted data is decrypted.

### Step 4: Verification
The digital signature is verified.

### Step 5: Output
The output will be the letter of credit, the details of the signer and the status of the signature (true implies that the signature is verified and valid).

***Sample output***
```
{
  "status": 200,
  "response": 
    {
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
      "LOC_DOCUMENTS_REQUIRED": "1.BENEFICIARY'S DRAFT AT SIGHT DRAWN ON BUYER'S BANK NAME, ADDRESS, MARKED "DRAWN UNDER BUYER'S BANK NAME IRREVOCABLE LETTER OF CREDIT NO.XXX DATED XXX". 2. SIGNED COMMERCIAL INVOICE IN TRIPLICATE. 3. PACKING LIST IN TRIPLICATE, INDICATING WEIGHT AND MEASUREMENT. 4. FULL SET (3 ORIGINALS AND 3 COPIES) OF CLEAN ON BOARD BILLS OF LADING MADE OUT TO ORDER OF SHIPPER AND BLANK ENDORSED MARKED "FREIGHT PREPAID" AND NOTIFY APPLICANT. 5. INSURANCE POLICY IN DUPLICATE ENDORSED IN BLANK FOR 110 PERCENT OF THE INVOICE VALUE INCLUDING ALL RISKS, WAR CLAUSES AND S.R.C.C. 6. CERTIFICATE OF ORIGIN IN 3 ORIGINALS AND 2 COPIES ISSUED BY CHAMBER OF COMMERCE.",
      "LOC_ADDITIONAL_CONDITIONS": "THE COMPLETE SET OF ORIGINAL DOCUMENTS TO BE SENT IN ONE LOT BY THE COURIER SERVICE TO APPLIANT BANK.",
      "LOC_CHARGES": "ALL BANKING CHARGES ARE FOR BENEFICIARY'S ACCOUNT.",
      "LOC_PERIOD_FOR_PRESENTATION": "DOCUMENTS MUST BE PRESENTED WITHIN THE VALIDITY OF THIS CREDIT.",
      "LOC_CONFIRMATION_INSTRUCTIONS": "CONFIRM",
      "LOC_ADVISING_THROUGH_BANK": "STATE BANK OF ZIMBLIA, WOODFORD, ZIMBLIA",
      "LOC_SENDER_TO_RECEIVER_INFORMATION": "THIS CREDIT IS SUBJECT TO UNIFORM CUSTOMS AND PRACTICE FOR DOCUMENTARY CREDIT, 2007 REVISION, INTERNATIONAL CHAMBER OF COMMERCE PUBLICATIONS NO.600."   
   
        },
       "signer_detail": 
        {
          "name": "Noodle Bank Official Signer",
          "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
        },
        "signature_status": true
    }
}
```

Have a query? Email us on info@primechain.in


