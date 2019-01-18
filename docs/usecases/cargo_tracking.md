# Cargo tracking

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

TRADE-Chain enables real-time tracking of cargo.

![Cargo tracking](http://www.primechaintech.com/img/api_documentation/cargo.jpg)

***Table of contents***   
[1. Publishing NMEA format GPS data](#1-publishing-nmea-format-gps-data)   


1. Publishing NMEA format GPS data

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
Sample output
```
{
"status": 200,
"response": {
"tx_id_enc_data": "3491c0a9678686ad8940d1451f2f05176dbae88db311df410aacbee3f913a06e",
"tx_id_signature": "280b55b43301a0ff036d901ccaab43c3ba9c74d8c5690a9ad2ec30c913607dfc",
"signature": "IAUFcrLOfZ3n/XNSolqlvrVii2Gt6VOahyvRv9clf/F/RMT9qTOZ26Dg+i6MtZcnsOUSpoG6Y5qmUcMRR7iuSKU=",
"aes_password": "3BY6mYQC6mza8rbNL4BnjiM36ItafymK",
"aes_iv": "K47jajud824W",
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

