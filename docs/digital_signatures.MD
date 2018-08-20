## 1. Signing data
To generate a digital signature, use `post /api/v1/create_signature` and provide 2 parameters - addresss (the blockchain address of the signer) and message (the hash of the data to be signed). Example:
```
{
  "address": "1LgxYpp4fPd6hVivcVa7HGLbmR6AZzvqdHwXdj",
  "message": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606"
}
```
The output will be the digital signature:
```
{
"status": 200,
"signature": "H0rpS5JUamrWh8tQrlMpwFmSqyoL1u4IuOYY1LuJJGdVEj48m6G2pxwlPeoZzxyH5lOXR+DS3ZbX12eMEbajLYw="
}
```
Note: The signature can be created only by the node containing the private key.

## 2. Verifying a digital signature

To verify that the the signature for the specified hash and public key is valid, use `post /api/v1/verify_signature` and provide 3 parameters - addresss (the blockchain address of the signer), message (the hash of the data to be verified) and signature (the digital signature). Example:
```
{
  "address": "1LgxYpp4fPd6hVivcVa7HGLbmR6AZzvqdHwXdj",
  "message": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606",
  "signature": "H0rpS5JUamrWh8tQrlMpwFmSqyoL1u4IuOYY1LuJJGdVEj48m6G2pxwlPeoZzxyH5lOXR+DS3ZbX12eMEbajLYw="
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
