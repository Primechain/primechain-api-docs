# KYC & Digital Identity verification 

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

TRADE-Chain provides a robust immutable platform for real-time KYC & Digital Identity verification. 

![KYC & Digital Identity verification ](http://www.primechaintech.com/img/api_documentation/kyc.png)

***Table of contents***


# 1. Issue KYC and Digital Identity records on TRADE-Chain

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

# 2. Retrieve KYC records from TRADE-Chain
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
