# Encrypted data storage

1. [Encrypt, sign and upload data](#1-encrypt-sign-and-upload-data)
2. [Decrypt and download data](#2-decrypt-and-download-data)
3. [Encrypt, sign and upload file](#3-encrypt-sign-and-upload-file)
4. [Decrypt and download file](#4-decrypt-and-download-file)

## 1. Encrypt, sign and upload data
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_data` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
  {
  "primechain_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "data": 
    {
      "type": "GUARANTEE",
      "40A": "IRREVOCABLE",
      "20": ":DOC.500",
      "31C": "181106 INDIA",
      "31D": "181206 DUBAI",
       "50": "IMPORTER COMPANY NAME, IMPORTER COMPANY ADDRESS, INDIA",
       "59": "EXPORTER COMPANY NAME, EXPORTER COMPANY ADDRESS, DUBAI"
    }
  }
}
```
The output contains:
1. The transaction id of the transaction in which the dats was stored on the blockchain
2. The digital signature
3. The AES decryption key data - password and iv
```
{
"status": 200,
"response": 
  {
    "transaction_id": "27ed040aa02b6fe6f8635bacaa3ad8f85c49d9bfdc9a1cb37fc33e5db900c228",
    "signature": "IMgAru76ErWwYHq1qFhUne1AnfQIU9a0WrAWgw4LiH4zcsT8tvnINzg15E5DgjdGbij4u7jxyCHBXoDKhU/2JPk=",
    "password": "kGhMFsTYQ7HwfWxLUKGXh37zwPF7yRJC",
    "iv": "nPKF0E6icGKs"
  }
}
```

## 2. Decrypt and download data
To decrypt and download a file, use `post /api/v1/decrypt_download_data` and pass these values:
* The blockchain address using which the file was signed
* The transaction id of the transaction in which the dats was stored on the blockchain
* The AES decryption key data - password and iv
```
{
  "txid": "27ed040aa02b6fe6f8635bacaa3ad8f85c49d9bfdc9a1cb37fc33e5db900c228",
  "password": "kGhMFsTYQ7HwfWxLUKGXh37zwPF7yRJC",
  "iv":"nPKF0E6icGKs"
}
```
The output will be the data.
```
{
"status": 200,
"response": 
  {
    20: ":DOC.500",
    50: "IMPORTER COMPANY NAME, IMPORTER COMPANY ADDRESS, INDIA",
    59: "EXPORTER COMPANY NAME, EXPORTER COMPANY ADDRESS, DUBAI",
    "type": "GUARANTEE",
    "40A": "IRREVOCABLE",
    "31C": "181106 INDIA",
    "31D": "181206 DUBAI"
  }
}
```

## 3. Encrypt, sign and upload file
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_file` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
  "primechain_address":"17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "file":"<your file>"
}
```
The output contains:
1. The transaction id of the transaction in which the dats was stored on the blockchain
2. The digital signature
3. The AES decryption key data - password and iv
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
* The blockchain address using which the file was signed
* The transaction id of the transaction in which the dats was stored on the blockchain
* The AES decryption key data - password and iv
```

```
The file will get downloaded.
