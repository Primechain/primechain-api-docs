# KYC (Individual)

1. [Upload KYC data](#1-upload-kyc-data)
2. [Download KYC data](#2-download-kyc-data)
3. [Upload KYC file](#3-upload-kyc-file)
4. [Download KYC file](#4-download-kyc-file)

# 1. Upload KYC data

To upload KYC data, use `post /api/v1/encrypt_sign_store_data` and pass the following parameters:   
1. Your primechain address. The primechain private key coressponding to this address will be used to sign the data. Note: The address must have write permissions to DATA_MASTERLIST and DATA_SIGNATURE_MASTERLIST granted by the seed node.

2. The KYC data. The recommended KYC codes are stored in the `CODE_MASTERLIST` stream.

For example:
```
{
  "primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
  "data": 
  {
    "data_category": "KYC",
    "entity_category": "INDIVIDUAL",
    "name": "Gopal Kumar Santoshi",
    "name_father": "INDIVIDUAL",
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
4. The 12 character AES initializaion vector (IV)
```
{
"status": 200,
"response": {
"tx_id": "9a6fa8fe940fb6cc36936ce18cc1fd13b1b9b16ab5de372c24330df624e51240",
"signature": "HyI4D2W8R6hqMQleDEWrS0stNk493YpERpm4pMESK8BBKYGnMkYxMiEB/hsH/UiuLHGoTmoR2Z/vQBpsAqIvhIw=",
"password": "4El9Aidug9aj4Co1XPc57pyrpQn675rh",
"iv": "XDNffhBhkEq4"
}
}

```
Save this output along with the following:
* Customers identifier e.g. PAN, account number
* Price (optional)

***Note:***
* The encrypted KYC data is stored in the DATA_MASTERLIST stream.   
* Your primechain address, the data hash and the digital signature are stored in the DATA_SIGNATURE_MASTERLIST stream.

# 2. Download KYC data
To download data, use `post /api/v1/decrypt_download_data` and pass these parameters:
* The transaction id of the transaction in which the data was stored on the blockchain
* The AES password
* The AES initializaion vector (iv)
```
{
"tx_id": "9a6fa8fe940fb6cc36936ce18cc1fd13b1b9b16ab5de372c24330df624e51240",
"password": "4El9Aidug9aj4Co1XPc57pyrpQn675rh",
"iv": "XDNffhBhkEq4"
}
```
The output will be the data.
```
{
"status": 200,
"response": {
"data_category": "KYC",
"entity_category": "INDIVIDUAL",
"name": "Gopal Kumar Santoshi",
"name_father": "INDIVIDUAL",
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

# 3. Upload KYC file

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


# 4. Download KYC file
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
