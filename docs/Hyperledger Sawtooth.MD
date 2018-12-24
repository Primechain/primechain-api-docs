# Hyperledger Sawtooth

[1. Create key pair](#1-create-key-pair)      
[2. Publish data to the blockchain](#2-publish-data-to-the-blockchain)     
[3. Retrieve data from the blockchain](#3-retrieve-data-from-the-blockchain)    
[4. Creating a digital signature](#4-creating-a-digital-signature)   
[5. Verify a digital signature](#5-verify-a-digital-signature)   
[6. Create, encrypt, sign and publish data to the blockchain](#6-create-encrypt-sign-and-publish-data-to-the-blockchain)   
[7. Decrypt, verify and retrieve data from the blockchain](#7-decrypt-verify-and-retrieve-data-from-the-blockchain)   

## 1. Create key pair
To create a key pair, use `get /api/v1/create_user_key_sawtooth`
The output will be the 
1. Private_key
2. Public key
```
{
"status": 200,
"primechain_sawtooth_private_key": "89b0d0a7ef410e9dc19907b8d9297ec2239222c2b38d56056964495b517fe6c1",
"primechain_sawtooth_public_key": "02b023ef5ce8f6ef4e3419ebc925060ceb3ed9f80c489e34fb93033956581b4941",
"response": "User keys generated"
}
```

## 2. Publish data to the blockchain
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

## 3. Retrieve data from the blockchain
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
## 4. Creating a digital signature

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

## 5. Verify a digital signature
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

## 6. Create, encrypt, sign and publish data to the blockchain
To create, encrypt, sign and publish data to the blockchain, use `post /api/v1/encrypt_sign_store_data_sawtooth` and pass 2 parameters: 
1. the primechain sawtooth private key 
2. the data 

***Sample input***
```
{
  "primechain_sawtooth_private_key": "89b0d0a7ef410e9dc19907b8d9297ec2239222c2b38d56056964495b517fe6c1",
  "data": 
    {
      "guarantee_number": "ASDRE76464",
      "guarantee_currency": "USD",
      "guarantee_amount_words": "Twenty Two million",
      "guarantee_amount_figures": "22,000,000.00",
      "guarantee_date_of_issue": "17-December-2018",
      "guarantee_date_of_maturity": "16-March-2019",
      "guarantee_beneficiary": "Nicole Corporation",
      "guarantee_details": "On behalf of our client, Nicole Corporation, for value received, we, Global Bank, hereby irrevocably and unconditionally and without protest or notification, promise to pay against this, our irrevocable bank guarantee, to the order of Nicole Corporation, as beneficiary, on the maturity date, the sum of Twenty Two million United States Dollars ($22,000,000.00 USD), upon their first written demand for payment hereunder. Such payment shall be made without set-off, free and clear of any deductions, charges, fees, levies, taxes or withholdings of any nature. This bank guarantee is transferable, without payment of any transfer fees. This bank guarantee is issued in accordance with the uniform customs and practices for bank guarantees, as set forth by the International Chamber of Commerce, Paris, France, latest revision of ICC 500 publication. This bank guarantee shall be governed by and construed in accordance with the laws of the Republic of India and is free and clear of any lien and encumbrances and is of non-criminal origin.",
      "authorized_bank_officer_name": "Nicole Kidman",
      "authorized_bank_officer_title": "Vice President",
      "authorized_bank_officer_telephone": "230950934545",
      "authorized_bank_officer_facsimile": "367645455624",
      "authorized_bank_officer_email": "nicole@example.com"      
    }
}
```
This is what happens:   

### Step 1: Hash computation
The SHA-512 hash of the data is computed.

### Step 2: Signing
The hash is signed using the private key of the signer, using the secp256k1 algorithm.

### Step 3: Encrypting the data
The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the data
2. the AES password
3. the Initialization Vector (IV). Initialization Vector is a nonce that is associated with an invocation of authenticated encryption on a particular plaintext and Additional Authenticated Data (AAD).   
4. the Authentication Tag (tag), which is a cryptographic checksum on data that is designed to reveal both accidental errors and the intentional modification of the data.

### Step 4: Storing the encrypted data
The encrypted data and the tag are published to the blockchain.

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

## 7. Decrypt, verify and retrieve data from the blockchain
To retrieve data from the blockchain, use `post /api/v1/decrypt_download_data_sawtooth` and pass these values:
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

### Step 1: Retrieval of encrypted data 
The encrypted data and tag are retrieved from the blockchain.

### Step 2: Decryption
The encrypted data is decrypted.

### Step 3: Verification
The digital signature is verified.

### Step 4: Output
The output will be the data if the signature is verified and valid.

***Sample output***
```
{
"status": 200,
"response": {
"guarantee_number": "ASDRE76464",
"guarantee_currency": "USD",
"guarantee_amount_words": "Twenty Two million",
"guarantee_amount_figures": "22,000,000.00",
"guarantee_date_of_issue": "17-December-2018",
"guarantee_date_of_maturity": "16-March-2019",
"guarantee_beneficiary": "Nicole Corporation",
"guarantee_details": "On behalf of our client, Nicole Corporation, for value received, we, Global Bank, hereby irrevocably and unconditionally and without protest or notification, promise to pay against this, our irrevocable bank guarantee, to the order of Nicole Corporation, as beneficiary, on the maturity date, the sum of Twenty Two million United States Dollars ($22,000,000.00 USD), upon their first written demand for payment hereunder. Such payment shall be made without set-off, free and clear of any deductions, charges, fees, levies, taxes or withholdings of any nature. This bank guarantee is transferable, without payment of any transfer fees. This bank guarantee is issued in accordance with the uniform customs and practices for bank guarantees, as set forth by the International Chamber of Commerce, Paris, France, latest revision of ICC 500 publication. This bank guarantee shall be governed by and construed in accordance with the laws of the Republic of India and is free and clear of any lien and encumbrances and is of non-criminal origin.",
"authorized_bank_officer_name": "Nicole Kidman",
"authorized_bank_officer_title": "Vice President",
"authorized_bank_officer_telephone": "230950934545",
"authorized_bank_officer_facsimile": "367645455624",
"authorized_bank_officer_email": "nicole@example.com"
}
}
```

Have a query? Email us on info@primechain.in
