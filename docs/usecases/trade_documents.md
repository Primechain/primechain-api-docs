# Trade documents

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

Blockchain provides a secure and transparent platform for issuance and sgaring of trade documents.

***Table of contents***

[1. Commercial Invoice](#1-commercial-invoice)   
[2. Letter of credit](#2-letter-of-credit)   
[3. Straight Bill of Lading](#3-straight-bill-of-lading)

## 1. Commercial Invoice

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

## 2. Letter of credit
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

## 3. Straight Bill of Lading

Sample input
```
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
      "CERTIFICATION_HAZARDOUS_MATERIAL": "If the shipments is of hazardous material, add - THIS IS TO CERTIFY THAT THE ABOVE-NAMED MATERIALS ARE PROPERLY CLASSIFIED, DESCRIBED, PACKAGED, MARKED AND LABELED AND ARE IN PROPER CONDITION FOR TRANSPORTATION ACCORDING TO THE APPLICABLE REGULATIONS OF THE DEPARTMENT OF TRANSPORTATION.",
}
```
