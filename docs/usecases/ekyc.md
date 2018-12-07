# Corporate & Individual KYC and due-diligence

1. [Upload KYC data](#1-upload-kyc-data)
2. [Download KYC data](#2-decrypt-and-download-data)
3. [Upload KYC file](#3-encrypt-sign-and-upload-file)
4. [Download KYC file](#4-decrypt-and-download-file)

# 1. Upload KYC data

To upload KYC data, use `post /api/v1/encrypt_sign_store_data` and pass your primechain address and the data. For example:
```
{
  {
  "primechain_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "data": 
    {
      "type": "GUARANTEE",
      "10001010": "cin",
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
* Your primechain address, the data hash and the digitsal signature are stored in the DATA_SIGNATURE_MASTERLIST stream.






