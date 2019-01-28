# Cargo tracking

[![Version](https://img.shields.io/badge/TRADE--Chain-v%201.0-brightgreen.svg)](https://github.com/Primechain/primechain-api-docs/blob/master/docs/usecases/trade_chain.md) [![Version](https://img.shields.io/badge/Contact-Primechain-blue.svg)](http://www.primechaintech.com/contactus.php) [![Live demo](https://img.shields.io/badge/Live-Demo-orange.svg)](http://169.63.131.117:2206/user/publish_cargo_data) 


TRADE-Chain enables real-time tracking of cargo.

![Cargo tracking](http://www.primechaintech.com/img/api_documentation/cargo.jpg)

***Table of contents***    
1. [Publishing GPS data to TRADE-Chain](#1-publishing-gps-data-to-trade-chain)   
2. [Retrieving GPS data from TRADE-Chain](#2-retrieving-gps-data-from-trade-chain)


# 1. Publishing GPS data to TRADE-Chain

To publish Global Positioning System (GPS) data for cargo, use `post /api/v1/publish_data` and pass 4 parameters:

1. `primechain_address` - the primechain address of the signer.
2. `keys` - upto 5 keys can be used to enable quick searching of the data. Each key can be upto 256 characters including blank spaces.
3. `data` - the GPS data, UNIX timestamp, etc.
4. `trade_channel_name` - the name of the trade channel to which the data is to be published.

Sample input
```
{
  "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
   "keys": 
    [
      "SS Ideal X"
    ],
   "data": 
      {
        "NMEA_GPS_DATA": "$GPGGA,181908.00,3404.7041778,N,07044.3966270,W,4,13,1.00,495.144,M,29.200,M,0.10,0000*40",
        "GPS_DATA": "18.5528145,73.7711756",
        "DATETIME": "1547821163"      
      },
   "trade_channel_name": "200_tons_unobtainium_march_2019"
}
```
***This is what happens:***   
1. The SHA-512 hash of the data is computed.
2. The hash is signed using the private key of the provided primechain address (using ECDSA).
3. The digital signature, hash and the primechain address of the signer are stored in the trade channel.
4. The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
    * the encrypted version of the data    
    * the AES password    
    * the Initialization Vector (IV)    
    * the Authentication Tag (tag)   
5. The encrypted data and the tag are published to the specified trade channel.

***The following is the output:***
1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the trade channel.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the the trade channel.
3. `signature` - the digital signature
4. `aes_password` - the AES password
5. `aes_iv` - the Initialization Vector (IV)
6. `trade_channel_name` - the name of the trade channel to which the data is published. 

Sample output
```
{
"status": 200,
"response": {
"tx_id_enc_data": "a3187d4f3b54360538036f1a9e8c9e1c7259bfa78c55f3e83f4a10afa1333be6",
"tx_id_signature": "b6c7d62f37f72fa4133eb42ad487cca797ca6717fb8aa916c6b66391f7cf847e",
"signature": "HxtINqrryADzs2lnBTr35uLs0HxIZHDHIlEX31If5K6JGlnX0n3EanqyS4x8rVPNF6k10i/v92Cl5yTaKW0ui8Q=",
"aes_password": "GhNr5i8HSaUHRiLcy6FamBo3li0I2lj0",
"aes_iv": "QuN4X1EV4Vd0",
"trade_channel_name": "200_tons_unobtainium_march_2019"
}
}
```
***Explanation of NMEA GPS data:***
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

# 2. Retrieving GPS data from TRADE-Chain
To retrieve GPS data use `post /api/v1/get_data` and pass 5 parameters:

1. `tx_id_enc_data` - the id of the transaction in which the encrypted data and tag were published to the trade channel.
2. `tx_id_signature` - the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the trade channel.
3. `aes_password` - the AES password.
4. `aes_iv` - the Initialization Vector (IV).
5. `trade_channel_name` - the name of the trade channel from which the data is to be retrieved.

Sample input
```
{
  "tx_id_enc_data": "a3187d4f3b54360538036f1a9e8c9e1c7259bfa78c55f3e83f4a10afa1333be6",
  "tx_id_signature": "b6c7d62f37f72fa4133eb42ad487cca797ca6717fb8aa916c6b66391f7cf847e",
  "aes_password": "GhNr5i8HSaUHRiLcy6FamBo3li0I2lj0",
  "aes_iv": "QuN4X1EV4Vd0",
  "trade_channel_name": "200_tons_unobtainium_march_2019"
}
```
***This is what happens:***   
1. The digital signature, hash and the primechain address of the signing entity are retrieved from the trade channel.
2. The encrypted data and tag are retrieved from the trade channel.
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
"response": 
  {
    "data": 
      {
        "NMEA_GPS_DATA": "$GPGGA,181908.00,3404.7041778,N,07044.3966270,W,4,13,1.00,495.144,M,29.200,M,0.10,0000*40",
        "GPS_DATA": "18.5528145,73.7711756",
        "TIMESTAMP": "1547821163"
      },
    "primechain_address": "1VUid7fZaiFnNXddiwfwvk8idyXixkFKRSQvMp",
    "signature_status": true,
    "timestamp": "18/01/2019 02:35:47:00"
  }
}
```
Have a query? Email us on info@primechain.in
