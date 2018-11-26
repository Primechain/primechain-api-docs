# Smart Asset Lifecycle Management

A blockchain smart asset can be the digital representation of a real-world asset (e.g. gold, equity shares, fiat currency, stressed asset) or an asset in itself (e.g. bitcoin and other crypto-currencies). The blockchain removes the characteristic of infinite reproducibility from a digital asset. It confirms that each unit of value was transferred only once, solving the long-standing problem of double spending. A blockchain can assign title rights because it provides a record that compels offer and acceptance. 

[1. Create a new asset](#1-create-a-new-asset)   
[2. Create additional units of an open asset](#2-create-additional-units-of-an-open-asset)   
[3. Details of a specified asset](#3-details-of-a-specified-asset)   
[4. Balances of all assets](#4-balances-of-all-assets)   
[5. Assets held by specified entities](#5-assets-held-by-specified-entities)   
[6. Transfer asset](#6-transfer-asset)    
[7. Transactions by a specified entity](#7-transactions-by-a-specified-entity)    

## 1. Create a new asset
To create a new smart asset, use `post /api/v1/create_new_asset_from`.

***Note:***
*  This may take upto 30 seconds.   
* `from_address` is the entity that creates the asset. It must have `send`, `receive` and `issue` permissions. It must also have permissions to write to the ***ASSET_DATA_MASTERLIST***   
* `to_address` is the entity that receives the newly created asset. It must have `receive` permission and ideally also `send` permission.   
*  The `from_address` and `to_address` can be the same.
*  `unit` refers to the minimum divisible quantity of the asset.
* `asset` refers to the name of the asset.
* `quantity` refers to the initial quantity of the asset.
* `details` refers to any details about the asset.
* Setting `"open": "true"` will create an open asset - additional units of the asset CAN be issued in the future. 
* Setting `"open": "false"` will create a closed asset - additional units of the asset CANNOT be issued in the future. 

```
{
  "from_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "to_address": "17Sonz7gM3ha6PvqZhRwKT7PUjA2H4TuKuRqF5",
  "asset": 
  	{
    	"name": "AUTH-tokens-series-K",
    	"open": true
  	},
  "unit": 1,
  "quantity": 17430,
  "details": "These are the details of this asset." 
}
```
***Output is:***
* the txid of the transaction in which the asset was created.
* the reference number of the asset.
* the newly created data stream specifically for writing data relating to this asset. The `to_address` is granted write permissions to this stream. 
```
{
  "status": 200,
  "transaction_id": "a922dce10c6f3690c11ab2526b24d59aee643fd248501c37be9a38d9bacd058a",
  "asset_ref": "836-266-28088",
  "description": 
    {
      "details": "These are the details of this asset."
    }
}
```

## 2. Create additional units of an open asset

To create additional units of an open asset, use `post /api/v1/asset_create_more_from`.

***Note:***
* `from_address` is the entity that creates the asset. It must have `send` permission.
* `to_address` is the entity that receives the newly created asset. It must have `receive` permission.
* The `from_address` and `to_address` can be the same.
* `asset_name` refers to the name of the asset.
* `quantity` refers to the additional quantity of the asset being issued.
```
{
  "from_address": "1AdBvHHyknKcvUsYbQ9pPXMS2wd8oD9coY3gT7",
  "to_address": "1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk",
  "asset_name": "AUTH-tokens",
  "quantity": 350
}
```
```
{
"status": 200,
"transaction_id": "d755b1b97a4acb5ce53618fb724e2a3f6db1ad6ebe3a19c86175e81573db3ab5"
}
```
Output is the txid of the transaction in which the additional units were created.

## 3. Details of a specified asset
To get details of a specific asset, use `post /api/v1/asset_details` and pass the asset name or referece id as a parameter.
```
{
  "asset_name": "107-265-45291"
}
```
```
{
  "asset_name": "AUTH-tokens-series-A"
}
```
```
{
"status": 200,
"response": [
  {
"name": "AUTH-tokens-series-A",
"issuetxid": "2eaea9d94fdc908b68a12f7d5c642513f53c8c7d1d507116b42f00a1ff0d68e7",
"assetref": "622-267-44590",
"multiple": 1,
"units": 1,
"open": true,
"details": {
"details": "These are the details of this asset."
},
"issueqty": 17430,
"issueraw": 17430,
"subscribed": true,
"synchronized": true,
"transactions": 2,
"confirmed": 2,
"issues": [
  {
"txid": "2eaea9d94fdc908b68a12f7d5c642513f53c8c7d1d507116b42f00a1ff0d68e7",
"qty": 17430,
"raw": 17430,
"details": {
"details": "These are the details of this asset."
},
"issuers": [
  "1AdBvHHyknKcvUsYbQ9pPXMS2wd8oD9coY3gT7"
],
}
],
}
],
}
```

## 4. Balances of all assets
To get the name, asset ref and balance of all assets, use `get /api/v1/asset_balances`

```
{
"status": 200,
"asset_balance": [
  {
"name": "Gold",
"assetref": "277-267-37184",
"qty": 13000
},
  {
"name": "AUTH-tokens-series-A",
"assetref": "622-267-44590",
"qty": 17430
},
  {
"name": "Silver",
"assetref": "299-267-41329",
"qty": 10000000000000
},
  {
"name": "AUTH-tokens",
"assetref": "595-266-8935",
"qty": 17430
}
],
}
```

## 5. Assets held by specified entities
Use  `assets_held_by_entity` to get details of Assets held by specified entities
```
{
  "address": "1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk"
}
```
```
{
"status": 200,
"response": {
"1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "622-267-44590",
"qty": 17430
},
  {
"name": "AUTH-tokens-series-B",
"assetref": "633-267-11748",
"qty": 17430
},
  {
"name": "AUTH-tokens",
"assetref": "595-266-8935",
"qty": 17430
}
],
"total": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "622-267-44590",
"qty": 17430
},
  {
"name": "AUTH-tokens-series-B",
"assetref": "633-267-11748",
"qty": 17430
},
  {
"name": "AUTH-tokens",
"assetref": "595-266-8935",
"qty": 17430
}
],
}
}
```
You can also enter multiple addresses:
```
{
   "address":
  		[
  			"1AdBvHHyknKcvUsYbQ9pPXMS2wd8oD9coY3gT7",
  			"1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk"
  		]
}
```
```
{
"status": 200,
"response": {
"1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "622-267-44590",
"qty": 17430
},
  {
"name": "AUTH-tokens-series-B",
"assetref": "633-267-11748",
"qty": 17430
},
  {
"name": "AUTH-tokens",
"assetref": "595-266-8935",
"qty": 17430
}
],
"1AdBvHHyknKcvUsYbQ9pPXMS2wd8oD9coY3gT7": [],
"total": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "622-267-44590",
"qty": 17430
},
  {
"name": "AUTH-tokens-series-B",
"assetref": "633-267-11748",
"qty": 17430
},
  {
"name": "AUTH-tokens",
"assetref": "595-266-8935",
"qty": 17430
}
],
}
}
```

## 6. Transfer asset
To send assets from one entity to another use `send_asset_from` and pass 4 parameters - `from_address`, `to_address`, `asset_name`, `quantity` and `details`
```
{
  "from_address": "1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk",
  "to_address": "17eC7qETgYmdHwwT8b2CKBdbT6MxTosGYVYjHU",
  "asset_name": "622-267-44590",
  "quantity": 4,
  "details": "These are the details of this transfer"
}
```
```
{
"status": 200,
"transaction_id": "925b18653decdc04544e0f570bbdce7eabf8945dc360f6b7f42ed2a5a02a1185"
}
```
The output is the txid of the transaction in which the asset was transferred.

## 7. Transactions by a specified entity

To list information about the transactions related to an address in this node’s wallet, including how they affected that address’s balance. use `entity_transaction_list` and pass the address as a parameter.

```
{
  "primechain_address": "17Sonz7gM3ha6PvqZhRwKT7PUjA2H4TuKuRqF5"
}
```

```
{
"status": 200,
"entity_transaction_list": [
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "17Sonz7gM3ha6PvqZhRwKT7PUjA2H4TuKuRqF5"
],
"addresses": [
  "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3"
],
"permissions": [
  {
"for": null,
"connect": false,
"send": true,
"receive": true,
"create": false,
"issue": false,
"mine": false,
"admin": false,
"activate": false,
"startblock": 0,
"endblock": 4294967295,
"timestamp": 1543234253,
"addresses": [
  "17Sonz7gM3ha6PvqZhRwKT7PUjA2H4TuKuRqF5"
],
}
],
"items": [],
"data": [],
"confirmations": 102,
"blockhash": "0d69963b68d1e50c524daa9bf9924de6ace08fb52b8287020df4bc40c2fce3a0",
"blockindex": 1,
"blocktime": 1543234262,
"txid": "3349d33772f690b16bd54bd51ce4ba6404dad9882395309198b2091bd5e0c3c4",
"valid": true,
"time": 1543234253,
"timereceived": 1543234253
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "AUTH-tokens-series-K",
"assetref": "836-266-28088",
"qty": 17430
}
],
},
"myaddresses": [
  "17Sonz7gM3ha6PvqZhRwKT7PUjA2H4TuKuRqF5"
],
"addresses": [
  "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9"
],
"permissions": [],
"issue": {
"name": "AUTH-tokens-series-K",
"assetref": "836-266-28088",
"multiple": 1,
"units": 1,
"open": true,
"details": {
"details": "These are the details of this asset."
},
"qty": 17430,
"raw": 17430,
"addresses": [
  "17Sonz7gM3ha6PvqZhRwKT7PUjA2H4TuKuRqF5"
],
},
"items": [],
"data": [],
"confirmations": 91,
"blockhash": "06d4ce7fdbdb787ab294bcd781dd498e32426d7e67c0e705ce26acf62b4ce25f",
"blockindex": 1,
"blocktime": 1543234386,
"txid": "b86d0c4896a06984104b2d75d7be9030b8fd1c44dab90d015e094f3e5ea660a8",
"valid": true,
"time": 1543234375,
"timereceived": 1543234375
}
],
}
```
