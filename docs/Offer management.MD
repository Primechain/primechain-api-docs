# Offer management

[1. Creating an offer](#1-creating-an-offer)

[2. Reading an offer](#2-reading-an-offer)

[3. Accepting an offer](#3-accepting-an-offer)

[4. Rejecting an offer](#4-rejecting-an-offer)

[5. Cancelling an offer](#5-cancelling-an-offer)

## 1. Creating an offer
To create an offer, use `create_offer` and pass these parameters:
* address of the entity making the offer - `from_address`, 
* address of the entityto whom the offer is made - `to_address`, 
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
{
  "from_address": "1LfegkhQAD6jVZ1VQ4eJMLd4Ydt3MqodbnizqV",
  "to_address": "1LcJbJWGmN59AAE7xfMk6GYW2Jsy4V8Fay2p4Q",
  "ask_asset": {
    "silver-tokens": 40
  },
  "offer_asset": {
    "gold-tokens": 10
  }
}
```
![Creating an offer](http://www.primechaintech.com/img/api_documentation/create_offer4.png)

The output is the `transaction id` and the `hexadecimal blob` of the offer details.
```
{
"status": 200,
"transaction_id": "6f3d9bca21303e4202903d12421bd689b601ecac0eb4e7956c123843260bd145",
"offer_blob": "0100000001d5d9b15fab6b3bc833f3c77d2a43f734675cfb39190b80f2e272e797308b5e01000000006a473044022005f121a474ec0eae78f80fe0fe5bfb016e12bf59949482f5e964f43b79d00d8f022001f62a8d4785759bf62ca4acc77b9fba69fe88118ff6400e6dbbffadd82a99178321033d1196659ec9c34eaa029393a4847a84b3a6f3caa9d49626f91f60748bb0d84fffffffff0100000000000000003776a9149115494fbc2450905dd05e2c8cd28672617807c388ac1c73706b71945e564ca39292efe316cae288dddf310a000000000000007500000000"
}
```

## 2. Reading an offer
To interpret an offer, use `read_offer` and pass the hex blob:
```
{
  "hex_blob": "0100000001d5d9b15fab6b3bc833f3c77d2a43f734675cfb39190b80f2e272e797308b5e01000000006a473044022005f121a474ec0eae78f80fe0fe5bfb016e12bf59949482f5e964f43b79d00d8f022001f62a8d4785759bf62ca4acc77b9fba69fe88118ff6400e6dbbffadd82a99178321033d1196659ec9c34eaa029393a4847a84b3a6f3caa9d49626f91f60748bb0d84fffffffff0100000000000000003776a9149115494fbc2450905dd05e2c8cd28672617807c388ac1c73706b71945e564ca39292efe316cae288dddf310a000000000000007500000000"
}
```
![Reading an offer](http://www.primechaintech.com/img/api_documentation/read_offer.png)
```
{
"status": 200,
"read_offer": {
"offer": {
"amount": 0,
"assets": [
  {
"name": "gold-tokens",
"assetref": "157-267-10355",
"qty": 40
}
],
},
"ask": {
"amount": 0,
"assets": [
  {
"name": "silver-tokens",
"assetref": "169-267-57137",
"qty": 10
}
],
},
"requiredfee": 0,
"candisable": true,
"cancomplete": true,
"complete": false
}
}
```
## 3. Accepting an offer
To accept an offer, use `accept_offer` and pass 3 parameters - `from_address`, `hex_blob`, `ask_asset` and `offer_asset`
```
{
  "from_address": "1LcJbJWGmN59AAE7xfMk6GYW2Jsy4V8Fay2p4Q",
      "hex_blob":"0100000001d5d9b15fab6b3bc833f3c77d2a43f734675cfb39190b80f2e272e797308b5e01000000006a473044022005f121a474ec0eae78f80fe0fe5bfb016e12bf59949482f5e964f43b79d00d8f022001f62a8d4785759bf62ca4acc77b9fba69fe88118ff6400e6dbbffadd82a99178321033d1196659ec9c34eaa029393a4847a84b3a6f3caa9d49626f91f60748bb0d84fffffffff0100000000000000003776a9149115494fbc2450905dd05e2c8cd28672617807c388ac1c73706b71945e564ca39292efe316cae288dddf310a000000000000007500000000",
   "ask_asset": {
    "silver-tokens": 40
  },
  "offer_asset": {
    "gold-tokens": 10
  }
}
```
![Accepting an offer](http://www.primechaintech.com/img/api_documentation/accept_offer.png)
```
{
"status": 200,
"response": "b404760027e02ff6d2fd192fde20e9a5d83cbb698e35a0c60fbff064349a5ae6"
}
```

## 4. Rejecting an offer
To reject an offer, use `reject_offer` and pass the `txid` of the offer as a parameter.
```
{
  "tx_id": "2b36fe1ee137155a561e0df4f26af422ef7853c564dd0815b754eaaa3942ab2b"
}
```
![Rejecting an offer](http://www.primechaintech.com/img/api_documentation/reject_offer.png)
```
{
"status": 200,
"response": true
}
```

## 5. Cancelling an offer


