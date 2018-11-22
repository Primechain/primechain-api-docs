# Entities

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
* private key 
* blockchain address. 

 The output will be the blockchain address of the newly created signer.
```
{
"status": 200,
"primechain_address": "15AnXVteaDaTb1wBstqxaXN2ixCEereugw7acE"
}
```
The private key is automatically stored in your node. This will not be visible to other nodes. If you don't want the private key stored in the node, use `get /api/v1/create_keypair`. 

## 2. Creating a new entity (for external key management)
If you want to generate a public/private key pair, which is not stored in the wallet and which is ready for external key management use `get /api/v1/create_keypair`. The output will be the primechain address, public key and private key of the newly created signer.

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
If you want to generate a public/private key pair along with an RSA key pair, use `get /api/v1/create_entity_rsa`. The output will be the:
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
  "nrequired": 1,
  "primary_address": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
  "secondary_address": "1f2N8o6MmK1rTvf6kZKxWiCMZ84wFLWhdD2V5"  
}
```
Each key can be a full public key, or an address if the corresponding key is in the node's wallet. Output is the P2SH multisig address.
```
{
"status": 200,
"address": "47m73n8bFqbjxJiTXvNpKNekKjsQG2yf6g5B1p",
"redeem_script": "51210266f1068c2cd4681af9c60ca502d9cbea34bcc33a697cbe443df63d79214a011d21034cc36b3b86e632bc23e5aa7e0f28e159baee469feb43d1e4227b6706f27aedd852ae"
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
  "address": "15p7mPvCBGKPDmGAvUX8CJH7QUPx65QFxQMfqT",
  "permission": "connect,send,receive,issue,create,activate,admin"
}
```
![Grant permissions to an entity](http://www.primechaintech.com/img/api_documentation/grant_permissions.png)
The output will be the txid of the transaction in which the permissions were granted.
```
{
"status": 200,
"transaction_id": "049bc8fd6468c547c282740659415b9b2cd14ecba9f0eb3bd05367d3041d8063"
}
```
***Note:*** Permissions can be revoked using `revoke_permission.`

## 6. Revoke permissions to an entity
Use `post /api/v1/revoke_permissions` to revoke the specified permissions from the specified address.
```
{
  "address": "15p7mPvCBGKPDmGAvUX8CJH7QUPx65QFxQMfqT ",
  "permission": "send,connect"
}
```
![Revoke permissions to an entity](http://www.primechaintech.com/img/api_documentation/revoke_permissions.png)
The output will be the txid of the transaction in which the permissions were revoked.
```
{
"status": 200,
"transaction_id": "5c1c23f55d145537970288fc194d01fe96f1d3aa41e8f1e0bdc468137df0c745"
}
```

## 7. List permissions given to all entities
To get a list of all permissions which have been explicitly granted to all entities, use `get /api/v1/listpermissions`. 
![List permissions given to all entities](http://www.primechaintech.com/img/api_documentation/listpermissions.png)
```
{
"address": [
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "mine",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "admin",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "activate",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "connect",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "send",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "receive",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "issue",
"startblock": 0,
"endblock": 4294967295
},
  {
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
"for": null,
"type": "create",
"startblock": 0,
"endblock": 4294967295
}
],
}
```

## 8. Information about the addresses in the wallet

To get information about the addresses in the wallet, use `get /api/v1/listaddresses`. 
![Information about the addresses in the wallet](http://www.primechaintech.com/img/api_documentation/listaddresses.png)
```
{
  "addresses": 
    [
      {
        "address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
        "ismine": true,
        "iswatchonly": false,
        "isscript": false,
        "pubkey": "023da6a7af2a23a83dfea12d91352b39c2c20c6832fe58742db7db380e658d27c6",
        "iscompressed": true,
        "account": "",
        "synchronized": true
      },
      {
        "address": "15p7mPvCBGKPDmGAvUX8CJH7QUPx65QFxQMfqT",
        "ismine": true,
        "iswatchonly": false,
        "isscript": false,
        "pubkey": "03509cdeb36d15287eeaa6af6bac26e468fe063855778bfbc9d8049bd9fe3d22d1",
        "iscompressed": true,
        "account": "",
        "synchronized": true
      }
    ],
}
```
## 9. Validate address

To get information about the validity of an address, including whether this node has the address's private key in its wallet, use `post /api/v1/validate_address`
![Validate address](http://www.primechaintech.com/img/api_documentation/validate_address.png)
```
{
"status": 200,
"address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
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
