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

## 1. Create data stream
To create a new stream on the blockchain with the specified name, use `post /api/v1/create_data_stream_from `
```
{
  "from_address": "15AnXVteaDaTb1wBstqxaXN2ixCEereugw7acE",
  "type": "stream",
  "stream_name": "TEST_STREAM",
  "details": "This is a test data stream" 
}
```
The output is the txid of the transaction creating the stream.
```
{
"status": 200,
"transaction_id": "ddc2fc8d7ad149e0e51a5fc4765b1917a38cbddc0fe7f77a7081cfcf5486a851"
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
  "address": "15GRafetDoXFgMXRHPfPYQRG3b4vLrpeDBCZS9",
  "stream_name": "OFFER_DETAILS_STREAM"
}
```
![Grant write permission to a stream](http://www.primechaintech.com/img/api_documentation/grant_write_permission_to_stream.png)
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
![Subscribe node to a data stream](http://www.primechaintech.com/img/api_documentation/subscribe.png)
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
![Unsubscribes node from a data stream](http://www.primechaintech.com/img/api_documentation/unsubscribe.png)
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
  "from_address": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
  "key": "Invoice no. 443598724",
  "value": 
  	{ 
    	"issue_date": "08-08-2018",
    	"value":"USD 44,500"
  	},
  "stream": "OFFER_DETAILS_STREAM"
}
```
![Write to a data stream](http://www.primechaintech.com/img/api_documentation/write_to_stream.png)
```
{
"status": 200,
"response": "50da4136ebf0fc608739ad97da8b57a2aad65a44d8a9b08cf42f26d2a55793d1"
}
```
## 7. List stream items by key
To list stream items by key, use `post /api/v1/list_stream_items_by_key` and pass 2 parameters - `key` and `stream_name`
```
{
"key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"stream_name": "OFFER_DETAILS_STREAM"
}
```
![List stream items by key](http://www.primechaintech.com/img/api_documentation/list_stream_items_by_key.png)
```
{
"status": 200,
"response": [
  {
"publishers": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"data": "{"key1":"Hello","key2":"world","key3":"chai pilo"}",
"confirmations": 48,
"blockhash": "00b419fa10d1b4c7e9c0d35573fe99e12cec16cb954545754120462f1fcc3d97",
"blockindex": 1,
"blocktime": 1535010800,
"txid": "579cbc75dad47d5e6c29b14bec65d2b5ebd5e703f4338a60b1f8614250772217",
"vout": 0,
"valid": true,
"time": 1535010791,
"timereceived": 1535010791
},
  {
"publishers": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"data": "{"key1":"Hello","key2":"world"}",
"confirmations": 48,
"blockhash": "00b419fa10d1b4c7e9c0d35573fe99e12cec16cb954545754120462f1fcc3d97",
"blockindex": 1,
"blocktime": 1535010800,
"txid": "579cbc75dad47d5e6c29b14bec65d2b5ebd5e703f4338a60b1f8614250772217",
"vout": 0,
"valid": true,
"time": 1535010791,
"timereceived": 1535010791
},
  {
"publishers": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"data": "{"hello":"world","check_stream_data":"hex-blob"}",
"confirmations": 48,
"blockhash": "00b419fa10d1b4c7e9c0d35573fe99e12cec16cb954545754120462f1fcc3d97",
"blockindex": 1,
"blocktime": 1535010800,
"txid": "579cbc75dad47d5e6c29b14bec65d2b5ebd5e703f4338a60b1f8614250772217",
"vout": 0,
"valid": true,
"time": 1535010791,
"timereceived": 1535010791
},
  {
"publishers": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"data": "{"hello":"world","check_stream_data":"hex-blob"}",
"confirmations": 48,
"blockhash": "00b419fa10d1b4c7e9c0d35573fe99e12cec16cb954545754120462f1fcc3d97",
"blockindex": 1,
"blocktime": 1535010800,
"txid": "579cbc75dad47d5e6c29b14bec65d2b5ebd5e703f4338a60b1f8614250772217",
"vout": 0,
"valid": true,
"time": 1535010791,
"timereceived": 1535010791
}
],
}
```

## 8. List stream items by publisher
To list stream items by publisher, use `post /api/v1/list_stream_items_by_publisher` and pass 2 parameters - `address` and `stream_name`
```
{
"address": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
"stream_name": "OFFER_DETAILS_STREAM"
}
```
![List stream items by publisher](http://www.primechaintech.com/img/api_documentation/list_stream_items_by_publisher.png)
```
{
  "status": 200,
  "response": 
  [
    {
      "publishers": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
      "key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a",
      "data": 
        "{
            "issue_date":"08-08-2018",
            "value":"USD 44,500"
         }",
      "confirmations": 48,
      "blocktime": 1535010800,
      "txid": "579cbc75dad47d5e6c29b14bec65d2b5ebd5e703f4338a60b1f8614250772217"
    }
  ],
}
```
## 9. List keys in a specified stream

To list keys in a specified stream, use `post /api/v1/list_stream_keys` and pass 1 parameter - `stream_name`
```
{
"stream_name": "OFFER_DETAILS_STREAM"
}
```
![List keys in a specified stream](http://www.primechaintech.com/img/api_documentation/list_stream_keys.png)

```
{
"status": 200,
"response": [
  {
"key": "1KZhwaRzvAo2Q3F3H117XCos7319nrs5JMbM9a"
},
  {
"key": "Invoice no. 443598724"
}
],
}
```
