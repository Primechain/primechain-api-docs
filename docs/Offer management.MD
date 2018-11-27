# Offer management

[1. Create a public offer](#1-create-a-public-offer)   
[2. Create a targetted offer](#2-create-a-targetted-offer)   
[3. Read an offer](#3-read-an-offer)   
[4. Accept an offer](#4-accept-an-offer)   
[5. Reject an offer](#5-reject-an-offer)   
[6. Cancel an offer](#6-cancel-an-offer)   

## 1. Create a public offer
To create an offer, use `create_public_offer` and pass these parameters:
* address of the entity making the offer - `from_address`, 
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
aaaa
```

The output is the `transaction id` and the `hexadecimal blob` of the offer details.
```
aaaa
```
## 2. Create a targetted offer
To create an offer, use `/create_targeted_offer` and pass these parameters:
* address of the entity making the offer - `from_address`   
* address of the entity to whom the offer is made - `to_address`   
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
{
  "from_address": "1Uw5kTMTx96YAoQ81BrnuDezcdFhVmAWvCMDTN",
  "to_address": "16XxJEpKQCmxEhXs56Wsb2WaTghVzKixYTR92k",
  "ask_asset": 
    {
      "Uranium-tokens-series-A": 40
    },
  "offer_asset": 
    {
      "Platinum-tokens-series-A": 10
    }
}
```
The output is the `transaction id` and the `offer blob` of the offer details.
```
{
  "status": 200,
  "offer_blob": "01000000019e57279825b7413826a879a437dc51572c89fcb1462e1f86927ddc8fb0485ad4000000006a4730440220282026f991b7f46dde67e4ae72b4e838e955cc538cbcbcc2cdf3f44ad20c04f10220777e5ed8178b1c542a4a044a9d3446d304f5df54ebd5f98c416d3cbd80adb79a832102be496ef6b719a8bf9f472fa778e490fc4dcbc333d133634a323c140a975244bdffffffff0100000000000000003776a914ceab8b6fd5876940500dc9e6e9e402b0424c34c888ac1c73706b712ca4a239e8175078e715648b47a58b4328000000000000007500000000"
}
```

## 3. Read an offer
To interpret an offer, use `read_offer` and pass the hex blob:
```
{
  "offer_blob": "01000000019e57279825b7413826a879a437dc51572c89fcb1462e1f86927ddc8fb0485ad4000000006a4730440220282026f991b7f46dde67e4ae72b4e838e955cc538cbcbcc2cdf3f44ad20c04f10220777e5ed8178b1c542a4a044a9d3446d304f5df54ebd5f98c416d3cbd80adb79a832102be496ef6b719a8bf9f472fa778e490fc4dcbc333d133634a323c140a975244bdffffffff0100000000000000003776a914ceab8b6fd5876940500dc9e6e9e402b0424c34c888ac1c73706b712ca4a239e8175078e715648b47a58b4328000000000000007500000000"
}
```
```
{
"status": 200,
"response": {
"offer": {
"amount": 0,
"assets": [
  {
"name": "Platinum-tokens-series-A",
"assetref": "895-267-41850",
"qty": 10
}
],
},
"ask": {
"amount": 0,
"assets": [
  {
"name": "Uranium-tokens-series-A",
"assetref": "902-267-35651",
"qty": 40
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
## 4. Accept an offer
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
```
{
"status": 200,
"response": "b404760027e02ff6d2fd192fde20e9a5d83cbb698e35a0c60fbff064349a5ae6"
}
```

## 5. Reject an offer
To reject an offer, use `reject_offer` and pass the `txid` of the offer as a parameter.
```
{
  "tx_id": "2b36fe1ee137155a561e0df4f26af422ef7853c564dd0815b754eaaa3942ab2b"
}
```
```
{
"status": 200,
"response": true
}
```

## 6. Cancel an offer
To cancel an offer, use `cancel_offer` and pass the `txid` of the offer as a parameter.
```
{
"tx_id": "2de5443596eae41a9b46ac41043e8d9c978da54b1bbde4715b872f4794ed1c24"
}
```
```
{
"status": 200,
"response": true
}
```
