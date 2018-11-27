# Offer management

[1. Create a public offer](#1-create-a-public-offer)   
[2. Create a targetted offer](#2-create-a-targetted-offer)   
[3. Read an offer](#3-read-an-offer)   
[4. Accept an offer](#4-accept-an-offer)   
[5. Reject an offer](#5-reject-an-offer)   
[6. Cancel an offer](#6-cancel-an-offer)   

## 1. Create a public offer
To create an offer, use `post /api/v1/create_public_offer` and pass these parameters:
* address of the entity making the offer - `primechain_address`, 
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
{
  "primechain_address": "1Uw5kTMTx96YAoQ81BrnuDezcdFhVmAWvCMDTN",
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

The output is the `transaction id` and the `offer_blob` of the offer details.
```
{
  "status": 200,
  "response": 
    {
      "offer_blob": "0100000001cc3c30cf5a5e2f891fb462f8796df599d9d815de67367b37a4aa5d3d27171e60000000006b483045022100f46fc5bed8b3dee978ad09e40616442279d272ac05abf2bea720cc680e5e8d0e0220659460108564bbdd993b60c8ca822637ac307c40bbaa06a78a7efd402a21e812832102be496ef6b719a8bf9f472fa778e490fc4dcbc333d133634a323c140a975244bdffffffff0100000000000000003776a914ceab8b6fd5876940500dc9e6e9e402b0424c34c888ac1c73706b712ca4a239e8175078e715648b47a58b4328000000000000007500000000",
      "offer_txid": "601e17273d5daaa4377b3667de15d8d999f56d79f862b41f892f5e5acf303ccc",
      "offer_vout": 0
    }
}
```
## 2. Create a targetted offer
To create an offer, use `post /api/v1/create_targeted_offer` and pass these parameters:
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
"response": {
"offer_blob": "01000000017a61711f21cfbff5fd8f465d9de00e262a1ffebcf3d1a9d70ec842e08736963a000000006b483045022100871b3625760bbaad16c376bc082d93aac98393eebf9560293214d98ffd8b29ad0220172131642087078977c4c5c6c68b8178a0903219a6210cdc5e07c3e9bae9ea16832102be496ef6b719a8bf9f472fa778e490fc4dcbc333d133634a323c140a975244bdffffffff0100000000000000003776a914ceab8b6fd5876940500dc9e6e9e402b0424c34c888ac1c73706b712ca4a239e8175078e715648b47a58b4328000000000000007500000000",
"offer_txid": "3a963687e042c80ed7a9d1f3bcfe1f2a260ee09d5d468ffdf5bfcf211f71617a",
"offer_vout": 0
}
}
```

## 3. Read an offer
To interpret an offer, use `post /api/v1/read_offer` and pass the hex blob:
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
To accept an offer, use `post /api/v1/accept_offer` and pass 2 parameters - 
1. `primechain_address` of the acceptor   
2. `offer_blob` relating to the offer   
```
{
  "primechain_address": "16XxJEpKQCmxEhXs56Wsb2WaTghVzKixYTR92k",
  "offer_blob": "01000000019e57279825b7413826a879a437dc51572c89fcb1462e1f86927ddc8fb0485ad4000000006a4730440220282026f991b7f46dde67e4ae72b4e838e955cc538cbcbcc2cdf3f44ad20c04f10220777e5ed8178b1c542a4a044a9d3446d304f5df54ebd5f98c416d3cbd80adb79a832102be496ef6b719a8bf9f472fa778e490fc4dcbc333d133634a323c140a975244bdffffffff0100000000000000003776a914ceab8b6fd5876940500dc9e6e9e402b0424c34c888ac1c73706b712ca4a239e8175078e715648b47a58b4328000000000000007500000000"
}
```
```
{
"status": 200,
"response": "030f9de4f6e753de3e29edf6ba12330b9364716013292af0203c3fcaa8306b73"
}
```

## 5. Reject an offer
To reject an offer, use `post /api/v1/reject_offer` and pass the `txid` of the offer as a parameter.
```
{
  "tx_id": "aaaa"
}
```
```
{
"status": 200,
"response": true
}
```

## 6. Cancel an offer
To cancel an offer, use `post /api/v1/cancel_offer` and pass the `txid` of the offer as a parameter.
```
{
"tx_id": "aaaa"
}
```
```
{
"status": 200,
"response": true
}
```
