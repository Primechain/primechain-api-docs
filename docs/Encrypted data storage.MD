# Encrypted data storage

1. [Sign, encrypt and store data in the blockchain](#1-sign-encrypt-and-store-data-in-the-blockchain)

2. [Decrypt and download data](#2-decrypt-and-download-data)

3. [Encrypt, sign and upload file](#3-encrypt-sign-and-upload-file)

4. [Decrypt and download file](#4-decrypt-and-download-file)

# 1. Sign, encrypt and store data in the blockchain
To encrypt data and store the encrypted data in the blockchain, use `post /api/v1/encrypt_sign_store_data` and pass 2 parameters: 
1. the data 
2. the primechain address of the signing entity

```
{
  "primechain_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "data": 
    {
      "name": "Scarlett Johansson",
      "email": "scarlett@example.com",
      "cell": ":1234567890"
    }
}
```

This is what happens:   

## Step 1: Hash computation

The SHA-512 hash of the data is computed.

## Step 2: Signing
The hash is signed using the private key of the signing entity (using ECDSA).

## Step 3: Storing the signature
The following are published to the `DATA_SIGNATURE_MASTERLIST` stream:
1. the digital signature
2. the hash
3. the primechain address of the signing entity

## Step 4: Encrypting the data
The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the data
2. the AES password
3. the Initialization Vector (IV), which is a nonce that is associated with an invocation of authenticated encryption on a particular plaintext and Additional Authenticated Data.   
4. the Authentication Tag (tag), which is the cryptographic checksum on data that is designed to reveal both accidental errors and the intentional modification of the data. 

## Step 5: Storing the encrypted data
The encrypted data and the tag are published to the `DATA_MASTERLIST` stream

## Step 6: Output 
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
    "tx_id": "27ed040aa02b6fe6f8635bacaa3ad8f85c49d9bfdc9a1cb37fc33e5db900c228",
    "signature": "IMgAru76ErWwYHq1qFhUne1AnfQIU9a0WrAWgw4LiH4zcsT8tvnINzg15E5DgjdGbij4u7jxyCHBXoDKhU/2JPk=",
    "password": "kGhMFsTYQ7HwfWxLUKGXh37zwPF7yRJC",
    "iv": "nPKF0E6icGKs"
  }
}
```

## 2. Decrypt and download data
To retrieve data from the blockchain and decrypt it, use `post /api/v1/decrypt_download_data` and pass these values:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the DATA_SIGNSTURE_MASTERLIST stream
3. The AES password
4. The Initialization Vector (IV)

```
{
  "txid": "27ed040aa02b6fe6f8635bacaa3ad8f85c49d9bfdc9a1cb37fc33e5db900c228",
  "password": "kGhMFsTYQ7HwfWxLUKGXh37zwPF7yRJC",
  "iv":"nPKF0E6icGKs"
}
```
This is what happens:   

## Step 1: Retrieval of signing data 
The digital signature, hash and the primechain address of the signing entity are retrieved from the DATA_SIGNSTURE_MASTERLIST stream.

## Step 2: Retrieval of encrypted data 
The encrypted data and tag are retrieved from the DATA_MASTERLIST stream.

## Step 3: Decryption
3. The encrypted data is decrypted.

## Step 4: Verification
4. The digital signature is verified

## Step 5: Output
The output will be the data and the details of the signer.
```
{
  "primechain_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "data": 
    {
      "name": "Scarlett Johansson",
      "email": "scarlett@example.com",
      "cell": ":1234567890"
    }
}
```

## 3. Encrypt, sign and upload file
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_file` and pass the blockchain address (using which the file will be signed) and the file.
```
{
  "primechain_address":"17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "file":"<your file>"
}
```
The output contains:
1. The transaction id of the transaction in which the data was stored on the blockchain
2. The digital signature
3. The AES password
4. The AES initializaion vector (iv)
```
{
    "status": 200,
    "response": {
        "transaction_id": "8c4419f7e808800b83ec6ac9090813dbeec59c2deb837993a47089ce45acf6b8",
        "signature": "IJFvhJtyv03/kUICkceq4orcAFPzMJKmfuK80pSesdRxXPPF/SQnR234P5I8kY/GslH4bRgFE9mwkm5HhCPTfZk=",
        "password": "pK4mTkZ5Mb6YRlwFmkUnpOO4DA8oY6JV",
        "iv": "T24LZEuWHyrz"
    }
}
```

## 4. Decrypt and download file
To decrypt and download a file, use `post /api/v1/decrypt_download_file` and pass these values:   
1 The transaction id of the transaction in which the file was stored on the blockchain   
2. The AES password   
3. The AES initializaion vector (iv)   
```
{
  "txid":"8c4419f7e808800b83ec6ac9090813dbeec59c2deb837993a47089ce45acf6b8",
  "password":"pK4mTkZ5Mb6YRlwFmkUnpOO4DA8oY6JV",
   "iv":"T24LZEuWHyrz"
}
```
The file will get downloaded.
