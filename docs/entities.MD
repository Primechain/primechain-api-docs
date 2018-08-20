# Entities

1. [Creating a new entity](#1-creating-a-new-entity)
2. [Creating a new entity (for external key management)](#2-creating-a-new-entity-for-external-key-management)
3. [List entities](#3-list-entities)


## 1. Creating a new entity
When you create a new signer (entity / person), ESE generates a public key, private key and a corresponding blockchain address. To create a new signer, use `get /api/v1/create_entity`. The output will be the blockchain address of the newly created signer.
```
{
"address": "159jsk5QNbd4ox521HxsgFK1zFM8fivWJRiUBM"
}
```
The private key is automatically stored in your node. This will not be visible to other nodes. If you don't want the private key stored in the node, use `get /api/v1/create_keypair `. 


## 2. Creating a new entity (for external key management)
If you want to generate a public/private key pair, which is not stored in the wallet and which is ready for external key management use `get /api/v1/create_keypair `. The output will be the blockchain address, public key and private key of the newly created signer.
```
{
"status": 200,
"address": "1SxJwKXwjCCoCdduECiNTNdkUThZgwknYdAwef",
"pubkey": "03954458fe54151b32a035e6179b18a74cb027b0201404c522a41efdc043f0a138",
"privkey": "VAV9DaTL8S4WjVCiezmGRTASH26GNmuaDVkee2jamZKVyWDLjMPE32R1"
}
```

## 3. List entities

