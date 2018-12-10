# List of data streams

This is the list of all the data streams created automatically by Primechain API. Click on a stream name to see details.

[ASSET_DATA_MASTERLIST](#asset_data_masterlist)     
[AUTH_USERS_MASTERLIST](#auth_users_masterlist)   
[BLACKLIST_MASTERLIST](#blacklist_masterlist)    
[BLOB_STREAM](#blob_stream)    
[DATA_MASTERLIST](#data_masterlist)     
[CODE_MASTERLIST](#code-masterlist)   
[DATA_SIGNATURE_MASTERLIST](#data_signature_masterlist)    
[FILE_MASTERLIST](#file_masterlist)     
[FILE_SIGNATURE_MASTERLIST](#file_signature_masterlist)    
[GREAT](#great)   
[OFFER_DETAILS_STREAM](#offer_details_stream)   
[ONBOARD_USERLIST](#onboard_userlist)      
[RSA_MASTERLIST](#rsa_masterlist)   
[SIGNATURE_MASTERLIST](#signature_masterlist)      
[VERIFIED_USER_MASTERLIST](#verified_user_masterlist)   
[WHITELIST_MASTERLIST](#whitelist_masterlist)   


# ASSET_DATA_MASTERLIST

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

# BLACKLIST_MASTERLIST

# BLOB_STREAM   

# CODE_MASTERLIST   

# DATA_MASTERLIST   

# DATA_SIGNATURE_MASTERLIST   

# FILE_MASTERLIST   

# FILE_SIGNATURE_MASTERLIST   

# GREAT   

# OFFER_DETAILS_STREAM   

# ONBOARD_USERLIST

# RSA_MASTERLIST


# SIGNATURE_MASTERLIST      

# VERIFIED_USER_MASTERLIST

# WHITELIST_MASTERLIST   

