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
*  This may take 8 to 10 seconds.
* `from_address` is the entity that creates the asset. It must have `send` permission.
* `to_address` is the entity that receives the newly created asset. It must have `receive` permission. It must also have permissions to write to the ***ASSET_DATA_MASTERLIST***
*  The `from_address` and `to_address` can be the same.
*  `unit` refers to the fractions of the asset.
* `asset` refers to the name of the asset.
* `quantity` refers to the initial quantity of the asset.
* `code` refers to any arbitrary code or category.
* Setting `"open": "true"` will create an open asset - additional units of the asset CAN be issued in the future. 
* Setting `"open": "false"` will create a closed asset - additional units of the asset CANNOT be issued in the future. 

```
{
  "from_address": "1AdBvHHyknKcvUsYbQ9pPXMS2wd8oD9coY3gT7",
  "to_address": "1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk",
  "asset": 
  	{
    	"name": "AUTH-tokens",
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
"transaction_id": "ae963786b6866a03ece2d1d6086860d03d60d01682771bf437e3896ca4ce62a0",
"asset_ref": "107-265-45291",
"stream": "STREAM_107-265-45291"
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
  "asset_name": "INR-tokens"
}
```
![Details of a specified asset](http://www.primechaintech.com/img/api_documentation/asset_details.png)
```
{
"status": 200,
"response": 
  [
    {
      "name": "INR-tokens",
      "issuetxid": "ebb05ee44fcafce787e7e1d318f5a69846fa27458eeff1ec1317eb5e6fcd6dd2",
      "assetref": "107-265-45291",
      "multiple": 1,
      "units": 1,
      "open": true,
      "details": {},
      "issueqty": 20500,
      "issueraw": 20500,
      "subscribed": true,
      "synchronized": true,
      "transactions": 2,
      "confirmed": 2,
      "issues": 
        [
          {
            "txid": "ebb05ee44fcafce787e7e1d318f5a69846fa27458eeff1ec1317eb5e6fcd6dd2",
            "qty": 8500,
            "raw": 8500,
            "details": {},
            "issuers": 
              [
                "1FG92XaytZPWspbkVpVicJpQzeFPA78VbUkii3"
              ],
           },
          {
            "txid": "77d0cf12efb81084aa90b2db51dac46a72a579e8fb2f0f1956b32cd83f5930c5",
            "qty": 12000,
            "raw": 12000,
            "details": {},
            "issuers": 
              [
                "1FG92XaytZPWspbkVpVicJpQzeFPA78VbUkii3"
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

`entity_transaction_list`
