# Trade Finance

[![Primechain Technologies](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)
[![TRADE-Chain brochure](https://img.shields.io/badge/Download-Brochure-green.svg)](http://www.primechaintech.com/docs/brochures/Trade_Chain.pdf)

The market for trade finance is above US$ 12 trillion annually. TRADE-Chain is a permissioned "global trade finance" blockchain for the world’s banks and financial institutions. TRADE-Chain nodes are available to banks, financial institutions and large exporters, importers, shippers and investors.

![Letter of credit](http://www.primechaintech.com/img/api_documentation/trade-finance.jpg)

### Table of contents  

***[1. Introduction and overview](#1-introduction-and-overview)***   
[1.1 Sandbox blockchain](#11-sandbox-blockchain)    
[1.2 Production blockchain](#12-production-blockchain)    
[1.3 System requirements for nodes](#13-system-requirements-for-nodes)   
[1.4 Information Security issues](#14-information-security-issues)   
[1.5 API keys for sandbox](#15-api-keys-for-sandbox)   
[1.6 Default address for a node](#16-default-address-for-a-node)   
[1.7 Additional addresses](#17-additional-addresses)

***[2. Data Streams and permissions to write to them](#2-data-streams-and-permissions-to-write-to-them)***    
[2.1 Create a new data stream](#21-create-a-new-data-stream)   
[2.2 Grant write permissions](#22-grant-write-permissions)   
[2.3 Revoke write permissions](#23-revoke-write-permissions)   

***[4. Publish data to a Data Stream](#4-publish-data-to-a-data-stream)***   
[4.1 Encrypt, sign and publish data](#41-encrypt-sign-and-publish-data)   
[4.2 Publish an invoice](#42-publish-an-invoice)   
[4.3 Publish a bank guarantee](#43-publish-a-bank-guarantee)   
[4.4 Publish a letter of credit](#44-publish-a-letter-of-credit)   
[4.5 Publish a bill of lading](#45-publish-a-bill-of-lading)   
[4.6 Publish GPS data](#46-publish-gps-data)   

***[5. Decrypt, verify and retrieve data from the blockchain](#5-decrypt-verify-and-retrieve-data-from-the-blockchain)*** 

***[6. Invoice discounting](#6-invoice-discounting)***   
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

***[7. Settle accounts in real-time](#7-settle-accounts-in-real-time)***


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
* Ubuntu 16.04 machine with 32 GB RAM, 4 core processor, 100 GB SSD disk). The following ports are required to be open: 22. 15590 and 61172.   
* Ubuntu 16.04 machine with 32 GB RAM, 8 core processor, 25 GB SSD disk). The following ports are required to be open: 22 and 2512.

### 1.4 Information Security issues
* Symmetric and asymmetric cryptography ensures ***confidentiality*** of data.   
* Hash functions ensure ***integrity*** of data.   
* Multiple blockchain nodes ensure ***availability*** of data.   
* Blockchain technology ensures provable ***immutability*** of data.   
* Digital signatures ensure ***non-repudiation***.   
* [Blockchain Security Controls](http://www.primechaintech.com/bsc.php) provide the security controls and information security framework.

### 1.5 API keys for sandbox
API keys authenticate access to the TRADE-Chain sandbox. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header. ([See example](https://camo.githubusercontent.com/c3e402907d4735fa944e79888ddc58209247e07e/687474703a2f2f7777772e7072696d65636861696e746563682e636f6d2f696d672f6170695f646f63756d656e746174696f6e2f6170695f6b65792e6a7067))

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

## 2. Data Streams and permissions to write to them
A data stream enables TRADE-Chain to be used as a general purpose append-only database, with TRADE-Chain providing timestamping, notarization and immutability. Storing all the data relating to a transaction, shipment or event in a dedicated data stream enables quick and efficient data retrieval and processing.

### 2.1 Create a new data stream
To create a new data stream use `post /api/v1/create_data_stream` and provide these 4 parameters:
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

}
```

## 4. Publish data to a Data Stream

### 4.1 Encrypt, sign and publish data
To encrypt, sign and publish data to a Data Stream, use `post /api/v1/publish_data` and pass 5 parameters: 
1. `primechain_private_key` - the private key of the signer.
2. `primechain_address` - the primechain address of the signer.
3. `keys` - the keys to enable quick searching of the data.
4. `data` - the data. 
5. `stream_name` - the name of the data stream.

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
4. The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: the encrypted version of the data, the AES password, the Initialisation Vector (IV) and the Authentication Tag (tag).
5. The encrypted data and the tag are published to the data stream.

***The following is the output:***
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the data stream.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the the data stream.
3. `signature` - the digital signature
4. `aes_password` - the AES password
5. `aes_iv` - the Initialization Vector (IV)
6. `stream_name` - the data-stream name

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
### 4.2 Publish an invoice
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

### 4.3 Publish a bank guarantee
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
### 4.4 Publish a letter of credit
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

### 4.5 Publish a bill of lading
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

### 4.6 Publish GPS data

It is recommended to use National Marine Electronics Association (NMEA) formatted Global Positioning System (GPS) data

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

## 5. Decrypt, verify and retrieve data from the blockchain
To retrieve data use `post /api/v1/get_data` and pass 5 parameters:
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the data stream.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the data stream.
3. `aes_password` - the AES password.
4. `aes_iv` - the Initialization Vector (IV).
5. `stream_name` - the name of the data stream.

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
      // timestamp 
      }
}
```

## 6. Invoice discounting

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
    * `invoice_amount` - the amount of the invoice.
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
     },
}
```
***Note:*** This may take upto 30 seconds.   

***Output is:***
* the id of the transaction in which the invoice was published to the blockchain - `tx_id`.
* the reference number of the asset - `invoice_reference_number`

Sample output
```
{
  "status": 200,
  "tx_id": "aaa",
  "invoice_reference_number": "aaa",
}
```

### 6.3 Viewing invoices



### 6.4 Bidding by investors
Investors place bids on invoices. To place a bid on an invoice, the investor must hold sufficient quantity of fiat currency  tokens (token). These tokens are issued by banks against fiat currency deposits held by them. Investors can purchase these tokens from their banks. Once an investor places a bid, the relevant amount of tokens are ‘locked’ and 'un-spendable' till either (1) the supplier (payee) rejects the bid or (2) the investor cancels his bid.

To create a bid, the investor uses `create_bid` and passes these parameters:
1. `invoice_reference_number` - the reference number of the invoice.
2. `token` - name of the fiat currency token.
3. `token_amount` - quantity of the fiat currency token.

Sample input
```
{
  "invoice_reference_number": "aaa",
  "token": "Global-Bank-USD",
  "token_amount": "10"
}
```
The following gets published to the `OFFER_DETAIL_STREAM`:
1. The primechain address of the bidder
2. Name of the invoice
3. Name of the fiat currency token 
4. Quantity of the fiat currency token offered for the invoice
5. A hexadecimal representation of the bid

The output is the id of the transaction in which the bid information is stored in the blockchain.
```
{
  "status": 200,
  "tx_id": "aaa"
}
```

To cancel a bid, the investor uses `post /api/v1/cancel_bid` and passes 1 parameter - the id of the transaction in which the bid information is stored in the blockchain:

Sample input
```
{
  "tx_id": "aaa"
}
```

and cancelling of bids 

### 6.5 Cancelling of bids by investors


### 6.6 Viewing bids
All participants can view all bids placed on all invoices using `get /api/v1/view_all_bids`. This creates a highly transparent platform and enables price discovery.

Sample output
```
aa
```
To view bid details for a specific invoice, use `post /api/v1/view_bid` and pass the invoice reference number as a parameter.

Sample input
```
{
  "invoice_reference_number": "aaa"
}
```
Sample output
```
aa
```

A supplier (payee) can accept or reject bids made on invoices in which she is the payee. If she accepts the bid, the invoice is transferred to the relevant investor and the bid amount of the tokens is transferred to her. She can redeem the tokens from the bank.

### 6.7 Rejection of bids


To accept a bid, use `post /api/v1/accept_bid` and pass the transaction id of the bid as a parameter:

Sample input
```
{
  "tx_id": "aaa"
}
```
Sample output
```
aaa
```
To reject a bid, use `post /api/v1/reject_bid` and pass the transaction id of the bid as a parameter:

Sample input
```
{
  "tx_id": "aaa"
}
```
Sample output
```
aaa
```

### 6.8 Acceptance of bids


### 6.9 Buyback of the invoice upon maturity of invoice
Upon maturity of the invoice, or any time before that, the payer of an invoice places a bid to purchase the invoice from the investor holding the invoice. To place this bid, the payer must hold sufficient quantity of fiat currency tokens (token). These tokens are issued by banks against fiat currency deposits held by them. Payers can purchase these tokens from their banks. 

To create a bid, the payer uses `create_bid` and passes these parameters:
1. `invoice_reference_number` - The reference number of the invoice.
2. `token` - Name of the fiat currency token.
3. `token_amount` - Quantity of the fiat currency token.

Sample input
```
{
  "invoice_reference_number": "aaa",
  "token": "Global-Bank-USD",
  "token_amount": "10"
}
```
The following gets published to the `OFFER_DETAIL_STREAM`:
1. The primechain address of the bidder
2. Name of the invoice
3. Name of the fiat currency token 
4. Quantity of the fiat currency token offered for the invoice
5. A hexadecimal representation of the bid

The output is the id of the transaction in which the bid information is stored in the blockchain.
```
{
  "status": 200,
  "tx_id": "aaa"
}
```
To accept the bid, the investor uses `post /api/v1/accept_bid` and passes the transaction id of the bid as a parameter:

Sample input
```
{
  "tx_id": "aaa"
}
```
Sample output
```
aaa
```
The invoice gets transferred to the payer and the investor receives the bid amount of the tokens. The investor can redeem the tokens from the bank.


### 6.10 Retiring the invoice
The corporate (payer) then retires the invoice using `post /api/v1/retire_invoice` and passing the invoice reference number as a parameter. 

Sample input
```
{
  "invoice_reference_number": "aaa"
}
```
The corporate (payer) can redeem the tokens with the relevant bank.

---
Have a query? Email us on info@primechain.in
