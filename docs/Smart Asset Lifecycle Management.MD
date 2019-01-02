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

## 6. Transfer asset
To send assets from one entity to another use `post /api/v1/send_asset_from` and pass 4 parameters - `from_address`, `to_address`, `asset_name`, `quantity` and `details`
```
{
  "from_address": "aaaa",
  "to_address": "aaaa",
  "asset_name": "aaaa",
  "quantity": aaaa,
  "details": "These are the details of this transfer"
}
```
```
{
  "status": 200,
  "tx_id": "aaaa"
}
```
The output is the id of the transaction in which the asset was transferred.


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

## 7. Transactions by a specified entity

To list information about the transactions related to an address in this node’s wallet, including how they affected that address’s balance. use `post /api/v1/entity_transaction_list` and pass the address as a parameter.

```
{
  "primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
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
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [
  "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt"
],
"permissions": [
  {
"for": {
"type": "stream",
"name": "DATA_SIGNATURE_MASTERLIST",
"streamref": "3-2122-40622"
},
"write": true,
"admin": false,
"activate": false,
"startblock": 0,
"endblock": 4294967295,
"timestamp": 1544432770,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
}
],
"items": [],
"data": [],
"confirmations": 423,
"blockhash": "01b402956cfd8484cf5ecd54465887060f695401bf011f168a02c5f9dd12be88",
"blockindex": 1,
"blocktime": 1544432770,
"txid": "c33f40019300b58fd230b104591d0dece808a0a1f6c712c46dd500cd776da989",
"valid": true,
"time": 1544432770,
"timereceived": 1544432770
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [
  "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt"
],
"permissions": [
  {
"for": {
"type": "stream",
"name": "DATA_MASTERLIST",
"streamref": "3-2392-21701"
},
"write": true,
"admin": false,
"activate": false,
"startblock": 0,
"endblock": 4294967295,
"timestamp": 1544432776,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
}
],
"items": [],
"data": [],
"confirmations": 422,
"blockhash": "0f4d459e7ed184e9366e7c4db497ab1932ec4dbb7e2c07abb8bdc86c6bbead06",
"blockindex": 1,
"blocktime": 1544432785,
"txid": "76726550fb12165b53f39230ee07a907b2166b459d4b7a01a6ff74c56bcb3f71",
"valid": true,
"time": 1544432777,
"timereceived": 1544432777
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [
  "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt"
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
"timestamp": 1544432782,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
}
],
"items": [],
"data": [],
"confirmations": 422,
"blockhash": "0f4d459e7ed184e9366e7c4db497ab1932ec4dbb7e2c07abb8bdc86c6bbead06",
"blockindex": 2,
"blocktime": 1544432785,
"txid": "7ed60088d7d2750703f5758b48f3bc484c8b606f261ff7a944cdf33245b810f0",
"valid": true,
"time": 1544432783,
"timereceived": 1544432783
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [
  {
"type": "stream",
"name": "DATA_SIGNATURE_MASTERLIST",
"streamref": "3-2122-40622",
"publishers": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"key": "80CNwZ37W3HU7/FlLziCr9pqD4q+s0jovp4cew88Xkw9+iHRENKARL1Zq5W37q+ZagFXZ4n6bbSP2QxSZLh38g==",
"data": "7b2261646472657373223a223136483657644452374c70487a5665456b6454694536644e695048426e6950746e7854596464222c2266696c655f68617368223a223830434e775a333757334855372f466c4c7a6943723970714434712b73306a6f7670346365773838586b77392b694852454e4b41524c315a7135573337712b5a616746585a346e3662625350325178535a4c683338673d3d222c227369676e6174757265223a224879493444325738523668714d516c6544455772533073744e6b34393359704552706d34704d45534b3842424b59476e4d6b59784d6945422f6873482f5569754c48476f546d6f52325a2f7651427073417149766849773d227d"
}
],
"data": [
  "7b2261646472657373223a223136483657644452374c70487a5665456b6454694536644e695048426e6950746e7854596464222c2266696c655f68617368223a223830434e775a333757334855372f466c4c7a6943723970714434712b73306a6f7670346365773838586b77392b694852454e4b41524c315a7135573337712b5a616746585a346e3662625350325178535a4c683338673d3d222c227369676e6174757265223a224879493444325738523668714d516c6544455772533073744e6b34393359704552706d34704d45534b3842424b59476e4d6b59784d6945422f6873482f5569754c48476f546d6f52325a2f7651427073417149766849773d227d"
],
"confirmations": 420,
"blockhash": "09583e36bd4c51cffea6db7c009e315db72a185f708101fa25f09bab1b74b9a9",
"blockindex": 1,
"blocktime": 1544432800,
"txid": "38dc4c1837b058c28bfccef45947d96716d9a1422abc5ce7bc88f45755941b2d",
"valid": true,
"time": 1544432793,
"timereceived": 1544432793
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [
  {
"type": "stream",
"name": "DATA_MASTERLIST",
"streamref": "3-2392-21701",
"publishers": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"key": "80CNwZ37W3HU7/FlLziCr9pqD4q+s0jovp4cew88Xkw9+iHRENKARL1Zq5W37q+ZagFXZ4n6bbSP2QxSZLh38g==",
"data": "7b22636f6e74656e74223a22613938663732373666393530623966343265343762626539636462333832363263613165386139336531646334393130623330343832326563613365653963623033626638666562653630633130366264363332306561386538343535313030343438326230613930663565333561326231663939393332323339663831626565363364346337376362326165636264363633343764313934656265323235333232303032363737666439383261363965396533633436656164646635346233343564663735373931373231346665343539626264323538323236616364363732383635346337313461323335653431633238666330666137623530626462363133343136393332636266626139653664666261613762303265306231663038363432366138376666326365633265303230346133386235386431333266313936666362366436353733396435306438646161336262306366363331373033653861336164633530363165373961333564376262613463393133656363316135633562333562333363323133336435666264376661653239323865636264613431663635663430643664633561343761393865626138396430623165376338613064343265616464386462396232323064393631393062313661666232333666643836373638333363646635333163343163643532636637623932393438363439636465636634313764613537633562373631623466386637383634383661376530313066613964393861393537306163336339613463663465376433643362613162653965396437613665386332323832643333343834663930343265376665333435363637646565646363636434333866346634373565363435643134636238326335353861363762643461356236613165346131336164653336666237363833336132373938323033616533396331363736393631303362633939393031363065323533306139613766336332396161396366366565663838656238313461653463656533616561646461353964343334303038666562616561316662343266376334623262346235316232373065333761633239386130646532396464653162336230663665653237383233636330643066222c22746167223a7b2274797065223a22427566666572222c2264617461223a5b36372c31322c3136322c3131332c32352c3136362c32342c36302c32362c3232312c35392c39372c33372c3132392c3138372c31335d7d7d"
}
],
"data": [
  "7b22636f6e74656e74223a22613938663732373666393530623966343265343762626539636462333832363263613165386139336531646334393130623330343832326563613365653963623033626638666562653630633130366264363332306561386538343535313030343438326230613930663565333561326231663939393332323339663831626565363364346337376362326165636264363633343764313934656265323235333232303032363737666439383261363965396533633436656164646635346233343564663735373931373231346665343539626264323538323236616364363732383635346337313461323335653431633238666330666137623530626462363133343136393332636266626139653664666261613762303265306231663038363432366138376666326365633265303230346133386235386431333266313936666362366436353733396435306438646161336262306366363331373033653861336164633530363165373961333564376262613463393133656363316135633562333562333363323133336435666264376661653239323865636264613431663635663430643664633561343761393865626138396430623165376338613064343265616464386462396232323064393631393062313661666232333666643836373638333363646635333163343163643532636637623932393438363439636465636634313764613537633562373631623466386637383634383661376530313066613964393861393537306163336339613463663465376433643362613162653965396437613665386332323832643333343834663930343265376665333435363637646565646363636434333866346634373565363435643134636238326335353861363762643461356236613165346131336164653336666237363833336132373938323033616533396331363736393631303362633939393031363065323533306139613766336332396161396366366565663838656238313461653463656533616561646461353964343334303038666562616561316662343266376334623262346235316232373065333761633239386130646532396464653162336230663665653237383233636330643066222c22746167223a7b2274797065223a22427566666572222c2264617461223a5b36372c31322c3136322c3131332c32352c3136362c32342c36302c32362c3232312c35392c39372c33372c3132392c3138372c31335d7d7d"
],
"confirmations": 420,
"blockhash": "09583e36bd4c51cffea6db7c009e315db72a185f708101fa25f09bab1b74b9a9",
"blockindex": 2,
"blocktime": 1544432800,
"txid": "9a6fa8fe940fb6cc36936ce18cc1fd13b1b9b16ab5de372c24330df624e51240",
"valid": true,
"time": 1544432793,
"timereceived": 1544432793
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [
  "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt"
],
"permissions": [
  {
"for": null,
"connect": false,
"send": true,
"receive": true,
"create": false,
"issue": true,
"mine": false,
"admin": false,
"activate": false,
"startblock": 0,
"endblock": 4294967295,
"timestamp": 1544511263,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
}
],
"items": [],
"data": [],
"confirmations": 281,
"blockhash": "06b5495d8d96393caf5afe7bb31d3d731cf775178194d108b2165770da165b95",
"blockindex": 1,
"blocktime": 1544511276,
"txid": "58b12bf136ccc29b06cfce570c5077eb6225e99b1ce810f2147ed847c74799d5",
"valid": true,
"time": 1544511263,
"timereceived": 1544511263
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "GOLD-tokens-series-A",
"assetref": "301-267-14695",
"qty": 40
}
],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [
  "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
],
"permissions": [],
"items": [],
"data": [],
"confirmations": 272,
"blockhash": "03c734caa6caac264cef1853312c75a4e944449658fdb185b023c61d20d9ca15",
"blockindex": 1,
"blocktime": 1544511323,
"txid": "43dbacfa1af8a27af648de957d7d83b74c675027c8a44b650eb69a8f1cc2406c",
"valid": true,
"time": 1544511315,
"timereceived": 1544511315,
"comment": "These are the details of this transfer"
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [],
"data": [],
"confirmations": 239,
"blockhash": "045ea9d1fcccee52200b0daa2310521e6180ad82fc8406962cc06acea47a8c50",
"blockindex": 1,
"blocktime": 1544512966,
"txid": "87f4fd20b1c6731217d289611527f80945630398bb0689b4671de7960b0fc266",
"valid": true,
"time": 1544512957,
"timereceived": 1544512957
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [],
"data": [],
"confirmations": 228,
"blockhash": "06bd694b44565d2c6e15f01ab286a88ee06b92ee05ba0c39affe3d171cbae831",
"blockindex": 1,
"blocktime": 1544513757,
"txid": "02ace6a2add09d7c0cae81d5513778a51af5375b7fa5f921fbf6a57b7374b3f6",
"valid": true,
"time": 1544513748,
"timereceived": 1544513748
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [],
"data": [],
"confirmations": 208,
"blockhash": "05047b39a7ded8c9241ec8f52ba63519691edcd91309202d92613cdf62f743f5",
"blockindex": 1,
"blocktime": 1544513907,
"txid": "8d09db2c2a7f05c54adfd1c5dcf343b9980ff52c61fa17b24bac6e12ff9dd894",
"valid": true,
"time": 1544513901,
"timereceived": 1544513901
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [],
"data": [],
"confirmations": 196,
"blockhash": "0730b636d5443738f897c96e1604d71ddf3f9f7fa1ad72c5ddb9ea4dbe8fecb3",
"blockindex": 1,
"blocktime": 1544515700,
"txid": "65b6293b60cac5bec78e346486724f150103e55c9267b9ec86405590224fbe58",
"valid": true,
"time": 1544515690,
"timereceived": 1544515690
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [],
"data": [],
"confirmations": 185,
"blockhash": "0f8d87abdc042df42091b95fb2bb57f40d86bdaa05c722a5311c4dc37c2d328f",
"blockindex": 1,
"blocktime": 1544519325,
"txid": "d8e32370ecd43ca8c22191b7a206db9b91144d040f0d20492df02cb544e0e4f8",
"valid": true,
"time": 1544519309,
"timereceived": 1544519309
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [
  {
"type": "stream",
"name": "OFFER_DETAIL_STREAM",
"streamref": "410-267-45359",
"publishers": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"key": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
"data": "7b227072696d65636861696e5f61646472657373223a223136483657644452374c70487a5665456b6454694536644e695048426e6950746e7854596464222c2261736b5f6173736574223a22415554482d746f6b656e732d7365726965732d41222c226f666665724173736574223a22474f4c442d746f6b656e732d7365726965732d41222c226269645f616d6f756e74223a342c226f666665725f616d6f756e74223a322c2274786964223a2264386533323337306563643433636138633232313931623761323036646239623931313434643034306630643230343932646630326362353434653065346638222c22766f7574223a302c226f666665725f626c6f62223a223031303030303030303166386534653034346235326366303264343932303064306630343464313439313962646230366132623739313231633261383363643465633730323365336438303030303030303036393436333034333032323030323463643936336563383639313236633135363131616531363866333966346266646364353037613864376533373338643037393265356639616530396236303231663233366632306163613939363666646532666437656339633030343635383564343239303163666637643765333637363732396134653064633639646264383332313033616237353438643863333134383131306635393534353361633439316466653435643237316339326238386430636664643236623431656161376266626161306666666666666666303130303030303030303030303030303030333737366139313432373063336562656539643138346466323632373534323461663931353233366635316166646466383861633163373337303662373165373766306265626534626438366266346236613232356262343163363264373034303030303030303030303030303037353030303030303030227d"
}
],
"data": [
  "7b227072696d65636861696e5f61646472657373223a223136483657644452374c70487a5665456b6454694536644e695048426e6950746e7854596464222c2261736b5f6173736574223a22415554482d746f6b656e732d7365726965732d41222c226f666665724173736574223a22474f4c442d746f6b656e732d7365726965732d41222c226269645f616d6f756e74223a342c226f666665725f616d6f756e74223a322c2274786964223a2264386533323337306563643433636138633232313931623761323036646239623931313434643034306630643230343932646630326362353434653065346638222c22766f7574223a302c226f666665725f626c6f62223a223031303030303030303166386534653034346235326366303264343932303064306630343464313439313962646230366132623739313231633261383363643465633730323365336438303030303030303036393436333034333032323030323463643936336563383639313236633135363131616531363866333966346266646364353037613864376533373338643037393265356639616530396236303231663233366632306163613939363666646532666437656339633030343635383564343239303163666637643765333637363732396134653064633639646264383332313033616237353438643863333134383131306635393534353361633439316466653435643237316339326238386430636664643236623431656161376266626161306666666666666666303130303030303030303030303030303030333737366139313432373063336562656539643138346466323632373534323461663931353233366635316166646466383861633163373337303662373165373766306265626534626438366266346236613232356262343163363264373034303030303030303030303030303037353030303030303030227d"
],
"confirmations": 185,
"blockhash": "0f8d87abdc042df42091b95fb2bb57f40d86bdaa05c722a5311c4dc37c2d328f",
"blockindex": 2,
"blocktime": 1544519325,
"txid": "461d7cc3687e63c72e9d0009b605606bd36608be5929cebb694bb4bffd8cf7c0",
"valid": true,
"time": 1544519309,
"timereceived": 1544519309
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "GOLD-tokens-series-A",
"assetref": "301-267-14695",
"qty": -2
},
  {
"name": "AUTH-tokens-series-A",
"assetref": "324-267-25303",
"qty": 4
}
],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [
  "1CbfDWDYN8A7i4zZisEzfkLwRcQUem3PaUin9p"
],
"permissions": [],
"items": [],
"data": [],
"confirmations": 174,
"blockhash": "0560661517b79490ca1a66c5b362bb6b9c5070b25078fe936b4da5a83af0c283",
"blockindex": 2,
"blocktime": 1544520351,
"txid": "932b8b016c5465981c7d68dc1ec4d6ce2157416c821a05699fbb1a4796b03a47",
"valid": true,
"time": 1544520341,
"timereceived": 1544520341
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [],
"data": [],
"confirmations": 163,
"blockhash": "0d4076f1cae15ac13a4a5896f62b2ceaf89146ce4440c911f863f0ecda9f43ac",
"blockindex": 1,
"blocktime": 1544521023,
"txid": "9d4830a199ca967ff00754e7b55027b25b3c95b038e68c5ac58d413a08ec5eff",
"valid": true,
"time": 1544521008,
"timereceived": 1544521008
},
  {
"balance": {
"amount": 0,
"assets": [],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"items": [
  {
"type": "stream",
"name": "AUTH_USERS_MASTERLIST",
"streamref": "476-266-56933",
"publishers": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"key": "16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA",
"data": "7b22757365725f6964656e746966696572223a223233373932333837222c22757365725f6465736372697074696f6e223a2253616d6169726168204e616770616c2773204e6f6f646c652042616e6b20617070206f6e206865722069506164222c227072696d65636861696e5f7075626c69635f6b6579223a22303231633264326538396436386137636434353035663234363463323664326163653963656433343333663537616336313961396335326663393037303432333039222c227072696d65636861696e5f61646472657373223a2231366738643855334b335062637659364c596166675a32334a726e785258775a714250387341222c227273615f7075626c69635f6b6579223a222d2d2d2d2d424547494e205055424c4943204b45592d2d2d2d2d5c6e4d494942496a414e42676b71686b6947397730424151454641414f43415138414d49494243674b434151454169423439754f41496677326e47737565626f564c5c6e2b43575059716959532f2b705972556a6f4365336f77776e3339356f363849506d59446d324e43596b313744777832624457352f42344f46677a6e772b6553655c6e4867314b3252724351627741724b73736a657a3034567456424f446f77762f683875737136522f67317a73412f59745a544c484d523074647239546f6e304f705c6e474262632f717367416f37364f4a76476379376477435863627a566b73636a55526956513847726e2b79767053354451573066736b6c556f5836554f386573545c6e6c4631752b54464461697a4d75356931626c2f43696269527a633569542f45393037796e426332505a417063696365733845657261385965386b474732637a355c6e4c49756634394f66546c71357a5251514c7a724853463554673463566d784f4834585533736266504e786e76545643424f4e7135394c597647734e42587544485c6e68514944415141425c6e2d2d2d2d2d454e44205055424c4943204b45592d2d2d2d2d227d"
}
],
"data": [
  "7b22757365725f6964656e746966696572223a223233373932333837222c22757365725f6465736372697074696f6e223a2253616d6169726168204e616770616c2773204e6f6f646c652042616e6b20617070206f6e206865722069506164222c227072696d65636861696e5f7075626c69635f6b6579223a22303231633264326538396436386137636434353035663234363463323664326163653963656433343333663537616336313961396335326663393037303432333039222c227072696d65636861696e5f61646472657373223a2231366738643855334b335062637659364c596166675a32334a726e785258775a714250387341222c227273615f7075626c69635f6b6579223a222d2d2d2d2d424547494e205055424c4943204b45592d2d2d2d2d5c6e4d494942496a414e42676b71686b6947397730424151454641414f43415138414d49494243674b434151454169423439754f41496677326e47737565626f564c5c6e2b43575059716959532f2b705972556a6f4365336f77776e3339356f363849506d59446d324e43596b313744777832624457352f42344f46677a6e772b6553655c6e4867314b3252724351627741724b73736a657a3034567456424f446f77762f683875737136522f67317a73412f59745a544c484d523074647239546f6e304f705c6e474262632f717367416f37364f4a76476379376477435863627a566b73636a55526956513847726e2b79767053354451573066736b6c556f5836554f386573545c6e6c4631752b54464461697a4d75356931626c2f43696269527a633569542f45393037796e426332505a417063696365733845657261385965386b474732637a355c6e4c49756634394f66546c71357a5251514c7a724853463554673463566d784f4834585533736266504e786e76545643424f4e7135394c597647734e42587544485c6e68514944415141425c6e2d2d2d2d2d454e44205055424c4943204b45592d2d2d2d2d227d"
],
"confirmations": 141,
"blockhash": "074941927ed2f19d6631afbd0b2ec345b95e93d0050fcd8aa94e4d9f2009dfa0",
"blockindex": 1,
"blocktime": 1544599972,
"txid": "ef3f1cde044f0a16382230d4e700143da3ef5138a2bfb60791c05461a0ff1de2",
"valid": true,
"time": 1544599961,
"timereceived": 1544599961
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "Tasset1",
"assetref": "575-267-50282",
"qty": 2233
}
],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"issue": {
"name": "Tasset1",
"assetref": "575-267-50282",
"multiple": 1,
"units": 1,
"open": true,
"details": {
"details": "Sample asset for trading"
},
"qty": 2233,
"raw": 2233,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
},
"items": [],
"data": [],
"confirmations": 53,
"blockhash": "0746d9288863c90131e26853e9b5a9ba239ba811d31cc299521997a849d424bb",
"blockindex": 1,
"blocktime": 1544684810,
"txid": "6ac4cba18e796bd211eb0bb162a9a6de3c368f1e19042c10433213774a44c5cf",
"valid": true,
"time": 1544684800,
"timereceived": 1544684800
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "Tasset",
"assetref": "586-267-9093",
"qty": 3344
}
],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"issue": {
"name": "Tasset",
"assetref": "586-267-9093",
"multiple": 1,
"units": 1,
"open": true,
"details": {
"details": "Sample asset for testing"
},
"qty": 3344,
"raw": 3344,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
},
"items": [],
"data": [],
"confirmations": 42,
"blockhash": "0298a6fa58a0f2f4454aecb1e41b2beff7093d69a6830bdee21d1fd8f7a61f2c",
"blockindex": 1,
"blocktime": 1544685131,
"txid": "8523e702acf968a499a46f143f15f211cb84606684e382b468701a25362010a2",
"valid": true,
"time": 1544685119,
"timereceived": 1544685119
},
  {
"balance": {
"amount": 0,
"assets": [
  {
"name": "Tasset",
"assetref": "586-267-9093",
"qty": 12
}
],
},
"myaddresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
"addresses": [],
"permissions": [],
"issue": {
"name": "Tasset",
"assetref": "586-267-9093",
"details": {},
"qty": 12,
"raw": 12,
"addresses": [
  "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
],
},
"items": [],
"data": [],
"confirmations": 31,
"blockhash": "07badcc984d045a483779b1c533541a97f831d69b7098a472234b11b19269220",
"blockindex": 1,
"blocktime": 1544686547,
"txid": "f7c185359b77adb0ce32a9520bcbc777de1526a3c4bcd923c89bc2d4f85e8f94",
"valid": true,
"time": 1544686536,
"timereceived": 1544686536
}
],
}
```
