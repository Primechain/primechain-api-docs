# List of data streams

[ASSET_DATA_MASTERLIST](#asset_data_masterlist)   
[BLACKLIST_MASTERLIST](#blacklist_masterlist)    
[BLOB_STREAM](#blob_stream)    
[DATA_MASTERLIST](#data_masterlist)     
DATA_SIGNATURE_MASTERLIST   
FILE_MASTERLIST   
FILE_SIGNATURE_MASTERLIST   
GREAT   
OFFER_DETAILS_STREAM   
ONBOARD_USERLIST   

[RSA_MASTERLIST](#rsa_masterlist)   
SIGNATURE_MASTERLIST      
WHITELIST_MASTERLIST   

# ASSET_DATA_MASTERLIST

# BLACKLIST_MASTERLIST

# BLOB_STREAM   

# DATA_MASTERLIST   

# DATA_SIGNATURE_MASTERLIST   

# FILE_MASTERLIST   

# FILE_SIGNATURE_MASTERLIST   

# GREAT   

# OFFER_DETAILS_STREAM   

# ONBOARD_USERLIST

# RSA_MASTERLIST
Data is entered into this stream when the `onboard_user` end-point is used. The data stored is:
1. the newly created entity's primechain address,    
2. the newly created entity's primechain public key,    
3. the newly created entity's RSA public key    

To obtain the data in this stream, use `list_stream_items` and pass the stream name as the value:
```
{
  "stream_name": "RSA_MASTERLIST"
}
```
The output will be something like this:
```
aaa
```

# SIGNATURE_MASTERLIST      


# WHITELIST_MASTERLIST   

