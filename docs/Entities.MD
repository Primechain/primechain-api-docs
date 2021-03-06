# Entity creation & permissions management

[1. Creating a new entity](#1-creating-a-new-entity)   
[2. Creating a new entity (for external key management)](#2-creating-a-new-entity-for-external-key-management)   
[3. Creating a new entity (with RSA keys)](#3-creating-a-new-entity-with-rsa-keys)   
[4. Create multisig address](#4-create-multisig-address)   
[5. Grant permissions to an entity](#5-grant-permissions-to-an-entity)   
[6. Revoke permissions to an entity](#6-revoke-permissions-to-an-entity)   
[7. List permissions given to a specific address](#7-list-permissions-given-to-a-specific-address)    
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
"response": {
"primechain_private_key": "VFGxBp56YTFwAkwtLn3rxKh4ah8JYRtKf2Kb3YkKyTqFnD1XdyWXmPX6",
"primechain_address": "1Zj8hJiAtR5UaZkrzWhsRwU1s6DYBQULeCx3Ro",
"primechain_public_key": "03b085ad524868aa32ba05109bf0448b188bfd3627fde1c91c127d938c07815879"
}
}
```

## 3. Creating a new entity (with RSA keys)
If you want to generate a blockchain key pair along with an RSA key pair, use `get /api/v1/create_entity_rsa`. The output will be the:
* primechain address
* primechain public key
* primechain private key
* RSA private key  
* RSA public key

```
{
"status": 200,
"response": {
"primechain_address": "18WiRzKsfmJEH6E3ESnrvgfcndAGwnFHrPnqRp",
"primechain_private_key": "VGFuvDqexth6GZPSkAXwZwEyQ9Y8LHFokUH2BwkcdvRPcGvF5HUy9euk",
"primechain_public_key": "035f3609b3ddb799946a6cbdf49820552ac9fed49ea10d954cdc4b1caf90cf88c4",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCUX/V0STFvx1Yh OEuCXVjqgPVZq4XxbBJj/P3/8vAsC498VyEgmy4rbWKS1+pSFt6ex8YDt1yZZroP N4Tg1I/jOk1YH/5rB7lmV+uv/g7WvE3FWEDRnDjbZBxClV4AhaZvOI5cR542BSii GfOVf4NqULMmjdVkdPxiJ8pl1mr9iy/LTC7gaD4RJ27kztNPUO+xsWoee5wtTlEv IUOKr/PwQIyBmu4uXXiVbVsNLlq7oFJ2yxHDcPVVI8klHRoiCjzwZvM05VY6xk5s DCysJ9EzpeBdwO84Qvqkr2I9NYLDFnr7yVYUYA72RcSbl+tPev1Oq7v0/qKlcJX5 XBajebzJAgMBAAECggEATqz/W3UAONRLUHwoVe0nm9lbv/uan6R9r/VTvidUwRY0 NGuDDmYauj5bWaASCQtFao5l6kyNVm5JVI5M8GbmEUg2APeeEaTb42/VctHVjnn1 ByK/5CXhZDwWXBwV51L3KNylaDs1olFj9WirZ+dgiLxX8qacs5LwzR9qTEvBGcWn CSgD1Yw60nQS9Y7NXkV0GHhSp7YXa+lXnG6cMEYqqxHD9GTD2p/SaoPf4t0ajobE 6ZH9UfbapRUPATTF5X0S+UqPfNUthCOvzSzX/bfrBECpwAAB4TWeinqJA3EpYw/j 9sbTGBenxZwhxIEs0On4WM3dV8HZJv+tSwo05ZpG7QKBgQDcTGijkH4R9bYE50OQ DLEdCmAE2gdJpxG0bEGFuF+AmuRT2mtmapMlsAx6udDuckUbRMbjqC9UjnxXqeEI dyuqf2SDDt3JhD23/Gk/qylld95w1LMueZY+SwYrWvjyydJE8sVjj78Kc6X2vuAB uDyB6geg+kVVcd1QyRgqmh4crwKBgQCsa6HGP7rJeDDCyKzL5aw0HZKJ0DW2O4hp asJjVHWDRfInzAGn9jXa62b5EoI1jCApNBoRPn1vCVq0K4z9zCypt66A62wrNIKI W/34NFkEtYMpQJE2Y6uYgrNGDy3yuPuNnOkl8/TQlJmEf/ykMEJepIBYq759BvTa zuVivM1MBwKBgQCPt91wD7zfdKAptMIUAOOvIWyg3ahxeWgIf7ODTFQpr2MT/WOh rhePN7n8eqr+VFgXQRhLvxYZoNcnzbD8d9pp4bAt/A3fAMHO/QGgwsY/5yKcE3dN 84571zAQKspMgjQGPSdfG5EzfV0hi0bSeGIpEwelEoEXDDCpGngEmwTYCwKBgQCU ZSpd6znC7mvhKT/3WRvl2tHlRMsFpaVZPWZCgU2GhyvMbru6KKDfYx1EH1br6UdA zzPkRYlFiKKFULpPMWv7Qjixgm2dndr+q1YhSkSXVfWmCokwa4Yjg9Hx6Vyde/Id RsAvRxEcd9jM/i6dzV9B/4jrSB1xlAwnSkyIt4Bl/wKBgEzqce+tYkn6NxbVcRiQ W6D/UXj1kP9HWYFnI4xWj5Zp9H54yuhZ//gzAf4qB9XYnrOHy3t3mu08/Yrg9F14 +YBHwQD8Gu3qTpw9vFfKXgJs2J8zt/0ePmgg+5rOho833WkKU0qJxhTSu5RcqYFp rYQDaP11oooPIHZr/yHMRI2/ -----END PRIVATE KEY-----",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlF/1dEkxb8dWIThLgl1Y 6oD1WauF8WwSY/z9//LwLAuPfFchIJsuK21iktfqUhbensfGA7dcmWa6DzeE4NSP 4zpNWB/+awe5Zlfrr/4O1rxNxVhA0Zw422QcQpVeAIWmbziOXEeeNgUoohnzlX+D alCzJo3VZHT8YifKZdZq/Ysvy0wu4Gg+ESdu5M7TT1DvsbFqHnucLU5RLyFDiq/z 8ECMgZruLl14lW1bDS5au6BSdssRw3D1VSPJJR0aIgo88GbzNOVWOsZObAwsrCfR M6XgXcDvOEL6pK9iPTWCwxZ6+8lWFGAO9kXEm5frT3r9Tqu79P6ipXCV+VwWo3m8 yQIDAQAB -----END PUBLIC KEY-----"
}
}
```

## 4. Create multisig address
To create a pay-to-scripthash (P2SH) multisig address and add it to the wallet, use `post /api/v1/create_multisig_address`. Funds sent to this address can only be spent by transactions signed by `nrequired` of the specified keys.

Note: The keys used here should have been created using `post /api/v1/create_keypair` or `post /api/v1/create_entity_rsa`

Sample input creating a multisig addresss where 2 out of the provided 3 keys need to be used.
```
{
  "nrequired": 2,
  "primechain_public_key": [
    "02f168e48c0fab361036eb7b7cd39d0f54f5c0450fc573e116900d8c6656a14a7f",
    "03d7997c08cdc430038c2481e1d2cf7db7b964ecd3410128486a1ac896d78c0e88",
    "03ff4dcf31b5b2469bd6332789007e76aac6950c7d99a1c9cb4c6e09b75f181c15"
  ]
}
```
Sample output
```
{
"status": 200,
"primechain_address": "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM"
}
```
Note: You should give send, receive permission to all 4 addresses (the multisig as well as the 3 used to create the multisig.)


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
  "primechain_address": "1VCeqGYXLaqMtAFtxTNeTzfW8T714us2t3uwYM",
  "permission": "send,receive"
}
```
The output will be the transaction id of the transaction in which the permissions were granted.
```
{
"status": 200,
"tx_id": "e39330efc1594e062a1047074231ce97f65f4d71dbf745576bba81504afba923"
}
```
***Note:*** Permissions can be revoked using `revoke_permission.`

## 6. Revoke permissions to an entity
Use `post /api/v1/revoke_permissions` to revoke the specified permissions from the specified address.
```
{
  "primechain_address": "1VCeqGYXLaqMtAFtxTNeTzfW8T714us2t3uwYM",
  "permission": "send"
}
```
The output will be the txid of the transaction in which the permissions were revoked.
```
{
"status": 200,
"tx_id": "989515694062a199f33770eeda617d631b4faafc8cc8a9048662d053e2516192"
}
```

## 7. List permissions given to a specific address
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
  "primechain_address": "1Qr572HfZyxmburpA6fQY4Nu2k7uWVR5dwwBoe"
}
```
The output will be:

```
{
"status": 200,
"response": {
"isvalid": true,
"primechain_address": "1Qr572HfZyxmburpA6fQY4Nu2k7uWVR5dwwBoe",
"ismine": true,
"iswatchonly": false,
"isscript": false,
"pubkey": "02fc0cbee9f8a649d21628f2c4640d5ce33c115cea64c265db2612e0c3b31dfb26",
"iscompressed": true,
"account": "",
"synchronized": true
}
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
