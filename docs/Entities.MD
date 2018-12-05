# Entity creation & permissions management

[1. Creating a new entity](#1-creating-a-new-entity)   
[2. Creating a new entity (for external key management)](#2-creating-a-new-entity-for-external-key-management)   
[3. Creating a new entity (with RSA keys)](#3-creating-a-new-entity-with-rsa-keys)   
[4. Create multisig address](#4-create-multisig-address)   
[5. Grant permissions to an entity](#5-grant-permissions-to-an-entity)   
[6. Revoke permissions to an entity](#6-revoke-permissions-to-an-entity)   
[7. List permissions given to all entities](#7-list-permissions-given-to-all-entities)   
[8. Information about the addresses in the wallet](#8-information-about-the-addresses-in-the-wallet)   
[9. Validate address](#9-validate-address)   
[10. List entities](#10-list-entities)   


## 1. Creating a new entity
To create a new entity, use `get /api/v1/create_entity`.The following are generated:
* a public key, 
* a private key 
* a blockchain address. 

 The output will be the blockchain address of the newly created signer.
```
{
"status": 200,
"primechain_address": "1VCeqGYXLaqMtAFtxTNeTzfW8T714us2t3uwYM"
}
```
The private key is automatically stored in your node. This will not be visible to other nodes. If you don't want the private key stored in the node, use `get /api/v1/create_keypair`. 

## 2. Creating a new entity (for external key management)
If you want to generate a blockchain key pair which is not stored in the wallet and which is ready for external key management use `get /api/v1/create_keypair`. The output will be the blockchain address, blockchain public key and blockchain private key of the newly created entity.

```
{
"status": 200,
"response": 
  {
    "primechain_privkey": "V7MjFJkL9jX5Ubb8PVuqxcyKarUawtweoHBChYVC6F3LMmqTLcK29Tpm",
    "primechain_address": "16FmdRaQLPPbiNRH2ECWCXShTDiXUpjw9QUXPb",
    "primechain_pubkey": "02134c2ab1a1bfe97dd9d0c23b658b0e1b3f012ac3d9a00387351c7e87994987ae"
   }
}
```

## 3. Creating a new entity (with RSA keys)
If you want to generate a blockchain key pair along with an RSA key pair, use `get /api/v1/create_entity_rsa`. The output will be the:
* primechain address
* primechain public key
* primechain private key
* RSA private key (this is also stored in the RSA_MASTERLIST data stream)   
* RSA public key

```
{
 "status":200,
 "response":   
  {
    "primechain_address":"1CAWXRnYRuteZ6L2LTEgCBZhUaDCppDG8CmGMJ",
    "primechain_privkey":"VDFNDcRuzdBaEKNFWgRfu5aiZBeqtRit9TW4dM4GCh61JECsV4e8B1B7",
    "primechain_pubkey":"02d7afe9af7402a43419dea57b8eb7735d6de95d147835da1e290c8b42e07b3180",
    "rsa_privkey":"-----BEGIN PRIVATE KEY-----\nMIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQC28MoHm4q9uPey\nkyUrCy3FlYEoTEDCb86TTDHT7PEI6ujQYpubSjbLJsuu2dCNEeNi7Gm5zd2phszS\nHcUNRam63Y9GYAdczgUcMB4/oRrWYINLthV1G07PljlFM9YzwjHADV0iqLZP3QPe\npwtMqLJf/kR/pht3xJ6Qh2DH7DuTGEjmnhpvUNCMHtrdG8t68Imq1QRqQPFtvjZP\nkNa0NQpTgD0O8niVxdN3vwWYSQVTDrPvSa9yHMdjSJUjNDJUzfdyqm/c57L8OxAJ\nQanuToKuxLy/fPJeCzjfZOzY/mdH6MdYwnviOWmoj5xOd3acfiSGBMjvjPrwrArk\nuDWSsUiNAgMBAAECggEAO+3DcRyOJbqbQh+b9G7UDr78MZRRPqDb3jr+s7sR9ubl\nX6Z97TAxpPlPjjcCb8QlZjmmJN0AuVFUdZyU+dURVgrQrbA1mTxQRjypHBUNsp6p\nRDsg6l0Iw04l8rqZeBksrQpzsS/tkVoIs36rX/B/hpzIGbzzkJeTjisbFEMZ/QRQ\nyPfRD9ykd6jxKuzX1+kq/xloo4dzJ6/PiRJFTVTKTG5VeEsgxcPh0R37WWQizQMK\nzSc6wgHspSVcYhe6kCoRQVI42vQkhLJnAN4LxQvkunRVhrT7zmAFRmV6XSONV9ne\nrYR3l7ExIDzI8/3Wb1ilqfo7ssSJ+q4MHwSuT4NpbQKBgQDbKn69pcTF5nMt94bs\nfog5oB0+G19Ccn4q667+mu4cLhHbalzXF9on9SCWcf/LfOArOSbZDDp1gCTKU+sW\n4kCzqwRi1TvGCzRRrKBTnAreLx9Baz76QKOnXGGXVu5R6D1iTBCVqyNzy9+a3X/K\n32lxelj5hWjazWXzRD+ZmH66rwKBgQDVr7bVttFUOkPFLQ4MFgtXTO2ORvZ+tfWQ\nQCvvvLh29iTxDzD9c80T2MLwv7hwu9fY+IFx5fQUQBm+6niqN4H6wGq53mPfxGg0\nEvM/pwNo5cCY+Nlh+S5WKQMoc4Ehe94dJGkNn2anRtNbyA1bF97Zh4RMISaDbYBe\nOqQd3XCPgwKBgQCftdHyRbClPpBEuRKbmIGQ7LsinTPH6kNC58j4RNKrum7M5C+P\nlxQk9h6vQ5fSI8f/93/1v1GCesVUo963KF1aEI/7rcQHR/byZcfX5eiNjO1L8OlN\n2Hjp5wo/DNxS19iTnzaeur31DmZ+JleP8UqXpT7dZnjIqdFXey6VsWj4hQKBgAHt\nTrnIp0SaLehGSr0jKcEEyZOh4jEsVOWTHpJP4l34REcEOw3eEHhgWQmwwOoLV5v2\nSbyMNVJFbbYCCUqHq51mRNAeSEpJTCNEFHt7dxVoFP+MJvGyPI+8WPHxcLWrl0ot\n/OCJknRpuBg4yp4KrhDKHxBMsDs5LpIq9zXpvE0fAoGARpEc3Z0WciBr2v94aFGm\ne/78DLEhyaCT13DAvzx1fgGwXobocbECzYSvjrwcYN19MOs7XDqeXWaPkP3tLwr2\naaNe9xDyUxDQObJuTmef+Fjj+6iNQRiPAQdCjcNNH64tg39ubc0qNOMHE4rvM9rW\njh88H0YIlvbayBocGik4Qs0=\n-----END PRIVATE KEY-----",
    "rsa_pubkey":"-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtvDKB5uKvbj3spMlKwst\nxZWBKExAwm/Ok0wx0+zxCOro0GKbm0o2yybLrtnQjRHjYuxpuc3dqYbM0h3FDUWp\nut2PRmAHXM4FHDAeP6Ea1mCDS7YVdRtOz5Y5RTPWM8IxwA1dIqi2T90D3qcLTKiy\nX/5Ef6Ybd8SekIdgx+w7kxhI5p4ab1DQjB7a3RvLevCJqtUEakDxbb42T5DWtDUK\nU4A9DvJ4lcXTd78FmEkFUw6z70mvchzHY0iVIzQyVM33cqpv3Oey/DsQCUGp7k6C\nrsS8v3zyXgs432Ts2P5nR+jHWMJ74jlpqI+cTnd2nH4khgTI74z68KwK5Lg1krFI\njQIDAQAB\n-----END PUBLIC KEY-----",
    "transaction_id":"fd73c8028fdca76d435c1c058eb4e54f8ee8a1754d61a9e8cad60aa538ea1060"
   }
 }
```

## 4. Create multisig address
To create a pay-to-scripthash (P2SH) multisig address and add it to the wallet, use `post /api/v1/create_multisig_address`. Funds sent to this address can only be spent by transactions signed by `nrequired` of the specified keys.
```
{
  "nrequired": 2,
  "address": [
    "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
    "1af89TzR7d7N3pqtKrfzQFxz9MYuNvpt2iFBmj",
    "1B14GaGb9KQYy7poHQA4JvrzgRmLs6QFyX4dw6"
  ]
}
```
Each key can be a full public key, or an address if the corresponding key is in the node's wallet. Output is the P2SH multisig address.
```
{
 "status": 200,
 "primechain_address": "4PDTYCYWRVwkjLHCH9RCkq5csUJ7LFwMMDHjfM",
 "redeem_script": "52210203f2047224b87a0e8fffa61a4741d13cb215e1735b16570eacb2c3729aa129aa210301b67565c43d7f130be061b66ed7f1160b02f72e9054ff573ddc6baac76a4a1321028cce374a25e5c2640c99ae5f4112f27d1ededb7e3160cafbee0592ec102b125653ae"
}
```
## 5. Grant permissions to an entity
Use `post /api/v1/grant_permissions` to grant 1 or more of the following 8 permissions 
* ***connect***	to connect to other nodes and see the blockchain's contents
* ***send***	to send smart blockchain assets to other entities
* ***receive***	to receive smart blockchain assets from other entities
* ***issue***	to issue new smart assets
* ***create***	to create data streams
* ***mine***	to mine blocks
* ***activate***	to change connect, send and receive permissions for other entities
* ***admin***	to change all permissions for other entities, including issue, mine, activate and admin
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
  "permission": "send,receive"
}
```
The output will be the txid of the transaction in which the permissions were granted.
```
{
 "status": 200,
 "transaction_id": "39ecbdc585812403cf7591449b71ae39ced68b044c9e8f2a969ba02cd5ac25ee"
}
```
***Note:*** Permissions can be revoked using `revoke_permission.`

## 6. Revoke permissions to an entity
Use `post /api/v1/revoke_permissions` to revoke the specified permissions from the specified address.
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
  "permission": "send,receive"
}
```
The output will be the txid of the transaction in which the permissions were revoked.
```
{
"status": 200,
"transaction_id": "1427b87f4d7b0d42bb84a0f52c068f04b99e9bc7773155280f7b26d618ac9e66"
}
```

## 7. List permissions given to all entities
To get a list of all permissions which have been explicitly granted to a specific address, use `post /api/v1/listpermissions` and pass the primechain address as a parameter:
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
}
```
The output will be something like this:
```
{
"status": 200,
"primechain_address": [
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "connect",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "send",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "receive",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "issue",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "create",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "mine",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "admin",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
},
  {
"address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"for": null,
"type": "activate",
"startblock": 0,
"endblock": 4294967295,
"admins": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"pending": [],
}
],
}
```

## 8. Information about the addresses in the wallet

To get information about the addresses in the wallet, use `get /api/v1/listaddresses`. 
![Information about the addresses in the wallet](http://www.primechaintech.com/img/api_documentation/listaddresses.png)
```
{
 "status": 200,
 "primechain_address": 
 [
  {
    "address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
    "ismine": true,
    "iswatchonly": false,
    "isscript": false,
    "pubkey": "0203f2047224b87a0e8fffa61a4741d13cb215e1735b16570eacb2c3729aa129aa",
    "iscompressed": true,
    "account": "",
    "synchronized": true
  },
  {
    "address": "1af89TzR7d7N3pqtKrfzQFxz9MYuNvpt2iFBmj",
    "ismine": true,
    "iswatchonly": false,
    "isscript": false,
    "pubkey": "0301b67565c43d7f130be061b66ed7f1160b02f72e9054ff573ddc6baac76a4a13",
    "iscompressed": true,
    "account": "",
    "synchronized": true
   },
   {
     "address": "1VtTz3kJvcGhnMBefhayNpzkRHqj5oudKUoXeD",
     "ismine": true,
     "iswatchonly": false,
     "isscript": false,
     "pubkey": "0326b77627f8b708d60a252b0b596588244301e15ae03fc180857e4339e38b4d89",
     "iscompressed": true,
     "account": "",
     "synchronized": true
   }
 ],
}
```
## 9. Validate address

To get information about the validity of an address, including whether this node has the address's private key in its wallet, use `post /api/v1/validate_address` and pass this parameter:
```
{
  "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
}
```
The output will be:

```
{
 "status": 200,
 "primechain_address": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
 "isvalid": true,
 "ismine": true
}
```

## 10. List entities
To get a list of entities in this node's wallet, use `get /api/v1/list_entities`
```
{
  "status": 200,
  "primechain_address": 
    [
     "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
     "1af89TzR7d7N3pqtKrfzQFxz9MYuNvpt2iFBmj",
     "1B14GaGb9KQYy7poHQA4JvrzgRmLs6QFyX4dw6",
     "14gtREapQns3DtYqiS6pke3sShgDmLxVQP6ZeS",
     "1ZYxMuEUjMMaSvCPtS8i4UuLvDu57GrPGQVH7b",
     "13ep2rhnTGiJXCNfqCiqJxw8NoCzN4eKYinSuN",
     "1FWGDnR9evbf4HQNKfeKeYKxRagwckH4Kemsxs",
     "18ZmXBoXpyAUJyGMPJuSK6jxMSvZaqto8E1PzK",
     "1F3Kftk57XJeQsF4jQqURidqZZcQY7UbVMtMcz",
     "1DxwNEoAwyeQszLptyYGJyEN413mzEn4MV9eSR",
     "1E8HozfDmmzemad8TbmL8MnPVpc5TnSEpRzNRD",
     "1C6ecGod2vqP85w8SRW1nquqn8HiynL9jjYzuP",
     "1X3GYYdmtrdZvv99HACeFMNre26w1EiVxNqrJ7",
     "1Xnvg8LsdHJfruJhcQcxrorjmgLEe5sBb9evkr",
     "1Lh4NnTmU4HFx6uN2nkPfWtbNQNT1sqDuwSMcM",
     "1Miao2swgemhAjZNjmmjb3Tv8aGM9DifbxbBKX",
     "1JUoybWwFsYT16K1rpm35SY8tJ8Y3er7dkjZ5D",
     "15AnXVteaDaTb1wBstqxaXN2ixCEereugw7acE",
     "1VtTz3kJvcGhnMBefhayNpzkRHqj5oudKUoXeD"
    ],
}
```
