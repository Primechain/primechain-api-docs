# List of data streams

This is the list of all the data streams created automatically by Primechain API. Click on a stream name to see details.

[ASSET_DATA_MASTERLIST](#asset_data_masterlist)     
[AUTH_USERS_MASTERLIST](#auth_users_masterlist)   
   
   
[DATA_MASTERLIST](#data_masterlist)     
[DATA_SIGNATURE_MASTERLIST](#data_signature_masterlist)    
[FILE_MASTERLIST](#file_masterlist)     
[FILE_SIGNATURE_MASTERLIST](#file_signature_masterlist)    
[GREAT](#great)   
[OFFER_DETAIL_STREAM](#offer_detail_stream)   
[ONBOARD_USERLIST](#onboard_userlist)      
[RSA_MASTERLIST](#rsa_masterlist)   

[VERIFIED_USER_MASTERLIST](#verified_user_masterlist)   
   




# ASSET_DATA_MASTERLIST
This is a closed stream.

Asset creators write to this stream when using [create_new_asset_from](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Smart%20Asset%20Lifecycle%20Management.MD#1-create-a-new-asset)


# AUTH_USERS_MASTERLIST
Data is entered into this stream when the `onboard_user` end-point is used. The data stored is:
1. new user's identifier
2. new user's description
3. new user's primechain address
4. new user's primechain public key
5. new user's RSA public key

To obtain the data in this stream, use `list_onboarded_user_details` and pass the user's primechain address as the parameter:
```
{
  "primechain_address": "1Pjzi3yK3jFCLCte2uTTYiHbh8QVTh6SNS8ehY"
}
```
The output will be something like this:
```
{
  "status": 200,
  "response": 
    {
      "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqLaEj608vDUGt/XZ0nmp L5x6vmJFli/ms30JSjjjcaAyAKMzn2c50jTERDhIvSh02Baa2SVu6KtlwxAKWzXG MQhiv2dsgL+ZanIQbP9WFzPw5VqlPs9O0BtnPkPWV9t31+YTAKirlwJbOsbvMQ2P x0rxaY7Fia5ifrlYNVwE/uMOWXhii7LdNcmTR9q1KW1KQUAy8agmShC+WmNEMRhy qPy1DehtKgeiE0Gq0bJmGg9BlTKF40DuXAuWHgS/oMOdaEK0afdz+ltm9vcAU1OW gPPPX7XTOusYtLT/S88oSlEPgJl0E9Xq1kBT1gbs1vGjyjDP9qdvSVSIBcwNRcAS MwIDAQAB -----END PUBLIC KEY-----",
      "user_identifier": "Sanya Nagpal",
      "user_description": "Indian citizen holding passport number 987654321",
      "primechain_public_key": "0300d59b899af64b7771423eda8b37e7f62e5f97b6a6f13fc77f3c4e9cd3430215"
   }
}
```

 
# DATA_MASTERLIST   
* This is a closed stream.

* Verified addresses write to DATA_MASTERLIST when using [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain) and [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)

* Verified users are those that are listed in VERIFIED_USER_MASTERLIST stream. They are given write permissions as described [here](https://github.com/Primechain/primechain-api/blob/master/README.md#28-verified-users).


# DATA_SIGNATURE_MASTERLIST   
* This is a closed stream.

* Verified addresses write to DATA_SIGNATURE_MASTERLIST when using [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain) and [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)

* Verified users are those that are listed in VERIFIED_USER_MASTERLIST stream. They are given write permissions as described [here](https://github.com/Primechain/primechain-api/blob/master/README.md#28-verified-users).


# FILE_MASTERLIST   
* This is a closed stream.

* Verified addresses write to FILE_MASTERLIST when using [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain) and [`decrypt_download_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)

* Verified users are those that are listed in VERIFIED_USER_MASTERLIST stream. They are given write permissions as described [here](https://github.com/Primechain/primechain-api/blob/master/README.md#28-verified-users).



# FILE_SIGNATURE_MASTERLIST   
* This is a closed stream.

* Verified addresses write to FILE_MASTERLIST when using [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain) and [`decrypt_download_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#5-decrypt-verify-and-retrieve-a-file-from-the-blockchain)

* Verified users are those that are listed in VERIFIED_USER_MASTERLIST stream. They are given write permissions as described [here](https://github.com/Primechain/primechain-api/blob/master/README.md#28-verified-users).


# GREAT   
* This is an open stream.

* Signatures created using [`create_save_signature`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Digital%20signatures.MD#3-sign-and-store-signature-in-great) are stored in GREAT (Global Repository of E-signatures And Timestamps) data stream.


# OFFER_DETAIL_STREAM   
* This is an open stream.

Following data of offers built using [`create_public_offer`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Offer%20management.MD#1-create-a-public-offer) are stored here: 

1. primechain_address of the offer creator   
2. name of asset asked for   
3. name of asset offerred   
4. quantity of asset asked for   
5. quantity of asset offerred   
6. offer hex blob   

# ONBOARD_USERLIST

# RSA_MASTERLIST
    

# VERIFIED_USER_MASTERLIST   
This is a closed stream.

Seed node writes to it when a new verified address is requested by a member. 

Verified addresses are given write permissions to  DATA_SIGNATURE_MASTERLIST and DATA_MASTERLIST streams so that they can use [`encrypt_sign_store_data`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#2-sign-encrypt-and-store-data-in-the-blockchain) and [`encrypt_sign_store_file`](https://github.com/Primechain/primechain-api-docs/blob/master/docs/Encrypted%20data%20storage.MD#4-sign-encrypt-and-store-a-file-in-the-blockchain)

 

