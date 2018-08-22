# Digital Signatures

1. [Signing data](#1-signing-data)
2. [Verifying a digital signature](#2-verifying-a-digital-signature)

## 1. Signing data
To generate a digital signature, use `post /api/v1/create_signature` and provide 2 parameters - addresss (the blockchain address of the signer) and message (the hash of the data to be signed). Example:
```
{
  "address": "1PQ81MEXFtLMrf8iqXZm7tMqnkEDDYs71GDrot",
  "message": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606"
}
```
![Signing data](http://www.primechaintech.com/img/api_documentation/create_signature.png)

The output will be the digital signature:
```
{
"status": 200,
"signature": "IK+0M1DdcCnjIzVB4j997WusLlglq3rhBFsqEsuxkOZ7XwseQR2yJQ9/eOp/h/a6lt38iTu4aYceSx1yE1oUYIs="
}
```
Note: The signature can be created only by the node containing the private key.

## 2. Verifying a digital signature

To verify that the the signature for the specified hash and public key is valid, use `post /api/v1/verify_signature` and provide 3 parameters - addresss (the blockchain address of the signer), message (the hash of the data to be verified) and signature (the digital signature). Example:
```
{
  "address": "1PQ81MEXFtLMrf8iqXZm7tMqnkEDDYs71GDrot",
  "message": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606",
  "signature": "IK+0M1DdcCnjIzVB4j997WusLlglq3rhBFsqEsuxkOZ7XwseQR2yJQ9/eOp/h/a6lt38iTu4aYceSx1yE1oUYIs="
}
```
![Verifying a digital signature](http://www.primechaintech.com/img/api_documentation/verify_signature.png)
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
