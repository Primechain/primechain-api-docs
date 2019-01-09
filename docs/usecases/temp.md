# Trade Finance

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

intro to trade finance

![Letter of credit](http://www.primechaintech.com/img/api_documentation/trade-finance.jpg)

***Table of contents***   

***[1. Generate API keys](#1-generate-api-keys)***   

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


## 1. Generate API keys
API keys authenticate access to the TRADE-Chain API service. To generate an API key, use `get api/v1/get_api_key`. An API key must be passed in the authorization header.

Sample API key
```
k3wq1TdYcEGb7sqX&Es8-xVR$ocdw5ICLtIh5rT661UDaZoKmLV!12X01ce!GnEW
```

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
The output is the txid of the transaction creating the stream.
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
"response": {
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
1. the private key of the signer
2. the primechain address of the signer
3. The keys to enable quick searching of the data 
4. the data
5. the name of the data stream

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

### 4.2 Publish a bank guarantee

### 4.3 Publish a letter of credit

### 4.4 Publish a bill of lading


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
