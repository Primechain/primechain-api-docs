# Electronic Signature Engine

[![Version](https://img.shields.io/badge/TRADE--Chain-v%201.0-brightgreen.svg)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_chain.md) [![Version](https://img.shields.io/badge/Contact-Primechain-blue.svg)](http://www.primechaintech.com/contactus.php)

1. [Signing data](#1-signing-data)
2. [Verifying a digital signature](#2-verifying-a-digital-signature)
3. [Sign and store signature in GREAT](#3-sign-and-store-signature-in-great)

## 1. Signing data
To generate a digital signature, use `post /api/v1/create_signature` and provide 2 parameters:
1. primechain addresss of the signer    
2. the data to be signed    

Example:
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
The output will be the digital signature:
```
{
  "status": 200,
  "signature": "H/zH4VWkOv9/Awu7OUEK43Fq1dtBcBxnrzmwOdytpsr0Grw+lPxWgbgh3Dcr4lhwgVOBb7vAoChjUvqxlqnpDAI="
}
```
Note: The signature can be created only by the node containing the private key of the signer.

## 2. Verifying a digital signature

To verify a signature, use `post /api/v1/verify_signature` and provide 3 parameters:
1. primechain addresss of the signer   
2. data    
3. digital signature   

Example:
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times.",
  "signature": "H/zH4VWkOv9/Awu7OUEK43Fq1dtBcBxnrzmwOdytpsr0Grw+lPxWgbgh3Dcr4lhwgVOBb7vAoChjUvqxlqnpDAI="
}
```
The output will be `true` if the signature is valid and `false` if the signature is invalid or if an error occurs.
```
{
"status": 200,
"response": true
}
```
```
{
"status": 200,
"response": false
}
```
Note: The signature can be verified by any node.

## 3. Sign and store signature in GREAT

To sign data and store the signature in the `GREAT` (Global Repository of E-signatures And Timestamps) data stream, use `post /api/v1/create_save_signature`.
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
The output will be the signature and the id of the transaction in which the signature is stored in the `GREAT` data stream:
```
{
"status": 200,
"response": 
  {
    "tx_id": "7d861030114ab5fb5b05c3307be04f9408c5e5251daade36996be4afba469bb3",
    "signature": "H/zH4VWkOv9/Awu7OUEK43Fq1dtBcBxnrzmwOdytpsr0Grw+lPxWgbgh3Dcr4lhwgVOBb7vAoChjUvqxlqnpDAI="
  }
}
```
