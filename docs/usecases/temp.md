# Trade Finance

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

intro to trade finance

![Letter of credit](http://www.primechaintech.com/img/api_documentation/trade-finance.jpg)

***Table of contents***   

***[1. Preliminary steps](#1-preliminary-steps)***   
[1.1 Generate API keys](#11-generate-api-keys)      
[1.2 Create an address whose private key is stored on the blockchain](#12-create-an-address-whose-private-key-is-stored-on-the-blockchain)   

***[2. Create a dedicated Data Stream](#2-create-a-dedicated-data-stream-for-a-specific-transaction,-shipment-or-event)***    
[2.1 Create a data stream](#21-create-a-data-stream)   
[2.2 Grant write permissions](#22-grant-write-permissions)   
[2.3 Revoke write permissions](#23-revoke-write-permissions)   

***[3. Publish data to the blockchain](#3-publish-data-to-the-blockchain)***   
[3.1 Publish an invoice](#31-publish-an-invoice)   
[3.2 Publish a bank guarantee](#32-publish-a-bank-guarantee)   
[3.3 Publish a letter of credit](#33-publish-a-letter-of-credit)   
[3.4 Publish a bill of lading](#34-publish-a-bill-of-lading)

***[4. Retrieve data from the blockchain](#4-retrieve-data-from-the-blockchain)***   

***[5. Invoice discounting](#5-invoice-discounting)***   

***[6. Publish GPS information and data in real-time](#6-publish-gps-information-and-data-in-real-time)***

***[7. Settle accounts in real-time](#7-settle-accounts-in-real-time)***


## 1. Preliminary steps
TRADE-Chain nodes are available to banks, financial institutions and large exporters, importers and shippers. The  preliminary steps to be carried out by node holders are:

### 1.1 Generate API keys
API keys authenticate access to the TRADE-Chain API service. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header.

Sample API key
```
k3wq1TdYcEGb7sqX&Es8-xVR$ocdw5ICLtIh5rT661UDaZoKmLV!12X01ce!GnEW
```

### 1.2 Create an address whose private key is stored on the blockchain
To create an address whose private key is stored on the blockchain, use `get /api/v1/create_entity`.

The output will be the blockchain address of the newly created entity. The private key is automatically stored in your node. This will not be visible to other nodes. 

Sample output
```
{
"status": 200,
"primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp"
}
```

## 2. Create a dedicated Data Stream
A data stream enables TRADE-Chain to be used as a general purpose append-only database, with TRADE-Chain providing timestamping, notarization and immutability. Storing all the data relating to a transaction, shipment or event in a dedicated data stream enables quick and efficient data retrieval and processing.

### 2.1 Create a data stream
To create a new data stream use `post /api/v1/create_data_stream` and provide these 4 parameters:
1. The creators address
2. The stream name
3. A short description of the data stream
4. Whether the stream is open or not. If open is set to true, write permissions need not be explicitly provided. All addresses can write to the stream. If open is set to false, write permissions need to be explicitly provided. It is recommended to keep the stream as closed and to provide write permissions on an address basis. 

Sample input
```
{
  "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
  "stream_name": "200_tons_xyz_Jan_2019",
  "details": "This stream is for the consignment of 200 tons of xyz material",
  "open":false
}
```
The output is the txid of the transaction creating the stream.
Sample output
```
{
"status": 200,
"tx_id": "d84f84849431d5a5c5565530021d4c8bc37bf7180c58a116bd42295f90b434e2"
}
```

### 2.2 Grant write permissions
To grant an entity write permission to a stream, use `post /api/v1/grant_write_permission_to_stream` and provide 3 parameters:
1. The primechain addresss of the entity to be granted write permission - `primechain_address_stream_writer`
2. The name of the relevant data stream - `stream_name`
3. The primechain addresss of the creator of the data stream - `primechain_address_stream_creator`

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
1. The primechain addresss of the entity whose write permission is to be revoked - `primechain_address_stream_writer`
2. The name of the relevant data stream - `stream_name`
3. The primechain addresss of the creator of the data stream - `primechain_address_stream_creator`

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

## 2. On-board relevant exporters, importers, shippers etc.

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
"response": {
"primechain_address": "1BiWh3dEMEDVRHNTsrYf7MCHHfXP2qL6or34PP",
"primechain_private_key": "VHpUJD5NkTrurFHEoQ79t55TUAgZYEFvygbZHSCJ3za6zSwtXbQqVsaV",
"primechain_public_key": "03fe0f7af92c260c0098dcf9818eb9b6998584d7cb68a776d7b9e63aa5ad16b53b",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCQPcJ5wYOPptDb LMnPDSjWlOdvlf8dQ6GOEQ9XDqk3iEiLl0kf9FaMG9Nzq12yVB5ZHpHWlDjyx45q d42ya+0d6AcyJlB/0z/vCLg0hFBA5A+EZBHXVnIVJzEoCOrQzpI3YMM35u6XsgYB nKir53M12IOUZ114DGSgkIiXqN6F7/6P6Zr2ZdaCTL95iXFiSKGcFlN9UTPYXghF kw1u1A0cv2ns6v/sfsCY10BjK8AXcuDaS5mg2vlFwuyUGjOQ4MXZwouHgKw5lIlE J46zxsDjpJHSrODkvqb/Y3GWuUx4evu3NoJ3mKq6DzHd9k5kPvHF2L9EFYrnP0nj KTjXqru7AgMBAAECggEAeCVJYVukNzrPS1EyRCoE80ASyuqZFoon/osNSQmoP95f 9w4r1dcTZB8lcXqzUAArSzZgaekKyocYhGxS9eRaHQgRPl+Vu/N9lKChtvTjWDnf BvrHtaOG4UHE+0D6PrViK4iI836DDI433I3eHVprp9VSPIIg5AcGpovdit4ZhFvS GwfFD2IQ61H/JgWei0n34tUEbRGYODhNaGPgTyCEZ1+rx1+HOS30K80TVChADuSw aNTDnYPzPpOsihHN/TllydtsX92Yavg3XzQZTbrRAQhblSRlCJHALJRJErcH1g3T PiwnvAcx9If4O4f3EwT/XslWSPY+T+eBZGaUtq0zUQKBgQDZLW3UoMAaUeIosM5Q /RGBYxNxu2qotNm3fKSMNTzB05DYDKYKyj1XtW448DVm9srFYJ67N/EK9yDKR59O 9aj+VPyAP7FWmyp8sJA8e+GjRIDvPeRoyr5pVBwK1Q0BYLmDI5MNiggBbFO+DBHu swylORd7c37WKdfJSSc6lWsy4wKBgQCqBpdxYcYqucLBemDeOJPRyRqiKCSUqzn3 85FtXoW3CzQ177rAp2uWFA8VCKHs1u7NLOuBayvo68lbbuebVgaffxpX0WSp6VnV 6tpPQCmDvisj5iIs7ETiNNm93ZvBWFek8xpEl26FbfgFAw1YCfEipjwfV6t6x9Do qzDJDxIzSQKBgQCUAGeWva3swdy0Cjmv66agXFqF6Uj4i7bLWn/wpN8w3/MXqRcG x2gie5wP5XMfJhRtijjiMW9tH5kTANhKQRPXryccZ0t9T+UWcGT7MxlD4I1VfQJJ f9FfilhJ8YMZa0dBXV77nRNzlNVE8IjP+OknN88O7FiFrqJFpDq9q9IQLQKBgDk/ 3PBlfqdWQxiIj2Nj44oIz/n30FFq0isGDVqpMBbxI9Rhcx15ggVXnbh0XqlzuZbG YEoEfxV/hx5NWpj4P2SnFISrUdzQYNphqL50mUXt23LMA4fiylLsfsCqhM52Y5R7 8sVTw/gTjiaJ341cU6BaHvZiu6+s5k/hjJy2gWdZAoGBAJMAcDfRnLDKMV5wiC4V ARxrXfmZdJhfoNRb9O4VOin+OkO+NQOdHi1ECA6mMMdAm1iHNDIep2nQlXLcp2K2 jzjD/lszxp5JHkoGWGEQi5l8FdHimgmRRg7GnNeui1cKJ9yAg+EgP4kflBOu/F66 vkIg4N6DI/lVIbvVbihIyITM -----END PRIVATE KEY-----",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkD3CecGDj6bQ2yzJzw0o 1pTnb5X/HUOhjhEPVw6pN4hIi5dJH/RWjBvTc6tdslQeWR6R1pQ48seOaneNsmvt HegHMiZQf9M/7wi4NIRQQOQPhGQR11ZyFScxKAjq0M6SN2DDN+bul7IGAZyoq+dz NdiDlGddeAxkoJCIl6jehe/+j+ma9mXWgky/eYlxYkihnBZTfVEz2F4IRZMNbtQN HL9p7Or/7H7AmNdAYyvAF3Lg2kuZoNr5RcLslBozkODF2cKLh4CsOZSJRCeOs8bA 46SR0qzg5L6m/2NxlrlMeHr7tzaCd5iqug8x3fZOZD7xxdi/RBWK5z9J4yk416q7 uwIDAQAB -----END PUBLIC KEY-----"
}
}
```

## 3. Publish data to the blockchain

`post /api/v1/publish_data`
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

### 3.1 Publish an invoice

### 3.2 Publish a bank guarantee

### 3.3 Publish a letter of credit

### 3.4 Publish a bill of lading


## 4. Retrieve data from the blockchain


## 5. Invoice discounting


## 6. Publish GPS information and data in real-time


## 7. Settle accounts in real-time


Have a query? Email us on info@primechain.in
