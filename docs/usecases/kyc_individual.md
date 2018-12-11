# KYC (Individual)

Financial and capital markets use the KYC (Know Your Customer) system to identify "bad" customers and minimise money laundering, tax evasion and terrorism financing. Efforts to prevent money laundering and the financing of terrorism are costing the financial sector billions of dollars. Banks are also exposed to huge penalties for failure to follow KYC guidelines. 

Costs aside, KYC can delay transactions and lead to duplication of effort between banks. B2 enables storage of encrypted records that can be viewed / purchased by banks that have been "whitelisted" by the issuer bank. This ensures data privacy and confidentiality while at the same time ensuring that records are shared only between banks that trust each other.

B2 is a secure platform for high-quality, validated KYC & due diligence information on individuals and corporates. 

All information is provided by Bankchain members in an encrypted format. Members may list a price for each record and may choose to share / sell the information to selected Bankchain members. 

***Primechain API can be used to create a transparent, secure and efficient sharing / monetization blockchain for 
high-quality, validated KYC & due diligence information on individuals.***

The blockchain nodes can be operated by Banks, Financial institutions and Regulators.

1. [Sign, encrypt and store KYC data in the blockchain](#1-sign-encrypt-and-store-kyc-data-in-the-blockchain)
2. [Decrypt, verify and retrieve KYC data from the blockchain](#2-decrypt-verify-and-retrieve-kyc-data-from-the-blockchain)

## 1. Sign, encrypt and store KYC data in the blockchain

To sign, encrypt and store KYC data in the blockchain, use [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain)

Sample input:
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
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
Sample output:
```
{
"status": 200,
"response": 
  {
    "tx_id_enc_data": "2f8b38c13db74e9a6f57edbd504f94fa9fd4138c3b0a68218f7bb83ad49848a9",
    "tx_id_signature": "e6bab35b15d91d02659fdfaebc96d50a6d76f7c4e620ba2ef662d78306ce1d15",
    "signature": "Hxc55xzUa4z/3/PoPTbWgOU0MCk+8Bne6Y65nkA4QOsueIR6HlRE0qlYUSpxwVEVuDn4E/VbgwWBCIknXB+f+EI=",
    "aes_password": "kTQCgp1AUvdjm1lMHe6vwN1zi3EthtKK",
    "aes_iv": "2F3FnHkHHd0R"
  }
}
```
Save this output in your private database along with the following:
* Customers identifier
* Price (optional)
* Description of the record

## 2. Decrypt, verify and retrieve KYC data from the blockchain
To decrypt, verify and retrieve KYC data in the blockchain, use [`decrypt_download_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#3-decrypt-verify-and-retrieve-data-from-the-blockchain)

Sample input:
```
{
  "tx_id_enc_data": "2f8b38c13db74e9a6f57edbd504f94fa9fd4138c3b0a68218f7bb83ad49848a9",
  "tx_id_signature": "e6bab35b15d91d02659fdfaebc96d50a6d76f7c4e620ba2ef662d78306ce1d15",
  "aes_password": "kTQCgp1AUvdjm1lMHe6vwN1zi3EthtKK",
  "aes_iv": "2F3FnHkHHd0R"
  }
```
Sample output:
```
{
"status": 200,
"response": 
  {
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

## 3. Sign, encrypt and store a file in the blockchain

To sign, encrypt and store a file in the blockchain, use [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)

## 3. Decrypt, verify and retrieve a file from the blockchain
To decrypt, verify and retrieve a file from the blockchain, use [`decrypt_download_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)
