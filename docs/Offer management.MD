# Offer management

[1. Create a public offer](#1-create-a-public-offer)   
[2. Get list of open public offers](#2-get-list-of-open-public-offers)   
[3. Read an offer](#3-read-an-offer)   
[4. Accept an offer](#4-accept-an-offer)   
[5. Cancel a public offer](#5-cancel-a-public-offer)  
[6. Create a targeted offer](#6-create-a-targeted-offer)   
[7. Reject a targeted offer](#7-reject-a-targeted-offer)   

## 1. Create a public offer
To create an offer, use `post /api/v1/create_public_offer` and pass these parameters:
* address of the entity making the offer - `primechain_address`, 
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
{
  "primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
  "ask_asset": 
   {
     "AUTH-tokens-series-A": 4
   },
  "offer_asset": 
  {
    "GOLD-tokens-series-A": 2
  }
}
```
The following is stored in the OFFER_DETAIL_STREAM   
1. primechain_address of the offer creator
2. name of asset asked for
3. name of asset offerred
4. quantity of asset asked for
5. quantity of asset offerred
6. offer hex blob

The output is the id and vout of the transaction in which the offer data is stored in the blockchain.
```
{
"status": 200,
"response": 
  {
    "offer_txid": "d8e32370ecd43ca8c22191b7a206db9b91144d040f0d20492df02cb544e0e4f8",
    "offer_vout": 0
   }
}
```

## 2. Get list of open public offers
To get a list of open public offers made by an address, use `post /api/v1/get_open_offer` and pass the address as a  parameter:
```
{
  "primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd"
}
```
Output
```
{
"status": 200,
"response": [
  {
"primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
"ask_asset": "AUTH-tokens-series-A",
"offer_asset": "GOLD-tokens-series-A",
"bid_amount": 4,
"offer_amount": 2,
"txid": "8d09db2c2a7f05c54adfd1c5dcf343b9980ff52c61fa17b24bac6e12ff9dd894",
"vout": 0
},
  {
"primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
"ask_asset": "AUTH-tokens-series-A",
"offer_asset": "GOLD-tokens-series-A",
"bid_amount": 4,
"offer_amount": 2,
"txid": "65b6293b60cac5bec78e346486724f150103e55c9267b9ec86405590224fbe58",
"vout": 0,
"offer_blob": "010000000158be4f2290554086ecb967925ce50301154f728664348ec7bec5ca603b29b665000000006a473044022018726f00fad05632a1f2d72718d4e276c018a5196c47dc936167c7d1cedcb544022062678becdca71459438983490ef400e6a974d7597fe56135cfb3b0c54e7e6e28832103ab7548d8c3148110f595453ac491dfe45d271c92b88d0cfdd26b41eaa7bfbaa0ffffffff0100000000000000003776a914270c3ebee9d184df26275424af915236f51afddf88ac1c73706b71e77f0bebe4bd86bf4b6a225bb41c62d704000000000000007500000000"
},
  {
"primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
"ask_asset": "AUTH-tokens-series-A",
"offer_asset": "GOLD-tokens-series-A",
"bid_amount": 4,
"offer_amount": 2,
"txid": "d8e32370ecd43ca8c22191b7a206db9b91144d040f0d20492df02cb544e0e4f8",
"vout": 0,
"offer_blob": "0100000001f8e4e044b52cf02d49200d0f044d14919bdb06a2b79121c2a83cd4ec7023e3d800000000694630430220024cd963ec869126c15611ae168f39f4bfdcd507a8d7e3738d0792e5f9ae09b6021f236f20aca9966fde2fd7ec9c0046585d42901cff7d7e3676729a4e0dc69dbd832103ab7548d8c3148110f595453ac491dfe45d271c92b88d0cfdd26b41eaa7bfbaa0ffffffff0100000000000000003776a914270c3ebee9d184df26275424af915236f51afddf88ac1c73706b71e77f0bebe4bd86bf4b6a225bb41c62d704000000000000007500000000"
}
],
}
```

## 3. Read an offer
To interpret an offer, use `post /api/v1/read_offer` and pass the hex blob:
```
{
  "offer_blob": "0100000001f8e4e044b52cf02d49200d0f044d14919bdb06a2b79121c2a83cd4ec7023e3d800000000694630430220024cd963ec869126c15611ae168f39f4bfdcd507a8d7e3738d0792e5f9ae09b6021f236f20aca9966fde2fd7ec9c0046585d42901cff7d7e3676729a4e0dc69dbd832103ab7548d8c3148110f595453ac491dfe45d271c92b88d0cfdd26b41eaa7bfbaa0ffffffff0100000000000000003776a914270c3ebee9d184df26275424af915236f51afddf88ac1c73706b71e77f0bebe4bd86bf4b6a225bb41c62d704000000000000007500000000"
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
"name": "GOLD-tokens-series-A",
"assetref": "301-267-14695",
"qty": 2
}
],
},
"ask": {
"amount": 0,
"assets": [
  {
"name": "AUTH-tokens-series-A",
"assetref": "324-267-25303",
"qty": 4
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
  "primechain_address": "1CbfDWDYN8A7i4zZisEzfkLwRcQUem3PaUin9p",
  "offer_blob": "0100000001f8e4e044b52cf02d49200d0f044d14919bdb06a2b79121c2a83cd4ec7023e3d800000000694630430220024cd963ec869126c15611ae168f39f4bfdcd507a8d7e3738d0792e5f9ae09b6021f236f20aca9966fde2fd7ec9c0046585d42901cff7d7e3676729a4e0dc69dbd832103ab7548d8c3148110f595453ac491dfe45d271c92b88d0cfdd26b41eaa7bfbaa0ffffffff0100000000000000003776a914270c3ebee9d184df26275424af915236f51afddf88ac1c73706b71e77f0bebe4bd86bf4b6a225bb41c62d704000000000000007500000000"
}
```
```
{
"status": 200,
"response": "932b8b016c5465981c7d68dc1ec4d6ce2157416c821a05699fbb1a4796b03a47"
}
```

## 5. Cancel a public offer
To cancel an offer, use `post /api/v1/cancel_public_offer` and pass the offerrer's address and `txid` of the offer as a parameter.
```
{
  "primechain_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
  "tx_id": "d8e32370ecd43ca8c22191b7a206db9b91144d040f0d20492df02cb544e0e4f8"
}
```
```
{
"status": 200,
"response": true
}
```

## 6. Create a targeted offer
To create an offer, use `post /api/v1/create_targeted_offer` and pass these parameters:
* address of the entity making the offer - `from_address`   
* address of the entity to whom the offer is made - `to_address`   
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
{
  "from_address": "16H6WdDR7LpHzVeEkdTiE6dNiPHBniPtnxTYdd",
   "to_address": "1CbfDWDYN8A7i4zZisEzfkLwRcQUem3PaUin9p",
   
  "ask_asset": 
   {
     "AUTH-tokens-series-A": 4
   },
  "offer_asset": 
  {
    "GOLD-tokens-series-A": 2
  }
}
```
The output is the `transaction id` and the `offer blob` of the offer details.
```
{
"status": 200,
"response": {
"offer_blob": "0100000001ff5eec083a418dc55a8ce638b0953c5bb22750b5e75407f07f96ca99a130489d000000006a47304402206774afd0964167b47d97a36135f94aa46deb39aba25359d6c898cf3d31a5c184022041753eadc1f0e1096d2f6e95765be7ea27725a6488dbb18940b1420839de8f15832103ab7548d8c3148110f595453ac491dfe45d271c92b88d0cfdd26b41eaa7bfbaa0ffffffff0100000000000000003776a914270c3ebee9d184df26275424af915236f51afddf88ac1c73706b71e77f0bebe4bd86bf4b6a225bb41c62d704000000000000007500000000",
"offer_txid": "9d4830a199ca967ff00754e7b55027b25b3c95b038e68c5ac58d413a08ec5eff",
"offer_vout": 0
}
}

```

## 7. Reject a targeted offer
To reject an offer, use `post /api/v1/reject_targeted_offer` and pass the offeree address and the `txid` of the offer as a parameter.
```
{
   "primechain_address": "1CbfDWDYN8A7i4zZisEzfkLwRcQUem3PaUin9p",
   "tx_id": "9d4830a199ca967ff00754e7b55027b25b3c95b038e68c5ac58d413a08ec5eff"
}
```
```
{
"status": 200,
"response": true
}
```
