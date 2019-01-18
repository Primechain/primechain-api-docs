# Factoring and invoice discounting platform

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

TRADE-Chain provides a secure and transparent real-time factoring / invoice discounting platform.

![Trade documents issuance and sharing](http://www.primechaintech.com/img/api_documentation/factoring.png)

***Table of contents***   
[1. Process flow](#1-process-flow)   
[2. Publishing a new invoice](#2-publishing-a-new-invoice)   
[3. Viewing invoices](#3-viewing-invoices)   
[4. Bidding by investors](#4-bidding-by-investors)   
[5. Cancelling of bids by investors](#5-cancelling-of-bids-by-investors)   
[6. Viewing bids](#6-viewing-bids)   
[7. Rejection of bids](#7-rejection-of-bids)   
[8. Acceptance of bids](#8-acceptance-of-bids)   
[9. Buyback of the invoice upon maturity of invoice](#9-buyback-of-the-invoice-upon-maturity-of-invoice)   
[10. Retiring the invoice](#10-retiring-the-invoice)

# 1. Process flow

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

# 2. Publishing a new invoice
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
  "invoice_payer": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
  "invoice_payee": "125LHLRKDDdaJSWXbVdaAGG7pGRT9dWPjjF7aG",
  "invoice_name": "Invoice no. 23523561",  
  "invoice_details": 
    {
      "invoice_amount": "USD 856,000",
      "invoice_maturity": "10-April-2019",
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
   "response": 
      {
         "tx_id": "ec106e10a7dcc69ed8e481be34d46b83e7f329a449755cd81b8d066b4e766fff",
         "invoice_reference_number": "700-267-4332",
         "invoice_details": 
            {
               "details": 
                  {
                     "invoice_amount": "USD 856,000",
                     "invoice_maturity": "10-April-2019",
                     "invoice_description": "This is optional additional information about the invoice."
                  }
            }
      }
}
```

# 3. Viewing invoices
Participants, especially investors, view invoices. This list of invoices can be filtered based on payer, payee, maturity date and value. To view all the invoices, use `get /api/v1/view_all_invoices`.

# 4. Bidding by investors
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
The following gets published to the `OFFER_DETAIL_REPOSITORY`:
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
***Note:*** This transaction id is critical for the discounting process.

# 5. Cancelling of bids by investors
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

# 6. Viewing bids
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

# 7. Rejection of bids
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

# 8. Acceptance of bids
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

# 9. Buyback of the invoice upon maturity of invoice
Upon maturity of the invoice, or any time before that, the payer of an invoice places a bid to purchase the invoice from the investor holding the invoice. To place this bid, the payer must hold sufficient quantity of fiat currency tokens (token). These tokens are issued by banks against fiat currency deposits held by them. Payers can purchase these tokens from their banks. 

To create a bid, use `post /api/v1/create_bid` and to accept the bid, use `post /api/v1/accept_bid` as explained in the sections above.

The invoice gets transferred to the payer and the investor receives the bid amount of the tokens. The investor can redeem the tokens from the bank.


# 10. Retiring the invoice
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
