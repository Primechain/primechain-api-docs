# Smart Asset Lifecycle Management

A blockchain smart asset can be the digital representation of a real-world asset (e.g. gold, equity shares, fiat currency, stressed asset) or an asset in itself (e.g. bitcoin and other crypto-currencies). The blockchain removes the characteristic of infinite reproducibility from a digital asset. It confirms that each unit of value was transferred only once, solving the long-standing problem of double spending. A blockchain can assign title rights because it provides a record that compels offer and acceptance. 

[1. Create a new asset](#1-create-a-new-asset)   
[2. Create additional units of an open asset](#2-create-additional-units-of-an-open-asset)   
[3. Details of a specified asset](#3-details-of-a-specified-asset)   
[4. Balances of all assets](#4-balances-of-all-assets)   
[5. Assets held by specified entities](#5-assets-held-by-specified-entities)   
[6. Transfer asset when private key is in the node](#6-transfer-asset-when-private-key-is-in-the-node)    
[7. Transfer asset from multisig address](#7-transfer-asset-from-multisig-address)    
[8. Transfer asset when private key is not in the node](#8-transfer-asset-when-private-key-is-not-in-the-node)
[9. Transactions by a specified entity](#9-transactions-by-a-specified-entity)    

## 1. Create a new asset
To create a new smart asset, use `post /api/v1/create_asset`.

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
  "from_address": "1K2MYAXp1tiMEKw2VKMrzy8X9peZFrrUbvZnXK",
  "to_address": "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM",
  "asset": 
  	{
    	"name": "SILVER-tokens-series-A",
    	"open": false
  	},
  "unit": 1,
  "quantity": 19500,
  "details": "Backed by silver jewellery held in Lot A at Zimblia office" 
}

```
***Output is:***
* the txid of the transaction in which the asset was created.
* the reference number of the asset.
* the newly created data stream specifically for writing data relating to this asset. The `to_address` is granted write permissions to this stream. 
```
{
"status": 200,
"tx_id": "00897558db1f7d2b4682ca79afd1830d5066266bc0118bbe87c7e2ff3a9cc5e1",
"asset_ref": "1074-267-61526",
"description": {
"details": "Backed by silver jewellery held in Lot A at Zimblia office"
}
}
```

## 2. Create additional units of an open asset

To create additional units of an open asset, use `post /api/v1/create_more_asset`.

***Note:***
* `from_address` is the entity that creates the asset. It must have `send` permission.
* `to_address` is the entity that receives the newly created asset. It must have `receive` permission.
* The `from_address` and `to_address` can be the same.
* `asset_name` refers to the name of the asset.
* `quantity` refers to the additional quantity of the asset being issued.
```
{
  "from_address": "1K2MYAXp1tiMEKw2VKMrzy8X9peZFrrUbvZnXK",
  "to_address": "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM",
  "asset_name": "SILVER-tokens-series-B",
  "quantity": 5000
}
```
```
{
"status": 200,
"tx_id": "c749efc4cca56b72749e8e2d0acf7bf6282383255482894c578e4c82869fbc4f"
}
```
Output is the id of the transaction in which the additional units were created.

## 3. Details of a specified asset
To get details of a specific asset, use `post /api/v1/asset_details` and pass the asset name or referece id as a parameter.
```
{
  "asset_name": "AUTH-tokens-series-A"
}
```
Output:
```
{
  "status": 200,
  "response": 
  [
    {
      "name": "AUTH-tokens-series-A",
      "issuetxid": "d7621cb45b226a4bbf86bde4eb0b7fe700ebfc000f8bb12450362746777dbe44",
      "assetref": "324-267-25303",
      "multiple": 1,
      "units": 1,
      "open": true,
      "details": {
      "details": "These are AUTH tokens"
    },
      "issueqty": 45350,
      "issueraw": 45350,
      "subscribed": true,
      "synchronized": true,
      "transactions": 2,
      "confirmed": 2,
      "issues": 
        [
          {
            "txid": "d7621cb45b226a4bbf86bde4eb0b7fe700ebfc000f8bb12450362746777dbe44",
            "qty": 45000,
            "raw": 45000,
            "details": 
              {
                "details": "These are AUTH tokens"
              },
            "issuers": 
              [
                "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
              ],
            },
          {
            "txid": "0ac10e7cc5d1a3bdd959f74034fabaae7e40ec5e4515aba4c57002e6e50b9736",
            "qty": 350,
            "raw": 350,
            "details": {},
            "issuers": 
              [
                "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
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
  "asset_balance": 
    [
      {
        "name": "AUTH-tokens-series-A",
        "assetref": "324-267-25303",
        "qty": 45350
       },
       {
        "name": "GOLD-tokens-series-A",
        "assetref": "301-267-14695",
        "qty": 19500
        }
    ],
}
```

## 5. Assets held by specified entities
Use  `post /api/v1/assets_held_by_entity` to get details of Assets held by specified entities
```
{
  "primechain_address": "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM"
}
```
```
{
"status": 200,
"response": {
"4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM": [
  {
"name": "SILVER-tokens-series-A",
"assetref": "1074-267-61526",
"qty": 19500
},
  {
"name": "SILVER-tokens-series-B",
"assetref": "1086-266-919",
"qty": 33500
}
],
"total": [
  {
"name": "SILVER-tokens-series-A",
"assetref": "1074-267-61526",
"qty": 19500
},
  {
"name": "SILVER-tokens-series-B",
"assetref": "1086-266-919",
"qty": 33500
}
],
}
}
```
You can also enter multiple addresses:
```
{
  "primechain_address":
  	[
  		"1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  		"16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
  	]
}
```
Output
```
{
"status": 200,
"response": {
"1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "324-267-25303",
"qty": 45350
},
  {
"name": "GOLD-tokens-series-A",
"assetref": "301-267-14695",
"qty": 19460
}
],
"16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd": [
  {
"name": "GOLD-tokens-series-A",
"assetref": "301-267-14695",
"qty": 40
}
],
"total": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "324-267-25303",
"qty": 45350
},
  {
"name": "GOLD-tokens-series-A",
"assetref": "301-267-14695",
"qty": 19500
}
],
}
}
```

## 6. Transfer asset when private key is in the node
To send assets when the sender's private key is in the node, use `post /api/v1/send_asset` and pass 5 parameters - 
1. Sender's address
2. Receiver's address
3. Asset name or reference
4. Asset quantity
5. Details of the transaction
```
{
  "from_address": "1K2MYAXp1tiMEKw2VKMrzy8X9peZFrrUbvZnXK",
  "to_address": "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM",
  "asset_name": "SILVER-tokens-series-A",
  "quantity": 12,
  "details": "These are the details of this transfer"
}
```
```
{
"status": 200,
"tx_id": "79e44ffa6e8b611ee7750f8a41bb16e44e628c9ef48c4c55ba15314a2c574428"
}
```
The output is the id of the transaction in which the asset was transferred.

## 7. Transfer asset from multisig address
To send assets from a multisig address, use `post /api/v1/transfer_multisign_asset` and pass 5 parameters:
1. Sender's address
2. Receiver's address
3. Asset name or reference
4. Asset quantity
5. Senders' private keys (of minimum required signers)

Sample input
```
{
  "senders_address": "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM",
  "receivers_address": "1GkxHWs76J2SbyZtq68NUuCMuBc48eERkcukFN",
  "asset_name": "SILVER-tokens-series-A",
  "asset_quantity": 175,
  "senders_private_key": [
    "VGEnfWgmCLCMjU2ao9tAp3JxX9eK2ahMMiUevqLUN1A9HwFPA5hB5sDH",
    "VHRLz6v1VypfTWpqNxAnhVhxNFG77K2XpVgtdNf3PwypovVX14TZrNjA"
  ]
}
```
Sample output
```
{
"status": 200,
"tx_id": "3f48baa90aba1b01e2fa857a965170a904e0ec657745c5b501f05d7bcad37176"
}
```

## 8. Transfer asset when private key is not in the node
To send assets when the sender's private key is not in the node, use `post /api/v1//transfer_asset` and pass 5 parameters:
1. Sender's address
2. Receiver's address
3. Asset name or reference
4. Asset quantity
5. Senders' private key

Sample input
```
{
  "senders_address": "1GkxHWs76J2SbyZtq68NUuCMuBc48eERkcukFN",
  "receivers_address": "1K2MYAXp1tiMEKw2VKMrzy8X9peZFrrUbvZnXK",
  "asset_name": "SILVER-tokens-series-A",
  "asset_quantity": 8,
  "senders_private_key": "V9ckYDSE8TX7T1Mzm9nGbBteC5kLBFdFZdFYWZp6qcLyPnjhcsszZScc"
}
```
Sample output
```
{
"status": 200,
"tx_id": "42dc57c7068b84bf126a6ed340f3d8696dbbd7b417ff314609e8ed041d2755ad"
}
```

## 9. Transactions by a specified entity

To list information about the transactions related to an address in this node’s wallet, including how they affected that address’s balance. use `post /api/v1/entity_transaction_list` and pass the address as a parameter.

```
{
  "primechain_address": "1GkxHWs76J2SbyZtq68NUuCMuBc48eERkcukFN"
}
```

```
{
"status": 200,
"entity_transaction_list": [
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "SILVER-tokens-series-A",
"assetref": "1074-267-61526",
"qty": 175
}
],
},
"myaddresses": [
  "1GkxHWs76J2SbyZtq68NUuCMuBc48eERkcukFN"
],
"addresses": [
  "4NM46pESGpnvCn8pJmVZpuFepaeUkwKF3YecSM"
],
"permissions": [],
"items": [],
"data": [],
"confirmations": 30,
"blockhash": "02a120250ab453e59fee1fd6e5bfcb7bc4e0ed58ac9c333770f8c1edafe4e793",
"blockindex": 1,
"blocktime": 1546418902,
"txid": "3f48baa90aba1b01e2fa857a965170a904e0ec657745c5b501f05d7bcad37176",
"valid": true,
"time": 1546418892,
"timereceived": 1546418892
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "SILVER-tokens-series-A",
"assetref": "1074-267-61526",
"qty": -8
}
],
},
"myaddresses": [
  "1GkxHWs76J2SbyZtq68NUuCMuBc48eERkcukFN"
],
"addresses": [
  "1K2MYAXp1tiMEKw2VKMrzy8X9peZFrrUbvZnXK"
],
"permissions": [],
"items": [],
"data": [],
"confirmations": 6,
"blockhash": "08907aeee46289a6db18c96371e309030b96c3b55f2f2c9f98cbcf3232d48863",
"blockindex": 1,
"blocktime": 1546419624,
"txid": "42dc57c7068b84bf126a6ed340f3d8696dbbd7b417ff314609e8ed041d2755ad",
"valid": true,
"time": 1546419613,
"timereceived": 1546419613
}
],
}
```
