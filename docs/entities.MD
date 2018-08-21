# Entities

1. [Creating a new entity](#1-creating-a-new-entity)
2. [Creating a new entity (for external key management)](#2-creating-a-new-entity-for-external-key-management)
3. [List entities](#3-list-entities)
4. [Create multisig address](#4-create-multisig-address)



## 1. Creating a new entity
When you create a new signer (entity / person), ESE generates a public key, private key and a corresponding blockchain address. To create a new signer, use `get /api/v1/create_entity`. The output will be the blockchain address of the newly created signer.
![Creating a new entity](http://www.primechaintech.com/img/api_documentation/create_entity.png)
```
{
"address": "1PQ81MEXFtLMrf8iqXZm7tMqnkEDDYs71GDrot"
}
```
The private key is automatically stored in your node. This will not be visible to other nodes. If you don't want the private key stored in the node, use `get /api/v1/create_keypair `. 

## 2. Creating a new entity (for external key management)
If you want to generate a public/private key pair, which is not stored in the wallet and which is ready for external key management use `get /api/v1/create_keypair`. The output will be the blockchain address, public key and private key of the newly created signer.
![Creating a new entity (for external key management)](http://www.primechaintech.com/img/api_documentation/create_keypair.png)
```
{
"status": 200,
"address": "1SxJwKXwjCCoCdduECiNTNdkUThZgwknYdAwef",
"pubkey": "03954458fe54151b32a035e6179b18a74cb027b0201404c522a41efdc043f0a138",
"privkey": "VAV9DaTL8S4WjVCiezmGRTASH26GNmuaDVkee2jamZKVyWDLjMPE32R1"
}
```

## 3. List entities
To get a list of entities in this node's wallet, use `get /api/v1/list_entities`
![List entities](http://www.primechaintech.com/img/api_documentation/list_entities.png)
```
{
  "list_entities": 
  [
    {
      "address": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1"
     },
    {
       "address": "1f2N8o6MmK1rTvf6kZKxWiCMZ84wFLWhdD2V5"
    },
    {
      "address": "1ZKRvTnxuYzmHFnSpTwLGKvWnSjYkJYrehm8uf"
    },
    {
      "address": "1UDowrpjFXZjdzTwWmcWfMrekdZvpjstoPiMGk"
    },
    {
      "address": "1MVeZ9GJxX7uXfijq6ZeDsAXWCPYZRALfNidvD"
    },
    {
      "address": "159jsk5QNbd4ox521HxsgFK1zFM8fivWJRiUBM"
    },
    {
      "address": "1LgxYpp4fPd6hVivcVa7HGLbmR6AZzvqdHwXdj"
    }
  ],
}
```
## 4. Create multisig address
To create a pay-to-scripthash (P2SH) multisig address and add it to the wallet, use `create_multisig_address`. Funds sent to this address can only be spent by transactions signed by `nrequired` of the specified keys.
![Create multisig address](http://www.primechaintech.com/img/api_documentation/create_multisig_address.png)
Each key can be a full public key, or an address if the corresponding key is in the node's wallet. Output is the P2SH multisig address.
```
{
"status": 200,
"address": "47m73n8bFqbjxJiTXvNpKNekKjsQG2yf6g5B1p",
"redeem_script": "51210266f1068c2cd4681af9c60ca502d9cbea34bcc33a697cbe443df63d79214a011d21034cc36b3b86e632bc23e5aa7e0f28e159baee469feb43d1e4227b6706f27aedd852ae"
}
```
