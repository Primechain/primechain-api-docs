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
The output will be the data and the details of the signer.
```
aaa
```
