# Data storage

MultiChain streams enable a blockchain to be used as a general purpose append-only database, with the blockchain providing timestamping, notarization and immutability. A MultiChain blockchain can contain any number of streams, where the data published in every stream is stored by every node. If a node chooses to subscribe to a stream, it will index that stream’s contents to enable efficient retrieval in various ways.

[1. Create data stream](#1-create-data-stream)

[2. List data streams](#2-list-data-streams)

[3. Grant write permission to a stream](#3-grant-write-permission-to-a-stream)

[4. Subscribe node to a data stream](#4-subscribe-node-to-a-data-stream)

[5. Unsubscribe node from a data stream](#5-unsubscribe-node-from-a-data-stream)


## 1. Create data stream
To create a new stream on the blockchain with the specified name, use `post /api/v1/create_data_stream_from `
```
{
  "from_address": "1AguXpqkeH2aZDpU5NaJ2xgp5ZoxiGgCi99c3E",
  "type": "stream",
  "stream_name": "TEST_STREAM",
  "details": "This is a test data stream" 
}
```
![Create data stream](http://www.primechaintech.com/img/api_documentation/create_data_stream_from.png)

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
![List data streams](http://www.primechaintech.com/img/api_documentation/list_data_streams.png)
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
  "address": "1FG92XaytZPWspbkVpVicJpQzeFPA78VbUkii3",
  "stream_name": "OFFER_DETAILS_STREAM"
}
```
![Grant write permission to a stream](http://www.primechaintech.com/img/api_documentation/grant.png)
```
{
"status": 200,
"transaction_id": "aaaa"
}
```
The output is the transaction_id of the transaction granting the permission.

## 4. Subscribe node to a data stream
To subscribe a node to a data stream, use `subscribe` and pass the stream name as a parameter.
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
To unsubscribe a node from a data stream, use `unsubscribe` and pass the stream name as a parameter.
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

