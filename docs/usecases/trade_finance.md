# Trade Finance

[![Primechain Technologies](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)
[![TRADE-Chain brochure](https://img.shields.io/badge/Download-Brochure-green.svg)](http://www.primechaintech.com/docs/brochures/Trade_Chain.pdf)

The market for trade finance is above US$ 12 trillion annually. TRADE-Chain is a permissioned "global trade finance" blockchain for the world’s banks and financial institutions. TRADE-Chain nodes are available to banks, financial institutions and large exporters, importers and shippers.

![Letter of credit](http://www.primechaintech.com/img/api_documentation/trade-finance.jpg)

***The pain points of today’s trade finance processes are:***
1. Delays and errors due to manual document creation and distribution
2. Invoice factoring risk
3. Delayed timeline
4. Manual AML review
5. Fraud risk due to multiple disconnected platforms
6. Fraud risk due to duplicate bills of lading

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

***Table of contents***   

***[1. Introduction and overview](#1-introduction-and-overview)***   
[1.1 Sandbox blockchain](#11-sandbox-blockchain)    
[1.2 Production blockchain](#12-production-blockchain)    
[1.3 System requirements](#13-system-requirements)   
[1.4 Information Security issues](#14-information-security-issues)   
[1.5 API keys for sandbox](#15-api-keys-for-sandbox)   

***[1.1 Generate API keys](#1-generate-api-keys)***   

***[2. Create a dedicated Data Stream](#2-create-a-dedicated-data-stream)***      

***[3. On-board users](#3-on-board-users)***

***[4. Publish data to a Data Stream](#4-publish-data-to-a-data-stream)***   
[4.1 Publish an invoice](#41-publish-an-invoice)   
[4.2 Publish a bank guarantee](#42-publish-a-bank-guarantee)   
[4.3 Publish a letter of credit](#43-publish-a-letter-of-credit)   
[4.4 Publish a bill of lading](#44-publish-a-bill-of-lading)

***[5. Retrieve data from the blockchain](#5-retrieve-data-from-the-blockchain)***   

***[6. Invoice discounting](#6-invoice-discounting)***   

***[7. Publish GPS information and data in real-time](#7-publish-gps-information-and-data-in-real-time)***

***[8. Settle accounts in real-time](#8-settle-accounts-in-real-time)***

## 1. Introduction and overview

TRADE-Chain is a permissioned multi-framework blockchain powered by Primechain APIs. TRADE-Chain nodes are available to banks, financial institutions and large exporters, importers, shippers and investors.

### 1.1 Sandbox blockchain
To access the TRADE-Chain sandbox, email us on info@primechain.in

### 1.2 Production blockchain
Nodes on the commpercial / production TRADE-Chain are available free to all Bankchain members and at an annual subscription fee for non-members. Email us on info@primechain.in for details.

### 1.3 System requirements for nodes
2 virtual machines / physical servers with the following details are required:
* Ubuntu 16.04 machine with 32 GB RAM, 4 core processor, 100 GB SSD disk). The following ports are required to be open: 22. 15590 and 61172.   
* Ubuntu 16.04 machine with 32 GB RAM, 8 core processor, 25 GB SSD disk). The following ports are required to be open: 22 and 2512.

### 1.4 Information Security issues
* Symmetric and asymmetric cryptography ensures confidentiality of data.   
* Hash functions ensure integrity of data.   
* Multiple blockchain nodes ensure availability of data.   
* Blockchain technology ensures provable immutability of data.   
* Digital signatures ensure non-repudiation.   
* [Blockchain Security Controls](http://www.primechaintech.com/bsc.php) provide the security controls and information security framework.

### 1.5 API keys for sandbox
API keys authenticate access to the TRADE-Chain sandbox. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header. ([See example](https://camo.githubusercontent.com/c3e402907d4735fa944e79888ddc58209247e07e/687474703a2f2f7777772e7072696d65636861696e746563682e636f6d2f696d672f6170695f646f63756d656e746174696f6e2f6170695f6b65792e6a7067))

Sample API key
```
k3wq1TdYcEGb7sqX&Es8-xVR$ocdw5ICLtIh5rT661UDaZoKmLV!12X01ce!GnEW
```

#### 1.6 Default address for a node and its permissions
When your node connects to TRADE-Chain, it is provided a default primechain address with relevant permissions connect, issue send, receive and permissions

## 2. Create a dedicated Data Stream
A data stream enables TRADE-Chain to be used as a general purpose append-only database, with TRADE-Chain providing timestamping, notarization and immutability. Storing all the data relating to a transaction, shipment or event in a dedicated data stream enables quick and efficient data retrieval and processing.

To create a new data stream use `post /api/v1/create_data_stream` and provide these 4 parameters:
1. Your node's default primechain address - `primechain_address`
2. The stream name - `stream_name`
3. A short description of the data stream - `details`
4. Whether the stream is open or not - `open`. If open is set to true, write permissions need not be explicitly provided. All addresses can write to the stream. If open is set to false, write permissions need to be explicitly provided. It is recommended to keep the stream as closed and to provide write permissions on an address basis. 

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

## 3. On-board users

To on-board relevant exporters, importers, shippers etc. use `get /api/v1/create_entity_rsa`. The output will be:
1. the primechain address, 
2. primechain private key
3. primechain public key, 
4. RSA private key
5. RSA public key

Sample output
```
{
  "status": 200,
  "response": 
     {
      "primechain_address": "1BiWh3dEMEDVRHNTsrYf7MCHHfXP2qL6or34PP",
      "primechain_private_key": "VHpUJD5NkTrurFHEoQ79t55TUAgZYEFvygbZHSCJ3za6zSwtXbQqVsaV",
      "primechain_public_key": "03fe0f7af92c260c0098dcf9818eb9b6998584d7cb68a776d7b9e63aa5ad16b53b",
      "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCQPcJ5wYOPptDb LMnPDSjWlOdvlf8dQ6GOEQ9XDqk3iEiLl0kf9FaMG9Nzq12yVB5ZHpHWlDjyx45q d42ya+0d6AcyJlB/0z/vCLg0hFBA5A+EZBHXVnIVJzEoCOrQzpI3YMM35u6XsgYB nKir53M12IOUZ114DGSgkIiXqN6F7/6P6Zr2ZdaCTL95iXFiSKGcFlN9UTPYXghF kw1u1A0cv2ns6v/sfsCY10BjK8AXcuDaS5mg2vlFwuyUGjOQ4MXZwouHgKw5lIlE J46zxsDjpJHSrODkvqb/Y3GWuUx4evu3NoJ3mKq6DzHd9k5kPvHF2L9EFYrnP0nj KTjXqru7AgMBAAECggEAeCVJYVukNzrPS1EyRCoE80ASyuqZFoon/osNSQmoP95f 9w4r1dcTZB8lcXqzUAArSzZgaekKyocYhGxS9eRaHQgRPl+Vu/N9lKChtvTjWDnf BvrHtaOG4UHE+0D6PrViK4iI836DDI433I3eHVprp9VSPIIg5AcGpovdit4ZhFvS GwfFD2IQ61H/JgWei0n34tUEbRGYODhNaGPgTyCEZ1+rx1+HOS30K80TVChADuSw aNTDnYPzPpOsihHN/TllydtsX92Yavg3XzQZTbrRAQhblSRlCJHALJRJErcH1g3T PiwnvAcx9If4O4f3EwT/XslWSPY+T+eBZGaUtq0zUQKBgQDZLW3UoMAaUeIosM5Q /RGBYxNxu2qotNm3fKSMNTzB05DYDKYKyj1XtW448DVm9srFYJ67N/EK9yDKR59O 9aj+VPyAP7FWmyp8sJA8e+GjRIDvPeRoyr5pVBwK1Q0BYLmDI5MNiggBbFO+DBHu swylORd7c37WKdfJSSc6lWsy4wKBgQCqBpdxYcYqucLBemDeOJPRyRqiKCSUqzn3 85FtXoW3CzQ177rAp2uWFA8VCKHs1u7NLOuBayvo68lbbuebVgaffxpX0WSp6VnV 6tpPQCmDvisj5iIs7ETiNNm93ZvBWFek8xpEl26FbfgFAw1YCfEipjwfV6t6x9Do qzDJDxIzSQKBgQCUAGeWva3swdy0Cjmv66agXFqF6Uj4i7bLWn/wpN8w3/MXqRcG x2gie5wP5XMfJhRtijjiMW9tH5kTANhKQRPXryccZ0t9T+UWcGT7MxlD4I1VfQJJ f9FfilhJ8YMZa0dBXV77nRNzlNVE8IjP+OknN88O7FiFrqJFpDq9q9IQLQKBgDk/ 3PBlfqdWQxiIj2Nj44oIz/n30FFq0isGDVqpMBbxI9Rhcx15ggVXnbh0XqlzuZbG YEoEfxV/hx5NWpj4P2SnFISrUdzQYNphqL50mUXt23LMA4fiylLsfsCqhM52Y5R7 8sVTw/gTjiaJ341cU6BaHvZiu6+s5k/hjJy2gWdZAoGBAJMAcDfRnLDKMV5wiC4V ARxrXfmZdJhfoNRb9O4VOin+OkO+NQOdHi1ECA6mMMdAm1iHNDIep2nQlXLcp2K2 jzjD/lszxp5JHkoGWGEQi5l8FdHimgmRRg7GnNeui1cKJ9yAg+EgP4kflBOu/F66 vkIg4N6DI/lVIbvVbihIyITM -----END PRIVATE KEY-----",
      "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkD3CecGDj6bQ2yzJzw0o 1pTnb5X/HUOhjhEPVw6pN4hIi5dJH/RWjBvTc6tdslQeWR6R1pQ48seOaneNsmvt HegHMiZQf9M/7wi4NIRQQOQPhGQR11ZyFScxKAjq0M6SN2DDN+bul7IGAZyoq+dz NdiDlGddeAxkoJCIl6jehe/+j+ma9mXWgky/eYlxYkihnBZTfVEz2F4IRZMNbtQN HL9p7Or/7H7AmNdAYyvAF3Lg2kuZoNr5RcLslBozkODF2cKLh4CsOZSJRCeOs8bA 46SR0qzg5L6m/2NxlrlMeHr7tzaCd5iqug8x3fZOZD7xxdi/RBWK5z9J4yk416q7 uwIDAQAB -----END PUBLIC KEY-----"
    }
}
```
## 4. Publish data to a Data Stream

To encrypt, sign anf publish data to a Data Stream, use `post /api/v1/publish_data` and pass 5 parameters: 
1. the private key of the signer - `primechain_private_key`
2. the primechain address of the signer - `primechain_address`
3. The keys to enable quick searching of the data - `keys`
4. the data - `data`
5. the name of the data stream - `stream_name`

Sample input
```
{
  "primechain_private_key": "VHpUJD5NkTrurFHEoQ79t55TUAgZYEFvygbZHSCJ3za6zSwtXbQqVsaV",
  "primechain_address": "1BiWh3dEMEDVRHNTsrYf7MCHHfXP2qL6or34PP",
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
2. The hash is signed using the provided private key (using ECDSA).
3. The digital signature, hash and the primechain address of the signer are stored in the data stream.
4. The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: the encrypted version of the data, the AES password, the Initialization Vector (IV) and the Authentication Tag (tag).
5. The encrypted data and the tag are published to the data stream.

***The following is the output:***
1. the id of the transaction in which the encrypted data and tag were published to the data stream.
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the the data stream.
3. the digital signature
4. The AES password
5. The Initialization Vector (IV)

Sample output
```
{
  "status": 200,
  "response": 
    {
      "tx_id_enc_data": "16346d48deea43865a276b5153fec90ac2ef83f146a20bf6826df995acdc5fc8",
      "tx_id_signature": "7c72b8fc633d9a091e878ef6c610e4383ca597f846092a35077374fb0accea76",
      "signature": "IGOfNLkkrioZwsA3sHnZTDWXP0LRb1OOSUo0Tu3TBKuYVIBgH7mDvIb4NE9eosNvWBYvVA50lZYzqQU1tKpL2tY=",
      "aes_password": "kfkNhEWZErbMLhtKkg6zSTy85Aq9QIJr",
      "aes_iv": "9UuZX4vgZ8r3",
      "stream_name": "200_tons_xyz_Jan_2019"
    }
}
```
### 4.1 Publish an invoice
Sample input
```
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "INVOICE_NUMBER": "Invoice number assigned by the exporter.",
      "SELLER": "Name and address of principal party responsible for effecting export.",
      "SOLD_TO": "The name and address of the person / company to whom the goods are shipped to for the designated end use",
      "SHIP_TO": "If different than (Sold To), the intermediate consignee – that is the name and address of the party who effects delivery of the merchandise to the ultimate consignee, or the party so named on the export license of the forwarding agent. The name and address of the duly authorized forwarder acting as agent for the exporter. ",
      "CUSTOMER_REFERENCE_NUMBER": "Oversees customer’s reference number.",
      "TERMS_OF_SALE": "Delivery and terms of sale agreement.",
      "TERMS_OF_PAYMENT": "Terms, conditions, and currency of settlement as agreed upon by the vendor and purchaser per the pro forma invoice, customer purchase order and / or the letter of credit.",      
      "CURRENCY_OF_SETTLEMENT": "Currency agreed upon between seller and buyer as payment.",
      "MODE_OF_SHIPMENT": "Indicate air, ocean, and surface. ",
      "ITEMS":
        {
          "ITEM_1": 
            {
               "ITEM_QUANTITY": "Record total number of units of this item",
               "ITEM_DESCRIPTION": "Record description of this item",
               "ITEM_UNIT_PRICE": "Record the unit price of the merchandise per unit of measure.",
               "ITEM_UNIT_OF_MEASURE": "Record total net weight and total gross weight in kilograms (1 kilogram = 2.2 pounds) for this item.",
               "ITEM_TOTAL_PRICE": "Record the extended value of this item"
            },
           "ITEM_2": 
            {
               "ITEM_QUANTITY": "Record total number of units of this item",
               "ITEM_DESCRIPTION": "Record description of this item",
               "ITEM_UNIT_PRICE": "Record the unit price of the merchandise per unit of measure.",
               "ITEM_UNIT_OF_MEASURE": "Record total net weight and total gross weight in kilograms (1 kilogram = 2.2 pounds) for this item.",
               "ITEM_TOTAL_PRICE": "Record the extended value of this item"
            },
        }
      "DESCRIPTION": "Provide full description of items shipped, the type of container, (carton, box, etc.) the gross weight per container, and the quantity and unit of measure of the merchandise.",
      "TOTAL_COMMERCIAL_VALUE": "Total value of the invoice.",
      "PACKAGE_MARKS": "Record in this field and on each package number (for example, “1 of 7,””3 of 7”) shippers company name, country of origin (e.g., Made in USA), destination port of entry, package weight in kilograms, package size (length x width x height) and shipper’s control number (optional). ",
      "MISCELLANEOUS_CHARGES": "Charges (packing, insurance, etc. Record any miscellaneous charges that are to be paid by customer, such as export transportation, insurance, export packaging inland freight to peer, etc.).",
      "CERTIFICATIONS": "Any certifications or declarations required of the shipper regarding any information recorded on the commercial invoice.",      
    }
}
```

### 4.2 Publish a bank guarantee
Sample input
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "GUARANTEE_NUMBER": "ASDRE76464",
      "guarantee_currency": "USD",
      "guarantee_amount_words": "Twenty Two million",
      "guarantee_amount_figures": "22,000,000.00",
      "guarantee_date_of_issue": "17-December-2018",
      "guarantee_date_of_maturity": "16-March-2019",
      "guarantee_beneficiary": "Nicole Corporation",
      "guarantee_details": "On behalf of our client, Nicole Corporation, for value received, we, Global Bank, hereby irrevocably and unconditionally and without protest or notification, promise to pay against this, our irrevocable bank guarantee, to the order of Nicole Corporation, as beneficiary, on the maturity date, the sum of Twenty Two million United States Dollars ($22,000,000.00 USD), upon their first written demand for payment hereunder. Such payment shall be made without set-off, free and clear of any deductions, charges, fees, levies, taxes or withholdings of any nature. This bank guarantee is transferable, without payment of any transfer fees. This bank guarantee is issued in accordance with the uniform customs and practices for bank guarantees, as set forth by the International Chamber of Commerce, Paris, France, latest revision of ICC 500 publication. This bank guarantee shall be governed by and construed in accordance with the laws of the Republic of India and is free and clear of any lien and encumbrances and is of non-criminal origin.",
      "authorized_bank_officer_name": "Nicole Kidman",
      "authorized_bank_officer_title": "Vice President",
      "authorized_bank_officer_telephone": "230950934545",
      "authorized_bank_officer_facsimile": "367645455624",
      "authorized_bank_officer_email": "nicole@example.com",
      "STAMP_PAPER_CERTIFICATE_NUMBER": "IN-KA56448168201790P",
      "STAMP_PAPER_STATE": "KARNATAKA",
      "STAMP_PAPER_CERTIFICATE_ISSUE_DATE": "12-03-2018",
      "GUARANTEE_VERSION": "1.0"      
    }
}
```
### 4.3 Publish a letter of credit
Sample input
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "LOC_FORM": "IRREVOCABLE",
      "LOC_NUMBER": "32453675864534",
      "LOC_DATE_OF_ISSUE": "17-DECEMBER-2018",
      "LOC_DATE_OF_EXPIRY": "16-MARCH-2019",
      "LOC_PLACE_OF_EXPIRY": "MUMBAI, INDIA",
      "LOC_APPLICANT_BANK": "GLOBAL BANK, GENEVA, SWITZERLAND",
      "LOC_APPLICANT": "NICOLE CORPORATION",
      "LOC_BENEFICIARY": "KIDMAN INC, ADELAIDE, AUSTRALIA",
      "LOC_CURRENCY": "USD",
      "LOC_AMOUNT_WORDS": "TWO MILLION",
      "LOC_AMOUNT_FIGURES": "2,000,000.00",
      "LOC_MAX_CREDIT_AMOUNT": "NOT EXCEEDING",
      "LOC_AVAILABLE_WITH": "ANY BANK",
      "LOC_AVAILABLE_BY": "BY NEGOTIATION",
      "LOC_DRAFTS_AT": "SIGHT",
      "LOC_DRAWEE": "INTERNATIONAL BANK, NEW YORK, USA",
      "LOC_PARTIAL_SHIPMENTS": "ALLOWED",
      "LOC_TRANSHIPMENT": "NOT ALLOWED",
      "LOC_FOR_TRANSPORTATION_TO": "MUMBAI, INDIA",
      "LOC_LATEST_DATE_OF_SHIPMENT": "17-JANUARY-2018",
      "LOC_DESCRIPTION_GOODS_SERVICES": "PLATINUM RODS",
      "LOC_QUANTITY_GOODS_SERVICES": "2000",
      "LOC_UNIT_PRICE_GOODS_SERVICES": "1000",
      "LOC_TRADE_TERMS": "CIF MUMBAI",
      "LOC_ORDER_NUMBER": "435346453",
      "LOC_DOCUMENTS_REQUIRED": "1.BENEFICIARY'S DRAFT AT SIGHT DRAWN ON BUYER'S BANK NAME, ADDRESS, MARKED 'DRAWN UNDER BUYER'S BANK NAME IRREVOCABLE LETTER OF CREDIT NO.XXX DATED XXX'. 2. SIGNED COMMERCIAL INVOICE IN TRIPLICATE. 3. PACKING LIST IN TRIPLICATE, INDICATING WEIGHT AND MEASUREMENT. 4. FULL SET (3 ORIGINALS AND 3 COPIES) OF CLEAN ON BOARD BILLS OF LADING MADE OUT TO ORDER OF SHIPPER AND BLANK ENDORSED MARKED 'FREIGHT PREPAID' AND NOTIFY APPLICANT. 5. INSURANCE POLICY IN DUPLICATE ENDORSED IN BLANK FOR 110 PERCENT OF THE INVOICE VALUE INCLUDING ALL RISKS, WAR CLAUSES AND S.R.C.C. 6. CERTIFICATE OF ORIGIN IN 3 ORIGINALS AND 2 COPIES ISSUED BY CHAMBER OF COMMERCE.",
      "LOC_ADDITIONAL_CONDITIONS": "THE COMPLETE SET OF ORIGINAL DOCUMENTS TO BE SENT IN ONE LOT BY THE COURIER SERVICE TO APPLIANT BANK.",
      "LOC_CHARGES": "ALL BANKING CHARGES ARE FOR BENEFICIARY'S ACCOUNT.",
      "LOC_PERIOD_FOR_PRESENTATION": "DOCUMENTS MUST BE PRESENTED WITHIN THE VALIDITY OF THIS CREDIT.",
      "LOC_CONFIRMATION_INSTRUCTIONS": "CONFIRM",
      "LOC_ADVISING_THROUGH_BANK": "STATE BANK OF ZIMBLIA, WOODFORD, ZIMBLIA",
      "LOC_SENDER_TO_RECEIVER_INFORMATION": "THIS CREDIT IS SUBJECT TO UNIFORM CUSTOMS AND PRACTICE FOR DOCUMENTARY CREDIT, 2007 REVISION, INTERNATIONAL CHAMBER OF COMMERCE PUBLICATIONS NO.600."        
    }
}
```

### 4.4 Publish a bill of lading
Sample input
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "SHIPPER": "Enter the company name and address of the shipper (consignor).",
      "POINT_OF_ORIGIN": "Enter the city, state and country of the actual shipping point.",
      "DATE_OF_SHIPMENT": "Enter the date of the shipment, the date the carrier took control of the merchandise.",
      "SHIPMENT_MODE": "Enter truck, rail, ship etc as relevant",
      "SHIPPERS_NUMBER": "Enter a unique control number to reference the shipment with the carrier.",
      "CARRIER": "Enter the name of the company that will take initial control of the shipment and cause its delivery to the consignee.",
      "AGENT_NUMBER": "Enter carrier’s control number, if known or required.",
      "CONSIGNED_TO": "Enter the full name of the final recipient of the shipment, the ultimate consignee; also enter the mailing or street address of the ultimate consignee, if different than destination, for carrier notification purposes.",
      "DESTINATION": "Enter the street address, city, zip / pin code, state and country where the carrier will make delivery to the Consignee",
      "ROUTE": "If applicable, enter the route the carrier will take to the consignee. This Field may also be used to specify docks, warehouses, etc., and to specify any intermediate carriers.",
      "DELIVERING_CARRIER": "If applicable, specify the carrier that will deliver the shipment to the ultimate consignee at the destination, but only if different than the carrier entered in CARRIER Field",
      "VEHICLE_NUMBER": "Enter any vehicle identifying numbers or initials, if applicable.",      
       "ITEMS":
        {
          "ITEM_1": 
            {
               "ITEM_NUMBER_OF_PACKAGES": "Enter the total number of packages per line item; if the packages are consolidated on a pallet or in an outer container, note this information. For example: 112 PKGS 3 Pall.",
               "ITEM_DESCRIPTION": "Enter the description of each item, noting the type of package (carton, barrel, etc.) and the quantity per package. Since the correct freight classification is essential in describing an item, there must be a separate line item for each different freight classification description. If more than one type of packaging is used per freight classification, a separate entry must be used for each type of package. Enter any special package markings, special handling requirements, and delivery instructions. Note: For hazardous material items, special provisions must be met in completing this field.",
               "ITEM_WEIGHT": "Enter the total gross weight, in pounds, for each line item. For bulk shipments, the TARE and net weights should also be referenced in the description field. For package shipments, include the weights of pallets and skids. The total weight of the merchandise should be shown after the last line item, with pallet and dunnage weights shown separately.",
               "ITEM_CLASS": "Enter either the five-digit class (per the Uniform Freight Classification or the National Motor Freight Classification) or a two-digit class rate (a percentage of the first class 100 rate) per line item. This information may be determined by contacting the carrier."
            },
           "ITEM_2": 
            {
               "ITEM_NUMBER_OF_PACKAGES": "Enter the total number of packages per line item; if the packages are consolidated on a pallet or in an outer container, note this information. For example: 112 PKGS 3 Pall.",
               "ITEM_DESCRIPTION": "Enter the description of each item, noting the type of package (carton, barrel, etc.) and the quantity per package. Since the correct freight classification is essential in describing an item, there must be a separate line item for each different freight classification description. If more than one type of packaging is used per freight classification, a separate entry must be used for each type of package. Enter any special package markings, special handling requirements, and delivery instructions. Note: For hazardous material items, special provisions must be met in completing this field.",
               "ITEM_WEIGHT": "Enter the total gross weight, in pounds, for each line item. For bulk shipments, the TARE and net weights should also be referenced in the description field. For package shipments, include the weights of pallets and skids. The total weight of the merchandise should be shown after the last line item, with pallet and dunnage weights shown separately.",
               "ITEM_CLASS": "Enter either the five-digit class (per the Uniform Freight Classification or the National Motor Freight Classification) or a two-digit class rate (a percentage of the first class 100 rate) per line item. This information may be determined by contacting the carrier."
            },
        }
      
      "WITHOUT_RECOURSE": "For prepaid shipments, leave blank. Otherwise, add - THE CARRIER SHALL NOT MAKE DELIVERY OF THE SHIPMENT WITHOUT PAYMENT OF FREIGHT AND ALL OTHERLAWFUL CHARGES.",
      "PREPAID_SHIPMENT": "Enter “Prepaid” if shipment is to be paid for by the shipper. If this field is left blank, the carrier will seek to collect the freight charges from the consignee ",
      "PREPAYMENTS_RECEIVED": "Carrier enters any payments received in advance from the shipper for the shipment.",
      "CHARGES_ADVANCED": "Carrier enters any advanced charges for the shipment, if applicable.",
      "COD_SHIPMENT": "First, check whether the freight charges are prepaid (the carrier bills the shipper) or collect (the carrier deducts the freight charges from the amount collected from the consignee). Second, enter the amount to be collected for the merchandise itself—be sure to include the freight charges. Third, enter any collection fees, if applicable. Enter total charges to be collected by carrier.",
      "SHIPMENT_DECLARED_VALUE": "When the weight charged by the carrier is dependent upon the value of the shipment, the dollar value per unit of measure (for example, $100.00/pound) must be stated by the shipper.",
      "SHIPPER_AGENT": "Enter the signature of the individual preparing the shipment for the shipper.",
      "CARRIERS_AGENT": "The carrier’s agent will sign here prior to taking control of the shipment.",
      "CERTIFICATION_HAZARDOUS_MATERIAL": "If the shipments is of hazardous material, add - THIS IS TO CERTIFY THAT THE ABOVE-NAMED MATERIALS ARE PROPERLY CLASSIFIED, DESCRIBED, PACKAGED, MARKED AND LABELED AND ARE IN PROPER CONDITION FOR TRANSPORTATION ACCORDING TO THE APPLICABLE REGULATIONS OF THE DEPARTMENT OF TRANSPORTATION."
     }
}
```

## 5. Retrieve data from the blockchain
To retrieve data use `post /api/v1/get_data` and pass 4 parameters:
1. the id of the transaction in which the encrypted data and tag were published to the data stream
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the data stream
3. the AES password
4. the Initialization Vector (IV)
5. the name of the data stream

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
1. the unencrypted data - `data`
2. the primechain address of the signer - `primechain_address`
3. the verification status of the signature - `signature_status`

Sample output
```
{
  "status": 200,
  "response": 
    {
      "data": "This is the data that will be encryptd and stored.",
      "signer_detail": 
        {
          "primechain_address": "1BiWh3dEMEDVRHNTsrYf7MCHHfXP2qL6or34PP"
         },
      "signature_status": true
      }
}
```

## 6. Invoice discounting


## 7. Publish GPS information and data in real-time


## 8. Settle accounts in real-time


Have a query? Email us on info@primechain.in
