# Digital Signatures

1. [Signing data](#1-signing-data)
2. [Verifying a digital signature](#2-verifying-a-digital-signature)
3. [Sign and store signature](#3-sign-and-store-signature)

## 1. Signing data
To generate a digital signature, use `post /api/v1/create_signature` and provide 2 parameters - addresss (the blockchain address of the signer) and data (the hash of the information to be signed). Example:
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
  "data": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606"
}
```

The output will be the digital signature:
```
{
  "status": 200,
  "signature": "IJHOhoHoNaWtszoPnzp6VZnfQS8oa3UMv5QhnQ7SRLLpZ2nqDCcZpxXcLFHCYZP7snMsGRW4dOyl7AYzb/17QOI="
}
```
Note: The signature can be created only by the node containing the private key.

## 2. Verifying a digital signature

To verify that the the signature for the specified hash and public key is valid, use `post /api/v1/verify_signature` and provide 3 parameters - addresss (the blockchain address of the signer), data (the hash of the information to be verified) and signature (the digital signature). Example:
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
  "data": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606",
  "signature": "IJHOhoHoNaWtszoPnzp6VZnfQS8oa3UMv5QhnQ7SRLLpZ2nqDCcZpxXcLFHCYZP7snMsGRW4dOyl7AYzb/17QOI="
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

## 3. Sign and store signature 

To sign data and store the signature in the `SIGNATURE_MASTERLIST` data stream, use `post /api/v1/create_save_signature`.
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
  "data": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606"
}
```
The output will be the signature and the transaction id through which the signature is stored in the `GREAT` data stream:
```
{
"status": 200,
"response": 
  {
    "tx_id": "c2ac22b1603ace9d86a760f48c893906515edb2ae34b14770f73a5cd99177e9b",
    "signature": "IJHOhoHoNaWtszoPnzp6VZnfQS8oa3UMv5QhnQ7SRLLpZ2nqDCcZpxXcLFHCYZP7snMsGRW4dOyl7AYzb/17QOI="
  }
}
```
