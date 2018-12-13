# Hyperledger Sawtooth

[1. Create key pair](#1-create-key-pair)
[2. Publish data to the blockchain](#2-publish-data-to-the-blockchain)  
[3. Retrieve data from the blockchain](#retrieve-data-from-the-blockchain) 

## 1. Create key pair
To create a key pair, use `get /api/v1/create_user_key_sawtooth`
```
{
"status": 200,
"primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
"primechain_sawtooth_public_key": "022dfb9755cf6a7313ddc58aa22894436d0e4c49e4c52f4706b554ef2dc56fc7de",
"response": "User keys generated"
}
```

## 2. Publish data to the blockchain
To publish data to the blockchain, use `post /api/v1/upload_data_sawtooth`
```
{
  "primechain_sawtooth_private_key": "2e04323b1e1fe072aea4620a46d234dd52dbf8f90cacdb7bf8579b65622ea59c",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
Output
```
{
"status": 200,
"primechain_sawtooth_address": "542e574e380d2d850c025b9dfdc28043487f17e5dcbe0220b1919db1dc85fa900987761f5ef72a9c3d60159141749b36f4abfab3a11a4ba85087a71f68eab716"
}
```

## Retrieve data from the blockchain
To retrieve data from the blockchain, use `post /api/v1/get_data_sawtooth`
```
{
"primechain_sawtooth_address": "542e574e380d2d850c025b9dfdc28043487f17e5dcbe0220b1919db1dc85fa900987761f5ef72a9c3d60159141749b36f4abfab3a11a4ba85087a71f68eab716"
}
```
Output
```
{
"status": 200,
"response": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
