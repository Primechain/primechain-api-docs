# Corporate & Individual KYC and due-diligence

1. [Upload KYC data](#1-upload-kyc-data)
2. [Download KYC data](#2-download-kyc-data)
3. [Upload KYC file](#3-upload-kyc-file)
4. [Download KYC file](#4-download-kyc-file)

# 1. Upload KYC data

To upload KYC data, use `post /api/v1/encrypt_sign_store_data` and pass the following parameters:   
1. Your primechain address. The primechain private key coressponding to this address will be used to sign the data. Note: The address must have write permissions to DATA_MASTERLIST and DATA_SIGNATURE_MASTERLIST granted by the seed node.

2. The KYC data. The recommended KYC codes for individuals and for corporates are stored in the `CODE_MASTERLIST` stream.


For example:
```
{
  "primechain_address": "126c5fHTWm54Td6dy22mJVguEsRz4fkfoag1fQ",
  "data": 
  {
    "data_category": "KYC",
    "entity_category": "INDIVIDUAL",
    "name": "Gopal Kumar Santoshi",
    "name_father": "Ram Kumar Santoshi",
    "name_wife": "Ekta Santoshi",
    "email": "gopal@example.com",
    "mobile": "+91-1234567890",
    "address": "213, Zimblia Avenue, Zimblia, IN",
    "gender": "male",
    "dob": "06-NOV-1973",
    "driving_license": "0987654321 dated 11-JAN-2010 issued by RTO, Zimblia",
    "passport": "6554345678 dated 18-MAR-2010 issued by PPO, Zimblia"
  }
}
```
The output contains:
1. The transaction id of the transaction in which the encryted data was stored on the blockchain
2. The digital signature 
3. The 32 character AES password
4. The 12 character AES initializaion vector (iv)
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
Save this output along with the following:
* Customers identifier e.g. PAN, account number
* Price (optional)

***Note:***
* The encrypted KYC data is stored in the DATA_MASTERLIST stream.   
* Your primechain address, the data hash and the digital signature are stored in the DATA_SIGNATURE_MASTERLIST stream.

## 2. Download KYC data
To download data, use `post /api/v1/decrypt_download_data` and pass these parameters:
* The transaction id of the transaction in which the data was stored on the blockchain
* The AES password
* The AES initializaion vector (iv)
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


## 3. Upload KYC file

To upload KYC data, use `post /api/v1/encrypt_sign_store_file` and pass your primechain address and the file. For example:
```
{
  "primechain_address":"17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "file":"<your file>"
}
```
The output contains:
1. The transaction id of the transaction in which the data was stored on the blockchain
2. The digital signature
3. The 32 character AES password
4. The 12 character AES initializaion vector (iv)
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
Save this output along with the following:
* Customers identifier e.g. PAN, account number
* Price (optional)

***Note:***
* The encrypted KYC data is stored in the FILE_MASTERLIST stream. 
* Your primechain address, the data hash and the digital signature are stored in the FILE_SIGNATURE_MASTERLIST stream.


## 4. Download KYC file
To download data, use `post /api/v1/decrypt_download_file` and pass these values:   
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
