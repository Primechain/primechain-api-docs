# KYC & Digital Identity verification 

[![Version](https://img.shields.io/badge/Version-1.0-brightgreen.svg)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_chain.md)

[![TRADE-Chain](https://img.shields.io/badge/Module%20of-TRADE--Chain-blue.svg)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_chain.md)


TRADE-Chain provides a robust immutable platform for real-time KYC & Digital Identity verification. 

![KYC & Digital Identity verification ](http://www.primechaintech.com/img/api_documentation/kyc.png)

***Table of contents*** 

[1. Issue KYC and Digital Identity records](#1-issue-kyc-and-digital-identity-records)   

[2. Search for KYC and Digital Identity records](#2-search-for-kyc-and-digital-identity-records)   

[3. Retrieve KYC and Digital Identity records](#3-retrieve-kyc-and-digital-identity-records)   


# 1. Issue KYC and Digital Identity records

To encrypt, sign and publish KYC records on TRADE-Chain, use `post /api/v1/publish_data` and pass 4 parameters: 
1. `primechain_address` - the primechain address of the signer.
2. `keys` - upto 5 keys can be used to enable quick searching of the data. Each key can be upto 64 characters including blank spaces.
3. `data` - the data. 
4. `trade_channel_name` - as kyc.

Lets take an example of Gopal Kumar Santoshi, a citizen of Zimblia having income tax registration number 235465657887565. This sample record is being published by Global Bank and is current as of 19-January-2019.
```
{
  "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
   "keys": 
    [
      "Gopal Kumar Santoshi",
      "235465657887565",
      "Zimblia",
      "Global Bank",
      "19-January-2019"
    ],
   "data": 
    {
      "name": "Gopal Kumar Santoshi",
      "name_of_father": "INDIVIDUAL",
      "name_of_wife": "Ekta Santoshi",
      "email": "gopal@example.com",
      "mobile": "+91-1234567890",
      "address": "213, Zimblia Avenue, Zimblia",
      "gender": "male",
      "date_of_birth": "06-NOV-1973",
      "driving_license": "0987654321 dated 11-JAN-2010 issued by RTO, Zimblia",
      "passport": "6554345678 dated 18-MAR-2010 issued by PPO, Zimblia"
    }, 
   "trade_channel_name": "kyc"
}
```

***This is what happens:***   
1. The SHA-512 hash of the data is computed.
2. The hash is signed using the private key of the provided primechain address (using ECDSA).
3. The digital signature, hash and the primechain address of the signer are stored in the trade channel.
4. The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
    * the encrypted version of the data    
    * the AES password    
    * the Initialization Vector (IV)    
    * the Authentication Tag (tag)   
5. The encrypted data and the tag are published to the specified trade channel.

***The following is the output:***
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the trade channel.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the the trade channel.
3. `signature` - the digital signature
4. `aes_password` - the AES password
5. `aes_iv` - the Initialization Vector (IV)
6. `trade_channel_name` - the name of the trade channel to which the data is published. 

Sample output
```
{
  "status": 200,
  "response": 
    {
      "tx_id_enc_data": "a5e3ff1e5d0e1b90098216e3e246bbea512adcb5413e1517dd25b86718a37a0e",
      "tx_id_signature": "bfb8b7b04d48c280ae3ec011f6f8505374b8538e3b139d9ae6dfb76ab19f0eed",
      "signature": "H+uDukHhapwSAzc0TJVoAnat3fvyIIV2OzJ3HJMicKz/UyVMCklIpLs0ZwAP9he1uPMDLURcQqUAeH/VC0C7MpM=",
      "aes_password": "iRvFOGQwimAjqbZvKKhgDlqG5yOk4BW9",
      "aes_iv": "YNxSvgWm2uVK",
      "trade_channel_name": "kyc"
    }
}
```
# 2. Search for KYC and Digital Identity records

To search for KYC and Digital Identity records on TRADE-Chain use `post /api/v1/list_stream_items_by_key` and pass 2 parameters:
1. `key` - the income tax registration number 
2. `stream_name` as kyc

Sample input
```
{
  "key": "235465657887565",
  "stream_name": "kyc"
}
``` 

Sample output
```
{
"status": 200,
"response": 
  [
    {
      "publishers": "164u1MZiF89pFfd9TTyh72vQMyPD8pYbd7eFDH",
      "key": 
        [
          "Gopal Kumar Santoshi",
          "235465657887565",
          "Zimblia",
          "Global Bank",
          "19-January-2019"
        ],
      "offchain": false,
      "available": true,
      "data": "
        {
            "content":"1f6688e01f060a5b004b72906f886434a5514643b5221a1be48aefa8b0985308dcd63763c3eb8b54bf4444e778410887c5f455bd029d75d8c5358fc1555fe535890264b2f0c1bd53e66e53c8093c573e614bcbcdc4a1dce0469cbb50614e795a00db1e8e8a0a01bf3033368b71a0f9f427a48533c65b90a7316644907b1efb9f6a33ecf0baf5b7d1b65d6fa5c67f2e6d53fef7f49ab67912c10e6d0e4a98e5d9890a5ed412f8916544dd776c4454953d2bb8f61e08a18253781dedd7207d00ef7756a6df919ad3c0c47f6ac371ba9cdac2f1b563a8e7d259feefac657565074ee85150245056bbf5ce98c7545de05f70cf10fe6d211fb11e04e8366659a07b301c8500b10e664972f65a432122fa816ecf0b3ea9b7da3a12b18479b8a960a57cec481f919ed7c28a147276b9cbf22a4d0560dda24bce590cd350e127e1b2a5bb50283b74b36b7a65559c4ddadbbca2a5b00dd9a846d457de7a0ce477c21f955d578956a3cbd230d98812b2f5d3273b702874",
            "tag":
              {
                "type":"Buffer",
                "data":[93,24,105,196,53,45,127,77,51,121,189,218,230,203,253,232]
               }
          }",
      "confirmations": 11,
      "blockhash": "032e6684653b576ea26b6733feb03dbc3b25d27f075167c3838011f17bb60a46",
      "blockindex": 2,
      "blocktime": 1547887737,
      "txid": "a5e3ff1e5d0e1b90098216e3e246bbea512adcb5413e1517dd25b86718a37a0e",
      "vout": 0,
      "valid": true,
      "time": 1547887724,
      "timereceived": 1547887724
     }
  ],
}
```
The actual record is stored in encrypted form and cannot be decrypted without the relevant credentials. In the above sample, the encrypted version of the actual record is displayed as:
```
"content":"1f6688e01f060a5b004b72906f886434a5514643b5221a1be48aefa8b0985308dcd63763c3eb8b54bf4444e778410887c5f455bd029d75d8c5358fc1555fe535890264b2f0c1bd53e66e53c8093c573e614bcbcdc4a1dce0469cbb50614e795a00db1e8e8a0a01bf3033368b71a0f9f427a48533c65b90a7316644907b1efb9f6a33ecf0baf5b7d1b65d6fa5c67f2e6d53fef7f49ab67912c10e6d0e4a98e5d9890a5ed412f8916544dd776c4454953d2bb8f61e08a18253781dedd7207d00ef7756a6df919ad3c0c47f6ac371ba9cdac2f1b563a8e7d259feefac657565074ee85150245056bbf5ce98c7545de05f70cf10fe6d211fb11e04e8366659a07b301c8500b10e664972f65a432122fa816ecf0b3ea9b7da3a12b18479b8a960a57cec481f919ed7c28a147276b9cbf22a4d0560dda24bce590cd350e127e1b2a5bb50283b74b36b7a65559c4ddadbbca2a5b00dd9a846d457de7a0ce477c21f955d578956a3cbd230d98812b2f5d3273b702874"
```

# 3. Retrieve KYC and Digital Identity records
To retrieve data use `post /api/v1/get_data` and pass 5 parameters:
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the trade channel.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the trade channel.
3. `aes_password` - the AES password.
4. `aes_iv` - the Initialization Vector (IV).
5. `trade_channel_name` - the name of the trade channel from which the data is to be retrieved.

Sample input
```
{
  "tx_id_enc_data": "a5e3ff1e5d0e1b90098216e3e246bbea512adcb5413e1517dd25b86718a37a0e",
  "tx_id_signature": "bfb8b7b04d48c280ae3ec011f6f8505374b8538e3b139d9ae6dfb76ab19f0eed",
  "aes_password": "iRvFOGQwimAjqbZvKKhgDlqG5yOk4BW9",
  "aes_iv": "YNxSvgWm2uVK",
  "trade_channel_name": "kyc"
}
```
***This is what happens:***   
1. The digital signature, hash and the primechain address of the signing entity are retrieved from the trade channel.
2. The encrypted data and tag are retrieved from the trade channel.
3. The encrypted data is decrypted.
4. The digital signature is verified.

***The following is the output:***
1. `data` - the unencrypted data.   
2. `primechain_address` - the primechain address of the signer.   
3. `signature_status` - the verification status of the signature.  
4. `timestamp` - the timestamp

Sample output
```
{
  "status": 200,
  "response": 
    {
      "data": 
        {
          "name": "Gopal Kumar Santoshi",
          "name_of_father": "INDIVIDUAL",
          "name_of_wife": "Ekta Santoshi",
          "email": "gopal@example.com",
          "mobile": "+91-1234567890",
          "address": "213, Zimblia Avenue, Zimblia",
          "gender": "male",
          "date_of_birth": "06-NOV-1973",
          "driving_license": "0987654321 dated 11-JAN-2010 issued by RTO, Zimblia",
          "passport": "6554345678 dated 18-MAR-2010 issued by PPO, Zimblia"
        },
      "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
      "signature_status": true,
      "timestamp": "19/01/2019 08:48:44:00"
    }
}
```
