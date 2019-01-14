# Trade Finance

[![Primechain Technologies](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)
[![TRADE-Chain brochure](https://img.shields.io/badge/Download-Brochure-green.svg)](http://www.primechaintech.com/docs/brochures/Trade_Chain.pdf)

The market for trade finance is above US$ 12 trillion annually. TRADE-Chain is a permissioned "global trade finance" blockchain for the world’s banks and financial institutions. TRADE-Chain nodes are available to banks, financial institutions and large exporters, importers, shippers and investors.

![Letter of credit](http://www.primechaintech.com/img/tradechain/tradechain_top.jpg)

### Table of contents  

***[1. Introduction and overview](#1-introduction-and-overview)***   
[1.1 Sandbox blockchain](#11-sandbox-blockchain)    
[1.2 Production blockchain](#12-production-blockchain)    
[1.3 System requirements for nodes](#13-system-requirements-for-nodes)   
[1.4 Information Security issues](#14-information-security-issues)   
[1.5 API keys for sandbox](#15-api-keys-for-sandbox)   
[1.6 Default address for a node](#16-default-address-for-a-node)   
[1.7 Additional addresses](#17-additional-addresses)

***[2. Trade channels and permissions to write to them](#2-trade-channels-and-permissions-to-write-to-them)***    
[2.1 Create a new data stream](#21-create-a-new-data-stream)   
[2.2 Grant write permissions](#22-grant-write-permissions)   
[2.3 Revoke write permissions](#23-revoke-write-permissions)   

***[3. Real-time issuing and sharing of trade documents.](#3-real-time-issuing-and-sharing-of-trade-documents)***   
[3.1 Types of documents](#31-types-of-documents)    
[3.2 Issuance of documents on TRADE-Chain](#32-issuance-of-documents-on-trade-chain)   
[3.3 Retrieving documents from TRADE-Chain](#33-retrieving-documents-from-trade-chain)    

***[4. Real-time tracking of cargo](#4-real-time-tracking-of-cargo)*** 

***[5. Cross-border and domestic trade payments](#5-cross-border-and-domestic-trade-payments)***

***[6. Factoring and invoice discounting platform](#6-factoring-and-invoice-discounting-platform)***   
[6.1 Process flow](#61-process-flow)   
[6.2 Publishing a new invoice](#62-publishing-a-new-invoice)   
[6.3 Viewing invoices](#63-viewing-invoices)   
[6.4 Bidding by investors](#64-bidding-by-investors)   
[6.5 Cancelling of bids by investors](#65-cancelling-of-bids-by-investors)   
[6.6 Viewing bids](#66-viewing-bids)   
[6.7 Rejection of bids](#67-rejection-of-bids)   
[6.8 Acceptance of bids](#68-acceptance-of-bids)   
[6.9 Buyback of the invoice upon maturity of invoice](#69-buyback-of-the-invoice-upon-maturity-of-invoice)   
[6.10 Retiring the invoice](#610-retiring-the-invoice)   

***[7. Auction platform for goods and freight contracts](#7-auction-platform-for-goods-and-freight-contracts)***


## 1. Introduction and overview

TRADE-Chain is a permissioned multi-framework blockchain powered by Primechain APIs. TRADE-Chain nodes are available to banks, financial institutions and large exporters, importers, shippers and investors.

***The pain points of today’s trade finance processes are:***
1. Delays and errors due to manual document creation and distribution.
2. Invoice factoring risk.
3. Delayed timeline.
4. Manual AML review.
5. Fraud risk due to multiple disconnected platforms.
6. Fraud risk due to duplicate bills of lading.

***Core benefits of TRADE-Chain:***
1. Real-time review and approval of documents.
2. Real-time, transparent view of invoices for discounting and factoring.
3. Eliminating the need for correspondent banks and other intermediaries.
4. Elimination of fraud by providing real-time, transparent view of bills of lading.
5. Transparency in terms of ownership and location of goods.
6. Real-time, automated settlements without the need for reconciliation.
7. Real-time view to regulators leading to complete regulatory transparency.
8. Reducing the letter of credit issue process from several days to a few hours.
9. Reducing the time of delivery for trade documents from several days to a few hours.   
10.Increased transparency by sharing transaction details with all parties.

### 1.1 Sandbox blockchain
To access the TRADE-Chain sandbox, email us on info@primechain.in

### 1.2 Production blockchain
Nodes on the commercial / production TRADE-Chain are available free to all Bankchain members and at an annual subscription fee for non-members. Email us on info@primechain.in for details.

### 1.3 System requirements for nodes
2 virtual machines / physical servers with the following details are required:
* Ubuntu 16.04 machine with 32 GB RAM, 4 core processor, 100 GB SSD disk with ports 22, 15590 and 61172 open.   
* Ubuntu 16.04 machine with 32 GB RAM, 8 core processor, 25 GB SSD disk with ports 22 and 2512 open.

### 1.4 Information Security issues
* Symmetric and asymmetric cryptography ensures ***confidentiality*** of data.   
* Hash functions ensure ***integrity*** of data.   
* Multiple blockchain nodes ensure ***availability*** of data.   
* Blockchain technology ensures provable ***immutability*** of data.   
* Digital signatures ensure ***non-repudiation***.   
* [Blockchain Security Controls](http://www.primechaintech.com/bsc.php) provide the security controls and information security framework.

### 1.5 API keys for sandbox
API keys authenticate access to the TRADE-Chain sandbox. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header. ([See example](http://www.primechaintech.com/img/api_documentation/sample_rest_api_client.jpg))

Sample API key
```
k3wq1TdYcEGb7sqX&Es8-xVR$ocdw5ICLtIh5rT661UDaZoKmLV!12X01ce!GnEW
```

### 1.6 Default address for a node
When a node connects to TRADE-Chain, it is provided a default primechain address with relevant permissions. 

### 1.7 Additional addresses
If required, additional addresses can be created on a node using `get /api/v1/create_entity`. The following are generated:
1. public key
2. private key
3. primechain address

The output will be the primechain address of the newly created signer. The private key is automatically stored in your node. This will not be visible to other nodes. This address will have permissions to send and receive assets e.g. invoices, fiat currency backed tokens, etc.

Sample output
```
{
  "status": 200,
  "primechain_address": "1VCeqGYXLaqMtAFtxTNeTzfW8T714us2t3uwYM"
}
```

## 2. Trade channels and permissions to write to them

Storing all the data relating to a transaction, shipment or event in a dedicated trade channel enables quick and efficient data retrieval and processing.

### 2.1 Create a new trade channel
To create a new trade channel use `post /api/v1/create_trade_channel` and provide these 4 parameters:
1. `primechain_address` - your node's default primechain address
2. `stream_name` - the stream name. This must be unique across the blockchain and can contain a maximum of 32 characters including blank spaces.
3. `details` - a short description of the data stream
4. `open`: `true` or `false` - whether the stream is open or not. If open is set to true, write permissions need not be explicitly provided. All addresses can write to the stream. If open is set to false, write permissions need to be explicitly provided. It is recommended to keep the stream as closed and to provide write permissions on an address basis. 

Sample input
```
{
  "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
  "stream_name": "200_tons_xyz_Jan_2019",
  "details": "This stream is for the consignment of 200 tons of xyz material",
  "open":false
}
```
The output is the transaction id of the transaction creating the stream - `tx_id`.
Sample output
```
{
 "status": 200,
 "tx_id": "d84f84849431d5a5c5565530021d4c8bc37bf7180c58a116bd42295f90b434e2"
}
```

### 2.2 Grant write permissions
To grant an entity write permission to a stream, use `post /api/v1/grant_write_permission_to_stream` and provide 3 parameters:
1. `primechain_address_stream_writer` - the primechain address of the entity to be granted write permission.
2. `stream_name` - the name of the relevant data stream.
3. `primechain_address_stream_creator` - the primechain address of the creator of the data stream.

***Note:*** This must be run on the node containing the private key of the stream creator.

Sample input
```
{
  "primechain_address_stream_writer": "125LHLRKDDdaJSWXbVdaAGG7pGRT9dWPjjF7aG",
  "stream_name": "200_tons_xyz_Jan_2019",
  "primechain_address_stream_creator": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp"
}
```
Sample output
```
{
  "status": 200,
  "tx_id": "94179d61270f24acc208b8647e735cb54307c4ccbfece64ebae0e9539c37b2bf"
}
```

### 2.3 Revoke write permissions
To revoke an entity's write permission to a stream, use `post /api/v1/revoke_write_permission_to_stream` and provide 3 parameters:
1. `primechain_address_stream_writer` - the primechain address of the entity whose write permission is to be revoked.
2. `stream_name` - the name of the relevant data stream.
3. `primechain_address_stream_creator` - the primechain address of the creator of the data stream.

***Note:*** This must be run on the node containing the private key of the stream creator.

Sample input
```
{
  "primechain_address_stream_writer": "125LHLRKDDdaJSWXbVdaAGG7pGRT9dWPjjF7aG",
  "stream_name": "200_tons_xyz_Jan_2019",
  "primechain_address_stream_creator": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp"
}
```
Sample output
```
{
  "status": 200,
  "tx_id": "83fd7c73360cc80a4bc89c3fa3de956deb145882219bcce3b5631a916b15b97a"
}
```

## 3. Real-time issuing and sharing of trade documents

### 3.1 Types of documents

TRADE-Chain provides a transparent repository for secure & real time issuing and sharing of trade documents such as:

***1. Commercial Documents:*** Quotation, Sales Contract, Pro Forma Invoice, Commercial Invoice, Packing List, Inspection Certificate, Insurance Policy, Insurance Certificate, Product Testing Certificate, Health Certificate, Phytosanitary Certificate, Fumigation Certificate, ATA Carnet, Consular Invoice.

***2. Transport Documents:*** Shipping Order, Dock / Mate's Receipt, Bill of Lading, House Bill of Lading, Sea Waybill, Air Waybill, House Air Waybill, Shipping Guarantee, Packing List.

***3. Financial Documents:*** Documentary Credit, Standby Credit, Collection Instruction, Bill of Exchange or Draft, Trust Receipt, Promissory Note.

***4. Government Documents:*** Certificate of Origin, Certificate of Origin, Import / Export Declaration, Import / Export Licence, International Import Certificate, Delivery Verification Certificate, Landing Certificate, Customs Invoice.

### 3.2 Issuance of documents on TRADE-Chain
To encrypt, sign and publish data to TRADE-Chain, use `post /api/v1/publish_data` and pass 4 parameters: 
1. `primechain_address` - the primechain address of the signer.
2. `keys` - the keys to enable quick searching of the data.
3. `data` - the data. 
4. `stream_name` - the name of the data stream to which the data is to be published.

Sample input
```
{
  "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
   "keys": 
    [
      "key1",
      "key2"
    ],
   "data": "This is the data that will be encryptd and stored.",
   "stream_name": "200_tons_xyz_Jan_2019"
}
```
***This is what happens:***   
1. The SHA-512 hash of the data is computed.
2. The hash is signed using the private key of the provided primechain address (using ECDSA).
3. The digital signature, hash and the primechain address of the signer are stored in the data stream.
4. The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
    * the encrypted version of the data    
    * the AES password    
    * the Initialization Vector (IV)    
    * the Authentication Tag (tag)   
5. The encrypted data and the tag are published to the data stream.

***The following is the output:***
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the data stream.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the the data stream.
3. `signature` - the digital signature
4. `aes_password` - the AES password
5. `aes_iv` - the Initialization Vector (IV)
6. `stream_name` - the name of the data-stream to which the data is published. 

Sample output
```
{
"status": 200,
"response": 
  {
    "tx_id_enc_data": "7e94282014b2b73bc17ac163e24b2538b6174ba96a4a27f4f2e2333e94346b96",
    "tx_id_signature": "f2d3f1954064b12d3f434cee8d68ed6f08960f7a400a41946c972680abdbaef2",
    "signature": "INfKjUiGDpMQ68K4GlTwh3Z3LDXrWpiJ4L2Qvn1wSqSxd0zauOZDn292E32GAQk6fsNvPl1G9ty1iRfXJWJDW0w=",
    "aes_password": "ScX56ZWKuqYsMpINcXScyfgSL0Ihc05c",
    "aes_iv": "lSr9HJqWN1eA",
    "stream_name": "200_tons_xyz_Jan_2019"
  }
}
```

## 3.3 Retrieving documents from TRADE-Chain
To retrieve data use `post /api/v1/get_data` and pass 5 parameters:
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the data stream.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the data stream.
3. `aes_password` - the AES password.
4. `aes_iv` - the Initialization Vector (IV).
5. `stream_name` - the name of the data stream from which the data is to be retrieved.

Sample input
```
{
  "tx_id_enc_data": "16346d48deea43865a276b5153fec90ac2ef83f146a20bf6826df995acdc5fc8",
  "tx_id_signature": "7c72b8fc633d9a091e878ef6c610e4383ca597f846092a35077374fb0accea76",
  "aes_password": "kfkNhEWZErbMLhtKkg6zSTy85Aq9QIJr",
  "aes_iv": "9UuZX4vgZ8r3",
  "stream_name": "200_tons_xyz_Jan_2019"
}
```
***This is what happens:***   
1. The digital signature, hash and the primechain address of the signing entity are retrieved from the data stream.
2. The encrypted data and tag are retrieved from the data stream.
3. The encrypted data is decrypted.
4. The digital signature is verified.

***The following is the output:***
1. `data` - the unencrypted data.   
2. `primechain_address` - the primechain address of the signer.   
3. `signature_status` - the verification status of the signature.  
4. `timestamp` - the timestamp

Sample output
```
{
"status": 200,
"response": {
"data": "This is the data that will be encryptd and stored.",
"signer_detail": "1BiWh3dEMEDVRHNTsrYf7MCHHfXP2qL6or34PP",
"signature_status": true,
"timestamp": "09/01/2019 01:42:47:00"
}
}
```

## 4. Real-time tracking of cargo

It is recommended to use National Marine Electronics Association (NMEA) formatted Global Positioning System (GPS) data while publishing real-time GPS data for cargo.

Sample input
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "NMEA_GPS_DATA": "$GPGGA,181908.00,3404.7041778,N,07044.3966270,W,4,13,1.00,495.144,M,29.200,M,0.10,0000*40",
    }
}
```
***Explanation:***
1. All NMEA messages start with the $ character, and each data field is separated by a comma.
2. `GP` represent that it is a GPS position (GL would denote GLONASS - Russia's version of GPS)
3. `181908.00` is the time stamp: UTC time in hours, minutes and seconds.
4. `3404.7041778` is the latitude in the DDMM.MMMMM format. Decimal places are variable.
5. `N` denotes north latitude.
6. `07044.3966270` is the longitude in the DDDMM.MMMMM format. Decimal places are variable.
7. `W` denotes west longitude.
8. `4` denotes the Quality Indicator: (`1` = Uncorrected coordinate, `2` = Differentially correct coordinate (e.g., WAAS, DGPS), `4` = RTK Fix coordinate (centimeter precision), `5` = RTK Float (decimeter precision)
9. `13` denotes number of satellites used in the coordinate.
10. `1.0` denotes the HDOP (horizontal dilution of precision).
11. `495.144` denotes altitude of the antenna.
12. `M` denotes units of altitude (eg. Meters or Feet)
13. `29.200` denotes the geoidal separation (subtract this from the altitude of the antenna to arrive at the Height Above Ellipsoid (HAE).
14. `M` denotes the units used by the geoidal separation.
15. `1.0` denotes the age of the correction (if any).
16. `0000` denotes the correction station ID (if any).
17. `*40` denotes the checksum.   
(Source: https://www.gpsworld.com/what-exactly-is-gps-nmea-data/)




## 5. Cross-border and domestic trade payments

## 6. Factoring and invoice discounting platform

Invoice discounting enables suppliers to sell their invoices at a discount to investors. This enables suppliers to get faster access to money they are owed and enables buyers to get more time to pay. Instead of relying on the creditworthiness of suppliers (usually smaller businesses), the investors deal with buyers (usually large businesses). This can lower financing costs, optimize working capital and improve business efficiency.

Invoice discounting is also referred to as supply chain finance and factoring. The process involves 4 parties: 
* banks   
* large corporates (payers)    
* supplier (payees)       
* investors   

Benefits of using the blockchain for invoice discounting include automated reconciliation and a provably immutable and transparent process.

### 6.1 Process flow

The process flow is as follows:
1. A corporate (payers) publishes an invoice to the blockchain. This invoice is a blockchain asset and is immediately transferred to the relevant supplier (payee).
2. Participants, especially investors, view invoices. This list of invoices can be filtered based on payer, payee, maturity date and value.
3. Investors purchase fiat currency tokens from the bank. The payment to the bank for purchasing these tokens is done via conventional banking processes.
4. All participants, especially investors, view all bids.
5. Investors place bids. The bid amount is "locked" and "un-spendable" till they cancel their bid or till the supplier (payee) rejects their bid. 
6. The supplier (payee) rejects bids that are not acceptable to her. 
7. The supplier (payee) accepts a bid. The invoice now gets transferred to the relevant investor and the supplier immediately receives the relevant quantity of tokens. This is an atomic transaction and does not require any re-conciliation. The supplier (payee) can redeem these tokens from the bank.
8. Upon maturity of the invoice, or any time before that, the corporate (payer) purchases fiat currency tokens from the bank. The payment to the bank for purchasing these tokens is done via conventional banking processes.
9. The corporate (payer) places a bid to purchase the invoice from the investor holding the invoice. 
10. The investor accepts the bid. The invoice now gets transferred to the corporate (payer) and the investor immediately receives the relevant quantity of tokens. This is an atomic transaction and does not require any re-conciliation.
11. The corporate (payer) retires the invoice by sending it to the burn address.

### 6.2 Publishing a new invoice
New invoices can be published to the blockchain by large corporates (payers) using `post /api/v1/create_invoice` and passing these parameters:   
1. `invoice_payer` - the primechain address of the corporate who is the payer of the invoice.  
2. `invoice_payee` - the primechain address of the supplier who is the payee of the invoice.    
3. `invoice_name` - the name of the invoice. This must be unique across the blockchain and can contain a maximum of 32 characters including blank spaces.
4. `invoice_details` - the details of the invoice. This contains 3 parameters, namely 
    * `invoice_amount` - the maturity amount of the invoice.
    * `invoice_maturity` - the maturity date of the invoice. 
    * `invoice_description` - optional additional information about the invoice.

The newly created invoice is created as an asset of the blockchain and is transferred automatically to the supplier (payee).

Sample input
```
{
  "invoice_payer": "aaa",
  "invoice_payee": "aaaa",
  "invoice_name": "Invoice no. 235235",  
  "invoice_details": 
    {
      "invoice_amount": "USD 856,000"
      "invoice_maturity": "10-April-2019"
      "invoice_description": "This is optional additional information about the invoice."
     }
}
```
***Note:*** This may take upto 30 seconds.   

***Output is:***
* `tx_id` - the id of the transaction in which the invoice was published to the blockchain
* `invoice_reference_number` - the unique reference number of the asset
* `invoice_details` - invoice details

Sample output
```
{
"status": 200,
"response": {
"tx_id": "6b8842e04d649d33a2f6cd4e632d1c61e5989dd46532a8a8eee566ee58656fbc",
"invoice_reference_number": "365-515-34923",
"invoice_details": {
"details": {
"invoice_amount": "USD 856,000",
"invoice_maturity": "10-April-2019",
"invoice_description": "This is optional additional information about the invoice."
}
}
}
}
```

### 6.3 Viewing invoices
Participants, especially investors, view invoices. This list of invoices can be filtered based on payer, payee, maturity date and value. To view all the invoices, use `get /api/v1/view_all_invoices`.

Sample output
```
{
"status": 200,
"all_invoices": [
  {
"name": "SILVER-tokens-series-A",
"issuetxid": "846d9aee914b262dab84206fa5f67254e3fb82efde467d5e3f3b906111ef1777",
"assetref": "115-513-28036",
"multiple": 1,
"units": 1,
"open": false,
"restrict": {
"send": false,
"receive": false
},
"details": {
"details": "Backed by silver jewellery held in Lot A at Zimblia office"
},
"issueqty": 19500,
"issueraw": 19500,
"subscribed": true,
"synchronized": true,
"transactions": 13,
"confirmed": 13,
"issues": [
  {
"txid": "846d9aee914b262dab84206fa5f67254e3fb82efde467d5e3f3b906111ef1777",
"qty": 19500,
"raw": 19500,
"details": {
"details": "Backed by silver jewellery held in Lot A at Zimblia office"
},
"issuers": [
  "1Go5neH1MUtcMdFfS6U5MDYsLJ51s6ZX1gmg3e"
],
}
],
},
  {
"name": "GOLD-tokens-series-A",
"issuetxid": "409dc914fd64e43ad667f6880276cfae1ae6c3ea92c0813a48d76f41924cf245",
"assetref": "137-267-40256",
"multiple": 1,
"units": 1,
"open": true,
"restrict": {
"send": false,
"receive": false
},
"details": {
"details": "Backed by silver jewellery held in Lot A at Zimblia office"
},
"issueqty": 19500,
"issueraw": 19500,
"subscribed": true,
"synchronized": true,
"transactions": 7,
"confirmed": 7,
"issues": [
  {
"txid": "409dc914fd64e43ad667f6880276cfae1ae6c3ea92c0813a48d76f41924cf245",
"qty": 19500,
"raw": 19500,
"details": {
"details": "Backed by silver jewellery held in Lot A at Zimblia office"
},
"issuers": [
  "1Go5neH1MUtcMdFfS6U5MDYsLJ51s6ZX1gmg3e"
],
}
],
},
  {
"name": "GOLD-tokens-series-B",
"issuetxid": "7df309886ba8fa220c3be3f4e24c763bb5ac6cc01063aa089b55cf4a64f68a63",
"assetref": "144-266-62333",
"multiple": 1,
"units": 1,
"open": true,
"restrict": {
"send": false,
"receive": false
},
"details": {
"details": "Backed by Gold jewellery held in Lot B at Zimblia office"
},
"issueqty": 24500,
"issueraw": 24500,
"subscribed": true,
"synchronized": true,
"transactions": 2,
"confirmed": 2,
"issues": [
  {
"txid": "7df309886ba8fa220c3be3f4e24c763bb5ac6cc01063aa089b55cf4a64f68a63",
"qty": 19500,
"raw": 19500,
"details": {
"details": "Backed by Gold jewellery held in Lot B at Zimblia office"
},
"issuers": [
  "1Go5neH1MUtcMdFfS6U5MDYsLJ51s6ZX1gmg3e"
],
},
  {
"txid": "113233f116656c8c7b866e87e904cd419ccbf69934e16adf31d1a9c8c3eddf61",
"qty": 5000,
"raw": 5000,
"details": {},
"issuers": [
  "1Go5neH1MUtcMdFfS6U5MDYsLJ51s6ZX1gmg3e"
],
}
],
},
  {
"name": "Invoice no. 235235",
"issuetxid": "6b8842e04d649d33a2f6cd4e632d1c61e5989dd46532a8a8eee566ee58656fbc",
"assetref": "365-515-34923",
"multiple": 1,
"units": 1,
"open": false,
"restrict": {
"send": false,
"receive": false
},
"details": {
"details": {
"invoice_amount": "USD 856,000",
"invoice_maturity": "10-April-2019",
"invoice_description": "This is optional additional information about the invoice."
}
},
"issueqty": 1,
"issueraw": 1,
"subscribed": true,
"synchronized": true,
"transactions": 1,
"confirmed": 1,
"issues": [
  {
"txid": "6b8842e04d649d33a2f6cd4e632d1c61e5989dd46532a8a8eee566ee58656fbc",
"qty": 1,
"raw": 1,
"details": {
"details": {
"invoice_amount": "USD 856,000",
"invoice_maturity": "10-April-2019",
"invoice_description": "This is optional additional information about the invoice."
}
},
"issuers": [
  "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp"
],
}
],
}
],
}
```

### 6.4 Bidding by investors
Investors place bids on invoices. To place a bid on an invoice, the investor must hold sufficient quantity of fiat currency  tokens (token). These tokens are issued by banks against fiat currency deposits held by them. Investors can purchase these tokens from their banks. Once an investor places a bid, the relevant amount of tokens are ‘locked’ and 'un-spendable' till either:
* the supplier (payee) rejects the bid or    
* the investor cancels his bid   

To create a bid, the investor uses `post /api/v1/create_bid` and passes these parameters:
1. `from_address` - the primechain address of the investor
2. `to_address` - the primechain address of the payee
1. `invoice_reference_number` - the reference number of the invoice
2. `token` - name of the fiat currency token
3. `token_amount` - quantity of the fiat currency token being offered in return for the invoice

Sample input
```
{
  "from_address": "1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
  "to_address": "1HhDFkG6erh3cusjY1M8tgEQr3dhTM8Dh71Pmr",
  "invoice_reference_number": "4607-266-27124",
  "token": "Global-Bank-USD",
  "token_amount": 100
}
```
The following gets published to the `OFFER_DETAIL_STREAM` data-stream:
1. The primechain address of the bidder
2. Reference number of the invoice
3. Name of the fiat currency token 
4. Quantity of the fiat currency token offered for the invoice
5. A hexadecimal representation of the bid

The output is the id of the transaction in which the bid information is stored in the blockchain.

Sample output
```
{
  "status": 200,
  "tx_id": "950e37cc585dc6437e95ef9d37956513daa9b83f0438fbf49a82f6c2e861e907"
}
```

### 6.5 Cancelling of bids by investors
To cancel a bid, the investor uses `post /api/v1/cancel_bid` and passes 1 parameter - the id of the transaction in which the bid information is stored in the blockchain:

Sample input
```
{
  "tx_id": "9acbe1619a749f0f690e65ae4e7836c56a9e923705119563c1351b7601ec3998"
}
```
Sample output
```
{
"status": 200,
"response": true
}
```

### 6.6 Viewing bids
All participants can view all bids placed on all invoices using `get /api/v1/view_all_bids`. This creates a highly transparent platform and enables price discovery.

Sample output
```
{
"status": 200,
"all_bid_details": [
  {
"from_address": "1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
"to_address": "1HhDFkG6erh3cusjY1M8tgEQr3dhTM8Dh71Pmr",
"invoice_reference_number": "4607-266-27124",
"token": "lite_coin_8763737",
"token_amount": 10,
"txid": "110f4b14f225789b22db9676470898ca6d32e6f8af0d5ccd30a4ebfa6d6397af",
"vout": 0,
"offer_blob": "0100000001af97636dfaeba430cd5c0daff8e6326dca9808477696db229b7825f2144b0f11000000006a4730440220736c0d78bcb3e27a27891485867c32422b4533f88005a76d33e95d8f3584afb502201e815010859e02ab055b7405c41b80903683c21fe495f673ab2d0d73216a4ed6832102ae5cc5f1f9e1557bf3323dae43afdad30a0cbd8c3738ca4a6d0b6127484c063affffffff0100000000000000003776a914fc94b1fcb15f639eef422098fdd415167740831788ac1c73706b712d3aad14eaa2d1925b57b995716a69f401000000000000007500000000"
}
],
}
```
To view bid details for a specific invoice, use `post /api/v1/view_bid` and pass the invoice reference number as a parameter.

Sample input
```
{
  "invoice_reference_number": "4607-266-27124"
}
```
Sample output
```
{
"status": 200,
"response": [
  {
"from_address": "1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
"to_address": "1HhDFkG6erh3cusjY1M8tgEQr3dhTM8Dh71Pmr",
"invoice_reference_number": "4607-266-27124",
"token": "lite_coin_8763737",
"token_amount": 100,
"txid": "602dceb782166d222c6fed8470feaa62fd3b66b0bfcef2a91f729684b46222a6",
"vout": 0,
"offer_blob": "0100000001a62262b48496721fa9f2cebfb0663bfd62aafe7084ed6f2c226d1682b7ce2d60000000006b483045022100ee606fc93d4d04298d04551b4c60893a7c0bab2cd92ad815b404d8210d6bb9ce02205ccbd2ec2db9a1b4a2b90edae48a5ce868b1d91bcc8e9d08d37680a37aaaa827832102ae5cc5f1f9e1557bf3323dae43afdad30a0cbd8c3738ca4a6d0b6127484c063affffffff0100000000000000003776a914fc94b1fcb15f639eef422098fdd415167740831788ac1c73706b712d3aad14eaa2d1925b57b995716a69f401000000000000007500000000"
}
],
}

```

### 6.7 Rejection of bids
A supplier (payee) can reject bids made on invoices in which she is the payee. To reject a bid, use `post /api/v1/reject_bid` and pass the following parameters:   
1. transaction id of the bid   
2. primechain address of the payee   

Sample input
```
{
  "tx_id": "9acbe1619a749f0f690e65ae4e7836c56a9e923705119563c1351b7601ec3998",
  "primechain_address": "1HhDFkG6erh3cusjY1M8tgEQr3dhTM8Dh71Pmr"
}
```
Sample output
```
{
"status": 200,
"response": true
}
```

### 6.8 Acceptance of bids
A supplier (payee) can accept bids made on invoices in which she is the payee. If she accepts the bid, the invoice is transferred to the relevant investor and the bid amount of the tokens is transferred to her. She can redeem the tokens from the bank. To accept a bid, use `post /api/v1/accept_bid` and pass the following parameters:   
1. transaction id of the bid   
2. primechain address of the payee   

Sample input
```
{
  "tx_id": "ce1a7475c8419ad3a30ef9db98d7219aa72221fe9fe2cae8f652a690efda80fa",
  "primechain_address": "1HhDFkG6erh3cusjY1M8tgEQr3dhTM8Dh71Pmr"
}
```
Sample output
```
{
"status": 200,
"tx_id": "1b1cd89ebd0b813780ffc0d39361ab4711a92e97ad6073304cb4909083268f71"
}
```

### 6.9 Buyback of the invoice upon maturity of invoice
Upon maturity of the invoice, or any time before that, the payer of an invoice places a bid to purchase the invoice from the investor holding the invoice. To place this bid, the payer must hold sufficient quantity of fiat currency tokens (token). These tokens are issued by banks against fiat currency deposits held by them. Payers can purchase these tokens from their banks. 

To create a bid, use `post /api/v1/create_bid` and to accept the bid, use `post /api/v1/accept_bid` as explained in the sections above.

The invoice gets transferred to the payer and the investor receives the bid amount of the tokens. The investor can redeem the tokens from the bank.


### 6.10 Retiring the invoice
The corporate (payer) then retires the invoice using `post /api/v1/retire_invoice` and passing the invoice reference number as a parameter. 

Sample input
```
{
  "invoice_reference_number": "aaa"
}
```
Sample output
```
{
  "status": 200,
  "tx_id": "93bf243e60a029430ccca38f2e2165b16e5ee9e8fa516ea2552144de089f0a4b"
}

```

## 7. Auction platform for goods and freight contracts
---
Have a query? Email us on info@primechain.in
