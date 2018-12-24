# Charge Registry

Corporates leverage their immovable, movable and intangible assets to raise debt. This creates charges such as hypothecation, lien, mortgage, and pledge. Blockchain based charge registry enables the sharing of charge related information to prevent fraud and increase speed of due-diligence. 

Categories of charge related records:
1. Bank financing arrangements
2. Guaranties to which the entity is a party
3. Hypothecation related records
4. Lien related records
5. Line of credit
6. Loan agreements
7. Loan Sanction Documents
8. Mortgage related records
9. Other charge related documents
10. Pledge related records
11. Promissory notes

### Steps involved

1. [Create, encrypt, sign and publish a charge related record to the blockchain](#1-create,-encrypt,-sign-and-publish-a-charge-related-record-to-the-blockchain)

2. [Decrypt, verify and retrieve a charge related record from the blockchain](#2-decrypt,-verify-and-retrieve-a-charge-related-record-from-the-blockchain)


## 1. Create, encrypt, sign and publish a charge related record to the blockchain
To create a charge record on the blockchain, use `post /api/v1/encrypt_sign_store_data` and pass 2 parameters: 
1. the primechain address of the bank issuing the charge record
2. the charge record data 

***Sample input***
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "charge_type": "Unsecured Promissory Note",
      "charge_number": "ASDRE76464",
      "charge_details": "Nicole Corporation agrees and promises to pay to Global Bank the sum of USD Two million for value received, with interest at the annual rate of 8% payable after 16-March-2019. If this note is in default and is placed for collection, Nicole Corporation shall pay all reasonable costs of collection and attorneys' fees."    
    }
}
```
This is what happens:   

### Step 1: Hash computation
The SHA-512 hash of the charge record is computed.

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
"response": {
"tx_id_enc_data": "1fd54d87692565fa918ba69a584cf2d1c09f467f72b2a7abc5e039dfed387496",
"tx_id_signature": "263ac44e6a6afb62da72cc8308b0937f39992b0069da4a6a3e4b25f3bfef7c5c",
"signature": "HzP/I+1Y4ToeeMDeAGOjwc62y2rRspei8os7fiMzuAMYJ00cxXYLPLb+XYP9Ju+A+7Di9QLZKN/na/2qUAGZvgo=",
"aes_password": "12wVwwDIK4pzZtxyJ8N4NBwCxumEMd26",
"aes_iv": "0MSe10jJ8sUc"
}
}
```

## 2. Decrypt, verify and retrieve a charge related record from the blockchain
To retrieve a charge record from the blockchain, use `post /api/v1/decrypt_download_data` and pass these values:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the issuers's primechain address were published to the DATA_SIGNATURE_MASTERLIST stream
3. the AES password
4. the Initialization Vector (IV)

***Sample input***
```
{
  "tx_id_enc_data": "1fd54d87692565fa918ba69a584cf2d1c09f467f72b2a7abc5e039dfed387496",
  "tx_id_signature": "263ac44e6a6afb62da72cc8308b0937f39992b0069da4a6a3e4b25f3bfef7c5c",
  "aes_password": "12wVwwDIK4pzZtxyJ8N4NBwCxumEMd26",
  "aes_iv": "0MSe10jJ8sUc"
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
The output will be the charge record, the details of the signer and the status of the signature (true implies that the signature is verified and valid).

***Sample output***
```
{
"status": 200,
"response": {
"data": {
"charge_type": "Unsecured Promissory Note",
"charge_number": "ASDRE76464",
"charge_details": "Nicole Corporation agrees and promises to pay to Global Bank the sum of USD Two million for value received, with interest at the annual rate of 8% payable after 16-March-2019. If this note is in default and is placed for collection, Nicole Corporation shall pay all reasonable costs of collection and attorneys' fees."
},
"signer_detail": {
"name": "Noodle Bank Official Signer",
"primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
},
"signature_status": true
}
}
```

Have a query? Email us on info@primechain.in
