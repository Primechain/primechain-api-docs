# Encrypted data storage

1. [Introduction](#1-introduction)
2. [Sign, encrypt and store data in the blockchain](#2-sign-encrypt-and-store-data-in-the-blockchain)
3. [Decrypt, verify and retrieve data from the blockchain](#3-decrypt-verify-and-retrieve-data-from-the-blockchain)
4. [Sign, encrypt and store a file in the blockchain](#4-sign-encrypt-and-store-a-file-in-the-blockchain)
5. [Decrypt, verify and retrieve a file from the blockchain](#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)


# 1. Introduction

For an overview of the digital / electronic signature process, see [this](https://github.com/Primechain/primechain-api-docs/blob/master/docs/The%20electronic%20signature%20process.MD).

Glossary of terms
* AAD: Additional Authenticated Data 
* AES: Advanced Encryption Standard.
* Authentication Tag (Tag): A cryptographic checksum on data that is designed to reveal both accidental errors and the intentional modification of the data. 
* GCM: Galois/Counter Mode
* Initialization Vector: A nonce that is associated with an invocation of authenticated encryption on a particular plaintext and AAD.   

For more information, see [NIST Special Publication 800-38D](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-38d.pdf)


# 2. Sign, encrypt and store data in the blockchain
To encrypt data and store the encrypted data in the blockchain, use `post /api/v1/encrypt_sign_store_data` and pass 2 parameters: 
1. the data 
2. the primechain address of the signing entity

Sample input 1
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "name": "Scarlett Johansson",
      "email": "scarlett@example.com",
      "cell": ":1234567890"
    }
}
```
Sample input 2
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

The SHA-512 hash of the data is computed.

### Step 2: Signing
The hash is signed using the private key of the signing entity (using ECDSA).

### Step 3: Storing the signature
The following are published to the `DATA_SIGNATURE_MASTERLIST` stream:
1. the digital signature
2. the hash
3. the primechain address of the signing entity

### Step 4: Encrypting the data
The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the data
2. the AES password
3. the Initialization Vector (IV)   
4. the Authentication Tag (tag)

### Step 5: Storing the encrypted data
The encrypted data and the tag are published to the `DATA_MASTERLIST` stream

### Step 6: Output 
The following is the output:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the DATA_SIGNSTURE_MASTERLIST stream
3. The AES password
4. The Initialization Vector (IV)

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

## 3. Decrypt, verify and retrieve data from the blockchain
To retrieve data from the blockchain and decrypt it, use `post /api/v1/decrypt_download_data` and pass these values:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the DATA_SIGNSTURE_MASTERLIST stream
3. The AES password
4. The Initialization Vector (IV)

```
{
    "tx_id_enc_data": "a8441a8e8fe52c6f84941fd1f08f774ecbf0dc9edf9fd18e9f9d20f1d2945940",
    "tx_id_signature": "8f15a1b3bc4cbeeae89ea28e77982ac7baa04c45870d9d40086b799ad795487f",
    "aes_password": "5M1qnsYeRmSvlwNtZ8oJiHC0g9ucVrgc",
    "aes_iv": "zNc59qnYapAw"
 }
```
This is what happens:   

### Step 1: Retrieval of signing data 
The digital signature, hash and the primechain address of the signing entity are retrieved from the DATA_SIGNSTURE_MASTERLIST stream.

### Step 2: Retrieval of encrypted data 
The encrypted data and tag are retrieved from the DATA_MASTERLIST stream.

### Step 3: Decryption
The encrypted data is decrypted.

### Step 4: Verification
The digital signature is verified

### Step 5: Output
The output will be the data and the details of the signer.
```
{
"status": 200,
"response": 
  {
    "data": 
      {
        "name": "Scarlett Johansson",
        "email": "scarlett@example.com",
        "cell": ":1234567890"
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

## 4. Sign, encrypt and store a file in the blockchain

To encrypt a file and store the encrypted file in the blockchain, use `post /api/v1/encrypt_sign_store_file` and pass 2 parameters: 
1. the data 
2. the primechain address of the signing entity

```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "file":"<your file>"
}
```

This is what happens:   

### Step 1: Hash computation

The SHA-512 hash of the file is computed.

### Step 2: Signing
The hash is signed using the private key of the signing entity (using ECDSA).

### Step 3: Storing the signature
The following are published to the `FILE_SIGNATURE_MASTERLIST` stream:
1. the digital signature
2. the hash
3. the primechain address of the signing entity

### Step 4: Encrypting the file
The file is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the file
2. the AES password
3. the Initialization Vector (IV)   
4. the Authentication Tag (tag)

### Step 5: Storing the encrypted file
The encrypted file and the tag are published to the `FILE_MASTERLIST` stream

### Step 6: Output 
The following is the output:
1. the id of the transaction in which the encrypted file and tag were published to the FILE_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the FILE_SIGNATURE_MASTERLIST stream
3. The AES password
4. The Initialization Vector (IV)

```
{
"status": 200,
"response": 
  {
    "tx_id_enc_file":"a8441a8e8fe52c6f84941fd1f08f774ecbf0dc9edf9fd18e9f9d20f1d2945940".
    "tx_id_signature": "8f15a1b3bc4cbeeae89ea28e77982ac7baa04c45870d9d40086b799ad795487f",
    "signature": "H523zhPwR1gdPn2R0/JlfTJLWB5HaII96vJcDx4qy8f2StF1AE6Qfft8lqE2IoDd2czj5cW8i9ZJLaWXu7KkEyE=",
    "aes_password": "5M1qnsYeRmSvlwNtZ8oJiHC0g9ucVrgc",
    "aes_iv": "zNc59qnYapAw"
  }
}
```

## 5. Decrypt, verify and retrieve a file from the blockchain
To retrieve a file from the blockchain and decrypt it, use `post /api/v1/decrypt_download_file` and pass these values:
1. the id of the transaction in which the encrypted file and tag were published to the FILE_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the FILE_SIGNATURE_MASTERLIST stream
3. The AES password
4. The Initialization Vector (IV)

```
{
    "tx_id_enc_file": "a8441a8e8fe52c6f84941fd1f08f774ecbf0dc9edf9fd18e9f9d20f1d2945940",
    "tx_id_signature": "8f15a1b3bc4cbeeae89ea28e77982ac7baa04c45870d9d40086b799ad795487f",
    "aes_password": "5M1qnsYeRmSvlwNtZ8oJiHC0g9ucVrgc",
    "aes_iv": "zNc59qnYapAw"
 }
```
This is what happens:   

### Step 1: Retrieval of signing data 
The digital signature, hash and the primechain address of the signing entity are retrieved from the FILE_SIGNATURE_MASTERLIST stream.

### Step 2: Retrieval of encrypted file 
The encrypted file and tag are retrieved from the FILE_MASTERLIST stream.

### Step 3: Decryption
The encrypted file is decrypted.

### Step 4: Verification
The digital signature is verified

### Step 5: Output
The output will be the file and the details of the signer.
```
aaa
```
