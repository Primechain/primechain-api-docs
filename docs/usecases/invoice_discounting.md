# Invoice discounting

Invoice discounting enables suppliers to sell their invoices at a discount to investors. This enables suppliers to get faster access to money they are owed and enables buyers to get more time to pay. 

Instead of relying on the creditworthiness of suppliers (usually smaller businesses), the investors deal with buyers (usually large businesses). This can lower financing costs, optimize working capital and improve business efficiency.

Invoice discounting is also referred to as supply chain finance and factoring. 

The process involves 4 parties:
1. Bank 
2. Corporates (payer)
3. Vendor (payee)
4. Investors

## On-boarding
The bank on-boards corporates, vendors and investors using ...

## Token issuance and redemption
The bank issues tokens on the blockchain against fiat currency held by it in an escrow account. These tokens can be purchased / redeemed by investors, corporates and vendors. 

## The invoice discounting process

1. Corporate sends details of an approved invoice to its bank.

2. The bank publishes the invoice (as an asset) to the blockchain. This asset is issued to the corporate who is the payer of that particular invoice.

3. The corporate verifies the details of the asset (invoice). If it is correct, it transfers the asset (invoice) to the vendor who is the payee for that invoice. If it is incorrect, it transfers the asset (invoice) to the burn address `1XXXXXXXM4XXXXXXiqXXXXXXdyXXXXXXc7qCdr`

4. Investors place bids on the invoice. To place a bid, they must hold sufficient quantity of tokens. Once they place a bid, the relevant amount of tokens are ‘locked’ till either (1) the vendor rejects the bid or (2) the investor cancels his bid.

5. The vendor can view all bids placed on invoices in which he is the payee.

6. The vendor can accept or reject bids. If the vendor accepts the bid, the asset (invoice) is transferred to the relevant investor and the bid amount is transferred to the vendor. The vendor can redeem the tokens from the bank.

7. When the invoice matures, the corporate pays the relevant amount to the bank and receives equivalent tokens. 

8. The corporate pays the amount to the relevant investor and receives the asset (invoice) from the investor.

9. The corporate then sends the asset (invoice) to the burn address `1XXXXXXXM4XXXXXXiqXXXXXXdyXXXXXXc7qCdr`


### Bank
The bank performs the following functions:
1. Onboard corporates
2. Onboard vendors
3. Onboard investors
4. Distribute tokens against fiat currency held by it
5. Redeem tokens for fiat currency
6. Publish verified invoices to the blockchain

### Corporate (payer)
These are corporates who are customers of the Bank and who will be provided nodes through which they can publish authenticated invoices payable by them.
Publish authenticated invoices to the blockchain
View all invoices published by the corporate

### Vendor (payee):
These are vendors of the corporates. They can accept or reject offers made on the invoices payable to them.
Upload financial and business related information
1. View all published invoices in which they are payees
2. View offers on all published invoices in which they are payees
3. Accept offers on published invoices in which they are payees
4. Reject offers on published invoices in which they are payees

### Investors: These are investors who can bid to purchase invoices at a discount.

1. View all published invoices
2. Bid on published invoices
3. Cancel their own bids
4. View their bids that have been accepted by vendors
5. View their bids that have been rejected by vendors

