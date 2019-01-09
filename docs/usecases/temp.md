# Trade Finance

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

intro to trade finance

![Letter of credit](http://www.primechaintech.com/img/api_documentation/trade-finance.jpg)

***Table of contents***   

***[1. Preliminary steps](#1-preliminary-steps)***   
[1.1 Generate API keys](#11-generate-api-keys)      
[1.2 Create an address whose private key is stored on the blockchain](#12-create-an-entity-whose-private-key-is-stored-on-the-blockchain)   

***[2. Create a dedicated Data Stream](#2-create-a-dedicated-data-stream-for-a-specific-transaction,-shipment-or-event)***    
[2.1 Create a data stream](#21-create-a-data-stream)   
[2.2 Grant write permissions](#22-grant-write-permissions)   
[2.3 Revoke write permissions](#23-revoke-write-permissions)   

***[3. Publish relevant data to the blockchain](#3-publish-relevant-data-to-the-blockchain)***   
[3.1 Publish an invoice](#31-publish-an-invoice)   
[3.2 Publish a bank guarantee](#32-publish-a-bank-guarantee)   
[3.3 Publish a letter of credit](#33-publish-a-letter-of-credit)   
[3.4 Publish a bill of lading](#34-publish-a-bill-of-lading)

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

To on-board relevant exporters, importers, shippers etc. use `get /api/v1/create_keypair`. The output will be:
1. the primechain address, 
2. primechain public key and 
3. primechain private key

Sample output
```
{
  "status": 200,
  "response": 
    {
      "primechain_private_key": "VCYNEaX1HuvxM56D69ULvNbR6H1Rcae6EbobiKr4PDYdYPs9NJq5C2yk",
      "primechain_address": "125LHLRKDDdaJSWXbVdaAGG7pGRT9dWPjjF7aG",
      "primechain_public_key": "02d80c774feea05859a3701c927a0d4b87b01654f75cbd57f49d673a03d94f69a1"
    }
}
```



## 3. Publish relevant data to the blockchain
```
{
  "rsa_pub_key_id": "5c3492873cf18b37aec45abe",
  "encrypted_private_key": "e2M+9kEuPhEAijGlHn/auxLT2RPHJToiq1GcjaTaJVrn0N3aX0q59mFHKW3dVJtxW4/B99h0o0LF4s7/BZ0FEOAhmQfyoAmSnnhzoh6nb5ZleGO/Dwq35AHDQxY660gFn2lf8yG3IWQ2RIHemy32t4lYKY/0RKN4ZVr3uj9MnWabdLbM6hBThEDSVcwa9XDjEKbi16JZSjrR85mIN+/3ioMQvhpG4q+s9IyOcXVCXGGmJoWhtXRzH3Gl4dWnhXUwD9+grrMPXaJTHbgO9vOpLIOqSuuuZA7CzXrAS2taxP4eUmgcsOXcwQdGcPr2h8M/0USUXa+8hPnkEPcXGEYuYw==",
  "primechain_address": "1VLRwqpawyNFNn8uTYhufsK1p7HFK5KAdKhsaE",
  "keys": [
    "hello",
    "00554"
  ],
  "data": "hello world"
}
```

### 3.1 Publish an invoice

### 3.2 Publish a bank guarantee

### 3.3 Publish a letter of credit

### 3.4 Publish a bill of lading


## 4. Enable invoice discounting. 


## 5. Publish GPS information and documents in real-time.


## 6. Settle accounts in real-time without the need for manual reconciliation.


Have a query? Email us on info@primechain.in
