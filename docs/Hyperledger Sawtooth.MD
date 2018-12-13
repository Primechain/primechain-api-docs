# Hyperledger Sawtooth

[1. Create key pair](#1-create-key-pair)      
[2. Publish data to the blockchain](#2-publish-data-to-the-blockchain)     
[3. Retrieve data from the blockchain](#3-retrieve-data-from-the-blockchain)    
[4. Crating a digital signature](#4-crating-a-digital-signature)   
[5. Verify a digital signature](#5-verify-a-digital-signature)   

## 1. Create key pair
To create a key pair, use `get /api/v1/create_user_key_sawtooth`
The output will be the 
1. Private_key
2. Public key
```
{
  "status": 200,
  "primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
  "primechain_sawtooth_public_key": "022dfb9755cf6a7313ddc58aa22894436d0e4c49e4c52f4706b554ef2dc56fc7de",
  "response": "User keys generated"
}
```

## 2. Publish data to the blockchain
To publish data to the blockchain, use `post /api/v1/upload_data_sawtooth` and pass 2 parameters:
1. Private_key
2. The data
```
{
  "primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
Output will be the Sawtooth address for the transaction.
```
{
  "status": 200,
  "primechain_sawtooth_address": "542e574e380d2d850c025b9dfdc28043487f17e5dcbe0220b1919db1dc85fa900987761f5ef72a9c3d60159141749b36f4abfab3a11a4ba85087a71f68eab716"
}
```

## 3. Retrieve data from the blockchain
To retrieve data from the blockchain, use `post /api/v1/get_data_sawtooth` and pass the Sawtooth address for the transaction.
```
{
  "primechain_sawtooth_address": "542e574e380d2d850c025b9dfdc28043487f17e5dcbe0220b1919db1dc85fa900987761f5ef72a9c3d60159141749b36f4abfab3a11a4ba85087a71f68eab716"
}
```
Output will be the data.
```
{
  "status": 200,
  "response": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
## 4. Crating a digital signature

To create a digital signature, use `post /api/v1/create_signature_sawtooth` and pass 2 parameters:
1. Private key
2. the data
```
{
  "primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
The output will be the digital signature:
```
{
  "status": 200,
  "signature": "d419285cc5087f28dd2bbf391c95ba46603d20ca916844c8b7af471bc12843214afeaf26eb6cca37c22aad42eb813b5afca98acb55ba5213a0a4ce2b92c3cf08"
}
```

## 5. Verify a digital signature
To create a digital signature, use `post /api/v1/verify_signature_sawtooth` and pass 2 parameters:
1. public key
2. the data
3. the digital signature
```
{
  "primechain_sawtooth_public_key": "022dfb9755cf6a7313ddc58aa22894436d0e4c49e4c52f4706b554ef2dc56fc7de",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times.",
  "signature": "d419285cc5087f28dd2bbf391c95ba46603d20ca916844c8b7af471bc12843214afeaf26eb6cca37c22aad42eb813b5afca98acb55ba5213a0a4ce2b92c3cf08"
}
```
The output will be:
