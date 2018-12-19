# Employee background verification

“Bad” employees pose a massive threat to employers (companies, Government agencies, organisations). Employers use background checks to make informed placement decisions, retain the most qualified candidates, and mitigate the risk of selecting the wrong candidate. This minimizes workplace violence, fraud, embezzlement, and theft. (Source: National Association of Professional Background Screeners)

Primechain-API enable the creation of a blockchain that allows trusted employers to share employee records in a transparent, secure and confidential manner. 

***Some of the benefits of using blockchain for employee background verification are:***   
1. Each record is digitally signed by the uploading entity.
2. The system is API driven and can easily be integrated with legacy systems.
3. Each record is automatically encrypted and the decryption credentials are only available to the uploading entity. This ensures data privacy.
4. Comprehensive background checks of employees can be done at a fraction of the current background verification cost. 
5. Convert your employee record repository from a cost to a revenue stream. 

### Steps involved

1. [Create, encrypt, sign and publish an employee record to the blockchain](#1-create-encrypt-sign-and-publish-an-employee-record-to-the-blockchain)

2. [Decrypt, verify and retrieve an employee record from the blockchain](#2-decrypt-verify-and-retrieve-an-employee-record-from-the-blockchain)


## 1. Create, encrypt, sign and publish an employee record to the blockchain
To create an employee record on the blockchain, use `post /api/v1/encrypt_sign_store_data` and pass 2 parameters: 
1. the primechain address of the uploading entity
2. the employee record data 

***Sample input***
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "employee_name": "Nicole Kidman",
      "employee_record_type": "Academic record",
      "employee_record_data": "Nicole Kidman has passed the B.E. Electronics and Telecommunications Engineering (Revised) course degree examination held by the University of Mumbai in the month of May 2018 and was placed in the first class.",
    }
}
```

Employee records can be of the following types:
1. Identity related information
2. Academic record
3. Contact information
4. Criminal record
5. Employment history
6. Professional license
7. Reference check

This is what happens:   

### Step 1: Hash computation
The SHA-512 hash of the employee record is computed.

### Step 2: Signing
The hash is signed using the private key of the uploader, using the Elliptic Curve Digital Signature Algorithm (ECDSA) algorithm.

### Step 3: Storing the signature
The following are published to the `DATA_SIGNATURE_MASTERLIST` stream:
1. the digital signature
2. the hash
3. the primechain address of the uploader

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
Save this output in your private database along with the following:

* Employee identifier e.g. PAN number, passport number etc.
* Price (optional)
* Description of the record

## 2. Decrypt, verify and retrieve an employee record from the blockchain
To retrieve an employee record from the blockchain, use `post /api/v1/decrypt_download_data` and pass these values:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the uploader's primechain address were published to the DATA_SIGNATURE_MASTERLIST stream
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
The output will be the employee record, the details of the uploader and the status of the signature (true implies that the signature is verified and valid).

***Sample output***
```
{
  "status": 200,
  "response": 
    {
      "data": 
        {
    {
      "employee_name": "Nicole Kidman",
      "employee_record_type": "Academic record",
      "employee_record_data": "Nicole Kidman has passed the B.E. Electronics and Telecommunications Engineering (Revised) course degree examination held by the University of Mumbai in the month of May 2018 and was placed in the first class.",
    }
        },
       "signer_detail": 
        {
          "name": "Noodle Corporation",
          "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
        },
        "signature_status": true
    }
}
```

Have a query? Email us on info@primechain.in



