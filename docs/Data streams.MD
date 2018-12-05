# Data streams

MultiChain streams enable a blockchain to be used as a general purpose append-only database, with the blockchain providing timestamping, notarization and immutability. A MultiChain blockchain can contain any number of streams, where the data published in every stream is stored by every node. If a node chooses to subscribe to a stream, it will index that stream’s contents to enable efficient retrieval in various ways.

[1. Create data stream](#1-create-data-stream)   
[2. List data streams](#2-list-data-streams)   
[3. Grant write permission to a stream](#3-grant-write-permission-to-a-stream)   
[4. Subscribe node to a data stream](#4-subscribe-node-to-a-data-stream)   
[5. Unsubscribe node from a data stream](#5-unsubscribe-node-from-a-data-stream)   
[6. Write to a data stream](#6-write-to-a-data-stream)   
[7. List stream items by key](#7-list-stream-items-by-key)   
[8. List stream items by publisher](#8-list-stream-items-by-publisher)   
[9. List keys in a specified stream](#9-list-keys-in-a-specified-stream)   
[10. Retrieve all data from a specified stream](#10-retrieve-all-data-from-a-specified-stream)   

## 1. Create data stream
To create a new stream on the blockchain with the specified name, use `post /api/v1/create_data_stream_from ` with 5 parameters:
```
{
  "from_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "type": "stream",
  "stream_name": "TEST_STREAM_8",
  "details": "This is a test data stream",
  "open":true
}
```
***Note:*** If `open` is set to `true`, write permissions need not be explicitly provided. All addresses can write to the stream. If `open` is set to `false`, write permissions need to be explicitly provided.

The output is the txid of the transaction creating the stream.
```
{
"status": 200,
"transaction_id": "e6c3f05d1f576fb559d04ab60124fdbd04d0b32605fab2534a81a63ebe0962ac"
}
```
***Note:*** 
* The entity creating the stream must have `create` permission.
* Publishers must be explicitly granted per-stream write permissions.

## 2. List data streams
To get information about all the streams created on the blockchain, use `get /api/v1/list_data_streams`. 
```
{
"stream_details": [
  {
"name": "root",
"createtxid": "144db07d12ca680753868c89f058849a5d5ae20c44f4caabe7a90fbd82e1f884",
"streamref": "0-0-0",
"open": false,
"details": {},
"subscribed": true,
"synchronized": true,
"items": 0,
"confirmed": 0,
"keys": 0,
"publishers": 0
},
  {
"name": "OFFER_DETAILS_STREAM",
"createtxid": "a9caefb96930a16b5e2b705914b6a934212d939dfc4ea3d8020d5fff003e3dc2",
"streamref": "3-265-51881",
"open": false,
"details": {
"purpose": "Stores the offer details"
},
"subscribed": true,
"synchronized": true,
"items": 0,
"confirmed": 0,
"keys": 0,
"publishers": 0
},
  {
"name": "BLOB_STREAM",
"createtxid": "e0c78df9ac8ccdd1ebe34a821f7f1a5791bfdeb8badda40eeb2c8e7f597361d9",
"streamref": "3-530-51168",
"open": false,
"details": {
"purpose": "Stores the hex blob of raw exchange"
},
"subscribed": true,
"synchronized": true,
"items": 0,
"confirmed": 0,
"keys": 0,
"publishers": 0
}
],
}
```
## 3. Grant write permission to a stream

To grant an entity write permission to a stream, use `post /api/v1/grant_write_permission_to_stream` and provide 2 parameters - addresss (the blockchain address of the entity) and the stream name. Example:
```
{
  "address": "1BGuzWgkBoyCtk71YyN7BFapY69qhgBL1wmLXk",
  "stream_name": "ASSET_DATA_MASTERLIST"
}
```
```
{
"status": 200,
"transaction_id": "a7671ffc82874c195e070017531b196093d5109d3fda55fd2c0c0acb823d1122"
}
```
The output is the transaction_id of the transaction granting the permission.

## 4. Subscribe node to a data stream
To subscribe a node to a data stream, use `post /api/v1/subscribe` and pass the stream name as a parameter.
```
{
  "stream_name": "TEST_STREAM"
}
```
The response is null
```
{
"status": 200,
"response": null
}
```
## 5. Unsubscribe node from a data stream
To unsubscribe a node from a data stream, use `post /api/v1/unsubscribe` and pass the stream name as a parameter.
```
{
  "stream_name": "TEST_STREAM"
}
```
The response is null
```
{
"status": 200,
"response": null
}
```

## 6. Write to a data stream

To write to a data stream, use `post /api/v1/write_to_stream` and pass these parameters:
```
{
  "from_address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "key": "Invoice no. 443598724",
  "value": 
  	{ 
    	"issue_date": "08-11-2018",
    	"value":"USD 44,500"
  	},
  "stream": "TEST_STREAM"
}
```
```
{
"status": 200,
"response": "c3238398b4633d7a0be543e81b2f57cb1314f178fea2b71ae29d4423866d7fe9"
}
```
## 7. List stream items by key
To list stream items by key, use `post /api/v1/list_stream_items_by_key` and pass 2 parameters - `key` and `stream_name`
```
{
  "key": "Invoice no. 443598724",
  "stream_name": "TEST_STREAM"
}
```
```
{
"status": 200,
"response": 
  [
    {
      "publishers": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
      "key": "Invoice no. 443598724",
      "data": "{"issue_date":"08-11-2018","value":"USD 44,500"}",
      "confirmations": 11,
      "blockhash": "075eaf3b5c8fd1063b18a0c02a6b67b106276aeff82bce22a4a809a199cf466e",
      "blockindex": 1,
      "blocktime": 1543234837,
      "txid": "c3238398b4633d7a0be543e81b2f57cb1314f178fea2b71ae29d4423866d7fe9",
      "vout": 0,
      "valid": true,
      "time": 1543234832,
      "timereceived": 1543234832
    }
  ],
}
```

## 8. List stream items by publisher
To list stream items by publisher, use `post /api/v1/list_stream_items_by_publisher` and pass 2 parameters - `address` and `stream_name`
```
{
  "address": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
  "stream_name": "TEST_STREAM"
}
```
```
{
  "status": 200,
  "response": 
    [
      {
        "publishers": "17kpbJdha6vt8QjZz3nsctSx2qWK38idttfDV9",
        "key": "Invoice no. 443598724",
        "data": "{"issue_date":"08-11-2018","value":"USD 44,500"}",
        "confirmations": 11,
        "blockhash": "075eaf3b5c8fd1063b18a0c02a6b67b106276aeff82bce22a4a809a199cf466e",
        "blockindex": 1,
        "blocktime": 1543234837,
        "txid": "c3238398b4633d7a0be543e81b2f57cb1314f178fea2b71ae29d4423866d7fe9",
        "vout": 0,
        "valid": true,
        "time": 1543234832,
        "timereceived": 1543234832
      }
    ],
}
```
## 9. List keys in a specified stream

To list keys in a specified stream, use `post /api/v1/list_stream_keys` and pass 1 parameter - `stream_name`
```
{
"stream_name": "TEST_STREAM"
}
```
```
{
  "status": 200,
  "response": 
    [
      {
        "key": "Invoice no. 443598724"
      }
    ],
}
```

## 10. Retrieve all data from a specified stream

To obtain all data from a specified stream, use `post /api/v1/list_stream_items` and pass 1 parameter - `stream_name`
```
{
  "stream_name": "RSA_MASTERLIST"
}
```
The output will be something like this:
```
{
"status": 200,
"response": [
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1af89TzR7d7N3pqtKrfzQFxz9MYuNvpt2iFBmj",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAk43Q5FlWcbnsU7Pbbxz1 cGVI3qtjOoRjyESCpKp/TTgiEr/6t8x6voo+WDOiiTTKD/jM/PGJkBh5bYiXwsDH wFqaEFa0wfvYTmGQxSBXwmuh45HdlWinryvXvZHlXnuCxZIPe7meW9FZN08QHRBL SNpMHBsfcVdPymRdfDwOJZb+GQPsO57RlIhJZ7SZ7KBtLaQu4xnrJcskRmj7vG28 zKixZFh5kuR0VJIdxPWwusURQJM6AUNkv9c1oIOPnkzXfOEYGoOqOtRSmXW5ifxy TjNcHyU7y9FABUbt+KPkZm+tngL91a3FQhT/qCgaARljQAiuL0MMNsc/N1wt6C+b XQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 2193,
"blocktime": 1542716811,
"txid": "8f76b080d29270ba34db89381d0594a03ab235e9c80fd3233f66f349f1e62fa4",
"vout": 0,
"valid": true,
"time": 1542716799,
"timereceived": 1542716799
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1C6ecGod2vqP85w8SRW1nquqn8HiynL9jjYzuP",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoolY3G1f8y824OwJgLKV MXOVFRZbHoCYepwsRFF9VQ+tZVEgx1aT9JdjIq2IlixB35NSCiB+0beG4rPu10/X 8800+GRxV5o1NjxGXftNXpHxx9lLdvaj1KSkXs3XCUZ1ibXpx7WULQWzhybbnHUE cizZER3/WGeVeedZTURoYr4ZS+mu4Db7q39AWrtUoCPDKWntByUsoDltExm8voZW x8wAtiNONSyEL7xOZL8lLenP13vOT4xc1WG66nZI6p2W+GtzQxcXMil4/DJ912aC dycmEJWTC1OfR2qrKdMJZ73uRLUw712pDqVCB3IJkZoJAHosyL1bl95cpPUQnJzm wQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1965,
"blocktime": 1542802615,
"txid": "2412d11977dbde02f30c2c38059d769a41c5b9b89f36bd92a53ec2568a89b1d7",
"vout": 0,
"valid": true,
"time": 1542802604,
"timereceived": 1542802604
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1VtTz3kJvcGhnMBefhayNpzkRHqj5oudKUoXeD",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsnNgnGjvlUYD26q0siHp zn6AtdXAw1m/QYm6Novu1UZaycN1sT5DG3A9H4HmStsxbF4mbyrJd+RZaih7C5Xz ASUYm0fphJTUx9KEbXH1zpYWxKhAVWnPOQ1kgQlP8uoAl8zupG9tnRTC5xyor1oc QfOJid2Suo2n6zymZlhyJsjcnVoVrG1TbgnkNCD/krZD/vOuEI3Sa8uHhOfv4YGI yQs/kqXaA4y/cRspx7GWPNt+Db6QHXXvCDnTTL80T4bp3Z7Y9IRn7VatyLXniNDI 1lzv82LXjrRIyAyHV+apbkapwGyH5Ir80rHjGNKigPdEngmWMAIdNJ3LjqyKshQj QQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1888,
"blocktime": 1542884017,
"txid": "33555a6ae4a76f308c896ae1ecb766935b6322ee96a6383ef4eee6d8a230de6b",
"vout": 0,
"valid": true,
"time": 1542884010,
"timereceived": 1542884010
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1bQzYGpdHxLyiKyk2GA1suBjMYsbot9M4NMSmY",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsrhLxeXXdY3CXCaOhCec DtDVByFNOWaFyfDJtDENd6k6FDYVXZlUCag/WtfifNrJpFnubDpfVRPjHGwQ0mOj 3bc2ZaW6APoaGAEl41UphlHFExdC1YKPDfFNIy9nQJHdTT0BWrg4GjsMz6z8Hwlq C/m1pvVje7HLa7pMD7lFjNFJugsvf4eQUwpRK1TlNZGOkZiLisYt5xdJUIl0OWRj hShyjeN0jvHI8CKZkY7VE9Sn/IgjLeeFKsNwAMWBmwgXFUCi0De9NtR91OR2Y8dV VdrYkwAx6KcYh0Fj5HbppSPlYbNLZPh5cEC0+k7zpitA10rHmS3thAZv2/iPxY1v /wIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1877,
"blocktime": 1542885826,
"txid": "7400f45589f2843a9b611e478cf7a7948cf20dba9255c955dbf768ce9159706e",
"vout": 0,
"valid": true,
"time": 1542885819,
"timereceived": 1542885819
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1L2EMSuZ7HYjgZ6WUwDv1XamVZcf52EMeYvxtx",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAi1ge1/CchJXUWahIoGd4 fJEZh2rAAiydcsdRikG18DwTw3N09GDvdtdUn9u7ZDTdyX+oaNEQ2i+VoRuwSnCS w7cwsFpsi9Jj+u4fv8S6cAaSgkUWnFe4RCe4WVd9mfxQf6pn8VF0esimeQ5v6uPe GexQIQPLtfKZFFufVCt74wE/5M2PPTJYhGF8qp/1YOlLKP5HtKGOG61EYh71wpUd I+CEqV8OOEHXs0r4cMv2K/9OkaZDEQx4bm5dZhylP54EEKqywhW6VAOfuBE+16wE 7bPOmhA7MqImq+BLlJzGQVnG4YQmfq/63exFMKef94i6TCt6numpvkpWbkfGYj2b iQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1877,
"blocktime": 1542885826,
"txid": "17a084693a205ef0251af11ab6b348f9f32af93aa75933db40001cec0fac5a6b",
"vout": 0,
"valid": true,
"time": 1542885819,
"timereceived": 1542885819
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1CAWXRnYRuteZ6L2LTEgCBZhUaDCppDG8CmGMJ",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtvDKB5uKvbj3spMlKwst xZWBKExAwm/Ok0wx0+zxCOro0GKbm0o2yybLrtnQjRHjYuxpuc3dqYbM0h3FDUWp ut2PRmAHXM4FHDAeP6Ea1mCDS7YVdRtOz5Y5RTPWM8IxwA1dIqi2T90D3qcLTKiy X/5Ef6Ybd8SekIdgx+w7kxhI5p4ab1DQjB7a3RvLevCJqtUEakDxbb42T5DWtDUK U4A9DvJ4lcXTd78FmEkFUw6z70mvchzHY0iVIzQyVM33cqpv3Oey/DsQCUGp7k6C rsS8v3zyXgs432Ts2P5nR+jHWMJ74jlpqI+cTnd2nH4khgTI74z68KwK5Lg1krFI jQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1866,
"blocktime": 1542885931,
"txid": "fd73c8028fdca76d435c1c058eb4e54f8ee8a1754d61a9e8cad60aa538ea1060",
"vout": 0,
"valid": true,
"time": 1542885918,
"timereceived": 1542885918
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "19P3vv4oTgGV67KGvFLxCS3FEm4vZYfvLW91m2",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoJU2hFqS4BPV8XFm9dzR 0fi1C9RXq9NP9raGZSCTyjByX5E5pI+IL+whQm6aia0RYnrcxcum6C8y0Bri8IGN Q7LE3STZ2xkEh5Pn7HyC5TIZs8H9SEZF5dak+e/f0ok64Ts516e5HS9AodnTAsk/ I1z+NRly6P6cJO6A5/tDcC0XkVyMEvZuLVKgwl1X4xALjCs/6jP+Xw7DkDbwU222 XW7souNqv2C6xmHqJ4Kkoz21iL6M+o9DDYZYOq94l6cNu1lHcNqGfObVxlF+BW+G 9cjHS5kxJYMGrNk5c+fX83MwgYR97p9hWIvUEYXmMp/rdKHTGzsGNG1dCTl3rYTw OwIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1278,
"blocktime": 1543299705,
"txid": "b12cc0d595805f4eac940a361277849da5f5ae875d7b8184c41e1a611080819b",
"vout": 0,
"valid": true,
"time": 1543299705,
"timereceived": 1543299705
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1FzGteA4fdbRgZDqdwRYLwYvZERzWEpj3Nyqi8",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAk4LUQursde9/b4Uz05bB tVZ6ffDkjAfnlviFrsI3uRkPIwmXp3ohSMXzuU+mc4dVSP95J7PfgB1WwEKsuNrv nQ/Bg6r/+JyJL6XfQ35uoJS5UikHw/FHH6IpD+nKcsMYnQxBNZxCGYjjmKN94W0s F6m7T9EQ/yhzIV6aIMhmwGaMPMHQC5vzofyojGr4bc44WEK4IGuaNZGKshAQ7H8r t/J5/AFCpqUSuNv/f910clV+rh6Dc03asges63KrTxA1XVsjNUm6xCM9Wyy4cvyN B9428KZOmtGhpGrz9EGVg/IkJ58eOMQJijwbsefPZNE+D1g3wTlIBWlka32/zal4 OwIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1080,
"blocktime": 1543401517,
"txid": "c723565010470dea5878266b598d7d2858bbc2dab6a6884fa324bde7f6b6f50d",
"vout": 0,
"valid": true,
"time": 1543401503,
"timereceived": 1543401503
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1GJLhBCcZw75VuPQKyVxcizQnEDPPzVw7KUj2R",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAjNiRRPOUqbd5lXDnnyXe 4CrZTek2+nR1ndhEcS+sqKmP5Rgi5NU0hrwmdDOh4vQQ0pi2vhJCKyo8LBvB5yag nRbA4xAe7A8/ywA7KpAax5TWx6bdOS7fNB+zHIh48w/lhljIK7Lr9nCR8iLmk3+i eUb2Y45Icfpofm4ZQH/B3m6fA1t+68UGVbOMVS5/0RiG6WxcdpO3OElpTGMzKuAy RSPtqAwl3xdjXRZtYztkbd/9wL0JVnl+NE4mcLVYOpxT7Kk4Vz/+5gdEhfmJnX1s ibwsMCPrNi77CRJdPNFF4/ORN4EkRJ9gfR3SLNkX0erRfzoYcLRHkMuCooB9wfxP DwIDAQAB -----END PUBLIC KEY-----",
"confirmations": 1069,
"blocktime": 1543401727,
"txid": "ec36555def4d33f81ea1caaaadf0df9640c7fd4e3da05738464ac2ec6920b99f",
"vout": 0,
"valid": true,
"time": 1543401718,
"timereceived": 1543401718
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1P9wEZY7xHAiZNS5JURzhZMk14qHbdTWJpSetr",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA07h08w89WcbtSJMulqO+ PV5l2Du03cPiNnwaJ/IjN56g516FPfFEcDH9buoJDmLdLWhrmRWW1KxUp+uCXRNR sFUDBISixui/RyUPhNzItksfR+Y0JllzZgRdulEwTovOr3XtVzgq5G2Klf+3qsLL 8wPFo7lHaH9sBkbfC0WdxxYu38zpHgVTltZPTyxOcdbP1zuGUE0cFQDnEpbEGlJB IzN27NtL/fL3D6l8pgDNB6qmuGgHdQJ3AayMDTDkueWVGS8bwrEojNFuNVqIGfEe WTallped8lakop/lCcZH5D2w8iMB8BftFT1Ey+PmGwg+iipa1JC6WKWMkTppKxWw NQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 482,
"blocktime": 1543857762,
"txid": "0471f5d72d278805c255b09c0d3b03463ab0dc2ea62db1ff92d00e7defe05088",
"vout": 0,
"valid": true,
"time": 1543857755,
"timereceived": 1543857755
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1B33Km1oRzK3nvyZW7aj1xcxjfZJRkBVFMGmBN",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAnmnr3KKKFDGWY66mtnsl X3U4WYS/S/tyZ85BgGNgFZlIgQV7iL5WQeHDk3BNGaqswKDRsQo4Vi6MnDx70zfs uEmIskPDVOIdFeIs1qMkRRZy8CkNa/rcYhaAIsCeIzs5m5710Zax1XxRNgkcJ9k1 kHFOADTMuYrV8MPUuM54OJ3WH6wjLzuAh58mdUinIruQNfbby9Pj4j/cvNw5KxJG LvGX/cCpf8LSuxFtSavgk/I41j5aW+CsZ8Iz08t7wmiFQmRUdU3B4VCM/gvbw6ZC FD8H3G4A6CHJ97iehDgOup7lao81jzTRUSfwqfQyfCPQe6HBqjP3aR645Z0FLQmT twIDAQAB -----END PUBLIC KEY-----",
"confirmations": 460,
"blocktime": 1543902863,
"txid": "3600f4fecff559b71c64479cc092f946c15ca4aa65dd2ce71fafa66bbae61089",
"vout": 0,
"valid": true,
"time": 1543902855,
"timereceived": 1543902855
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "15bQDZvAshoqkX2adqLAfWUttnFhXP3EsC92Jo",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAo8tGo5+i679dN9vlp86y oGSGqJnHtM4PdN/XQKklIsKCYWhFdRaaOq5hsfUOIwEhBCX7/eacsFZTYN8XZSsH yNJxyjf0iZnT2EjyNlf1nkJ8YrhTuXKNeCJnDS5aKvc+2l1uLp+xs8cvEvbX04fv +5y3tya1mRcxeEleWvXFzzGSFqQt4+egQOY+x5LghunbKs9E8iEWDYBE9DocINMk jcqaJgtaGlusxH3e01wGBdZW+lm6GZ7EuXsGPLLob5qNOE3HVWy/cTW/k4vSgqvu 7UIgrZ5idX+V2I3rBQYc168PM3MPfO9V1XcrzBgAFsXBPd25pCSo9LO7kuVEswBr IwIDAQAB -----END PUBLIC KEY-----",
"confirmations": 119,
"blocktime": 1543990954,
"txid": "d872cb67771ead926871a79ae8b2d6d65d9238fe00ddd39278d7a107638c44bc",
"vout": 0,
"valid": true,
"time": 1543990940,
"timereceived": 1543990940
},
  {
"publishers": "1aT3P8hqCK21x3EKyFKLzqLYdAnAqBALx3Gri3",
"key": "1LRXkkzPrXX7jiMr6WZsDjrcQ2mFLBxbS8KVcN",
"data": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAgrDF+Ii7qmtcq0D6X89q qmQFaOLexs78kgXCLTXYQn4lPipKkRYu77ZBvEReQ/dnGuQpknS/wAM5WBTySXcb qGe5Y4vAvL/n3Ei1xPvUm63JhgW750h1AaIrn69id7ECi3WcQcazzeFFh4yV/9fq oWBFoHg6iqLD9roImzT508iw/AqVgEHAtVzX7/w/BJD22q0GQ/dLgFJh0058dKCm GcOx0ZgVQvH9xruh8OGGBvK2GAb9qinp8ItzBV2qxCjkplDMwJ7jTQrxlFSeobzx esPC3rmSykEdv9Z7MIwBeMOT7BkzQTL5otTwfDJh73oJc3hscl02Uv4mAn/NSoOz HQIDAQAB -----END PUBLIC KEY-----",
"confirmations": 119,
"blocktime": 1543990954,
"txid": "c35ef79d84c2c246ad16bc6e0aeda602a5633bde608a96091d8397312e4f5b33",
"vout": 0,
"valid": true,
"time": 1543990940,
"timereceived": 1543990940
}
],
}
```
