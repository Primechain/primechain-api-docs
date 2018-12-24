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
  "primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
The output will be the digital signature:
```
{
"status": 200,
"signature": "65a985418249c2f8c20d3a8f42b5398fbd7c7a75c31eb11038efa721505f24dc4d8eff7d6151562a464daeb34f3dcf8323191aae25997f2e5ce52ca46c6186f9"
}
```

## 5. Verify a digital signature
To create a digital signature, use `post /api/v1/verify_signature_sawtooth` and pass 2 parameters:
1. public key
2. the data
3. the digital signature
```
{
  "primechain_sawtooth_public_key": "022dfb9755cf6a7313ddc58aa22894436d0e4c49e4c52f4706b554ef2dc56fc7de",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times.",
  "signature": "65a985418249c2f8c20d3a8f42b5398fbd7c7a75c31eb11038efa721505f24dc4d8eff7d6151562a464daeb34f3dcf8323191aae25997f2e5ce52ca46c6186f9"
}
```
The output will be:
```
{
"status": 200,
"response": true
}
```
## 6. Create, encrypt, sign and publish data to the blockchain
To create, encrypt, sign and publish data to the blockchain, use `post /api/v1/encrypt_sign_store_data_sawtooth` and pass 2 parameters: 
1. the primechain sawtooth private key 
2. the data 

***Sample input***
```
{
  "primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
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
1. the sawtooth address where the data is published
2. the digital signature
3. the AES password
4. the Initialization Vector (IV)

***Sample output***
```
{
"status": 200,
"response": {
"sawtooth_address": "97fd77ad086befd425f5bf34a93f393593849eaf4edd3cba568f7385633db76d29e891",
"signature": "fd61ee928d36d5b8762831a985b1b49574a2b155e099d92307494fb11d32968622f03986370243d9f33702573a5afe02798c893007f1d9f4c2a21657e7e55226",
"aes_password": "3P83TKUsek9vh9EAsqJx1uAh14xWk3LA",
"aes_iv": "NukszFAnCE09"
}
}
```



## 7. Decrypt, verify and retrieve data from the blockchain
To retrieve data from the blockchain, use `post /api/v1/decrypt_download_data_sawtooth` and pass these values:
1. the sawtooth address where the data is published
2. the sawtooth public key of the signer
3. the AES password
4. the Initialization Vector (IV)
5. the digital signature

***Sample input***
```
{
"sawtooth_address": "97fd77ad086befd425f5bf34a93f393593849eaf4edd3cba568f7385633db76d29e891",
"primechain_sawtooth_public_key": "022dfb9755cf6a7313ddc58aa22894436d0e4c49e4c52f4706b554ef2dc56fc7de",
"signature": "fd61ee928d36d5b8762831a985b1b49574a2b155e099d92307494fb11d32968622f03986370243d9f33702573a5afe02798c893007f1d9f4c2a21657e7e55226",
"aes_password": "3P83TKUsek9vh9EAsqJx1uAh14xWk3LA",
"aes_iv": "NukszFAnCE09"
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
The output will be the data, the details of the signer and the status of the signature (true implies that the signature is verified and valid).

***Sample output***
```

}
```

Have a query? Email us on info@primechain.in
