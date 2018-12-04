# Blockchain administration

1. [Blockchain parameters](#1-blockchain-parameters)
2. [Runtime parameters](#2-runtime-parameters)
3. [Blockchain information](#3-blockchain-information)
4. [Memory pool information](#4-memory-pool-information)
5. [Raw memory pool](#5-raw-memory-pool)
6. [List blocks](#6-list-blocks)
7. [Peer info](#7-peer-info)


## 1. Blockchain parameters
Use `get /api/v1/blockchain_params` to view the blockchain parameters:

```
{
"status": 200,
"blockchain_params": {
"chain-protocol": "multichain",
"chain-description": "MultiChain primechain-api",
"root-stream-name": "root",
"root-stream-open": false,
"chain-is-testnet": false,
"target-block-time": 10,
"maximum-block-size": 1000000000,
"default-network-port": 61172,
"default-rpc-port": 15590,
"anyone-can-connect": false,
"anyone-can-send": false,
"anyone-can-receive": false,
"anyone-can-receive-empty": true,
"anyone-can-create": false,
"anyone-can-issue": false,
"anyone-can-mine": false,
"anyone-can-activate": false,
"anyone-can-admin": false,
"support-miner-precheck": true,
"allow-arbitrary-outputs": false,
"allow-p2sh-outputs": true,
"allow-multisig-outputs": true,
"setup-first-blocks": 60,
"mining-diversity": 0.3,
"admin-consensus-upgrade": 0.5,
"admin-consensus-admin": 0.5,
"admin-consensus-activate": 0.5,
"admin-consensus-mine": 0.5,
"admin-consensus-create": 0,
"admin-consensus-issue": 0,
"lock-admin-mine-rounds": 10,
"mining-requires-peers": false,
"mine-empty-rounds": 10,
"mining-turnover": 0.5,
"first-block-reward": -1,
"initial-block-reward": 0,
"reward-halving-interval": 52560000,
"reward-spendable-delay": 1,
"minimum-per-output": 0,
"maximum-per-output": 100000000000000,
"minimum-relay-fee": 0,
"native-currency-multiple": 100000000,
"skip-pow-check": true,
"pow-minimum-bits": 4,
"target-adjust-freq": -1,
"allow-min-difficulty-blocks": false,
"only-accept-std-txs": true,
"max-std-tx-size": 100000000,
"max-std-op-returns-count": 1024,
"max-std-op-return-size": 67108864,
"max-std-op-drops-count": 100,
"max-std-element-size": 32768,
"chain-name": "primechain-api",
"protocol-version": 10011,
"network-message-start": "f2e1ccf2",
"address-pubkeyhash-version": "00c4bbce",
"address-scripthash-version": "05f724b2",
"private-key-version": "80e9f374",
"address-checksum-value": "97582e9c",
"genesis-pubkey": "03bb8ca6bc395d6638ab1bc9a7e8a34ef10b894663bef065ee0d5966c43f8adabc",
"genesis-version": 1,
"genesis-timestamp": 1543911518,
"genesis-nbits": 537919487,
"genesis-nonce": 3,
"genesis-pubkey-hash": "b180acd07afad0857f3993da10cfd7342e20208a",
"genesis-hash": "0a5648249009b26040a0305af1d7cdd463311a12d95db0264ecbb6beef4f8941",
"chain-params-hash": "ee65fb033910ff0703e02a3bfd5ccb5b89cd111c59e8582f80a4616b5b2d16fb"
}
}
```

## 2. Runtime parameters
To get a selection of this node's runtime parameters (these are set when the node starts up), use `get /api/v1/runtime_params`

```
{
"status": 200,
"runtime_params": {
"port": 61172,
"reindex": false,
"rescan": false,
"txindex": true,
"autocombineminconf": 1,
"autocombinemininputs": 50,
"autocombinemaxinputs": 100,
"autocombinedelay": 1,
"autocombinesuspend": 15,
"autosubscribe": "",
"handshakelocal": "1Qr572HfZyxmburpA6fQY4Nu2k7uWVR5dwwBoe",
"bantx": "",
"lockblock": "",
"hideknownopdrops": false,
"maxshowndata": 16384,
"miningrequirespeers": false,
"mineemptyrounds": 10,
"miningturnover": 0.5,
"lockadminminerounds": 10,
"gen": true,
"genproclimit": 1
}
}
```

## 3. Blockchain information

Use `get /api/v1/blockchain_info` to get general information about this node and blockchain. 

```
{
"status": 200,
"blockchain_info": {
"version": "1.0.6",
"nodeversion": 10006901,
"protocolversion": 10011,
"chainname": "primechain-api",
"description": "MultiChain primechain-api",
"protocol": "multichain",
"port": 61172,
"setupblocks": 60,
"nodeaddress": "primechain-api@169.63.131.118:61172",
"burnaddress": "1XXXXXXXM4XXXXXXiqXXXXXXdyXXXXXXc7qCdr",
"incomingpaused": false,
"miningpaused": false,
"walletversion": 60000,
"balance": 0,
"walletdbversion": 2,
"reindex": false,
"blocks": 81,
"timeoffset": 0,
"connections": 3,
"proxy": "",
"difficulty": 0,
"testnet": false,
"keypoololdest": 1543915768,
"keypoolsize": 2,
"paytxfee": 0,
"relayfee": 0,
"errors": "",
"chain": "main",
"chain_name": "primechain-api",
"description_": "MultiChain primechain-api",
"protocol_": "multichain",
"setup_blocks": 60,
"re_index": false,
"blocks_": 81,
"headers": 81,
"bestblockhash": "0166ed431644e7a6f768ac2ad5b3904e13a158be729cd5873854fffb01821007",
"difficulty_": 0,
"verificationprogress": 1,
"chainwork": "0000000000000000000000000000000000000000000000000000000000000520",
"chainrewards": 0
}
}
```
***Notes:***
1. The `bestblockhash` of the most recent block on the active chain can be compared across nodes to check if they are perfectly synchronized.
2. The `burnaddress` is an address with no known private key. Assets can be sent to the `burnaddress` to make them provably unspendable. 
3. The `nodeaddress` can be passed to other nodes for connecting. 
4. The `setupblocks` field gives the length in blocks of the setup phase in which some consensus constraints are not applied.

## 4. Memory pool information
The memory pool contains transactions that the node has seen and validated, but which have not yet been confirmed on the active chain. To get information about the memory pool, use `get /api/v1/mempool_info`

```
{
  "status": 200,
  "mempool_info": 
    {
      "size": 0,
      "bytes": 0
    }
}
```
***Note:***
If the memory pool is growing continuously, this suggests that transactions are being generated faster than the network is able to process them.

## 5. Raw memory pool
For a list of transaction IDs which are in the node's memory pool, use `get /api/v1/raw_mempool`

```
{
  "status": 200,
  "raw_mempool": [],
}
```

## 6. List blocks
Use `post /api/v1/list_blocks` for information about the blocks specified, on the active chain only.

***List blocks 10 to 12***

Pass this as a parameter:
```
{
  "block_number":"10-12"
}
```
The output will be something like this:
```
{
"status": 200,
"list_blocks": [
  {
"hash": "068c42ca81014ecddb9dedbd00e9256f823babd539aef30e580229dee79c1821",
"miner": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"confirmations": 72,
"height": 10,
"time": 1543911612,
"txcount": 1
},
  {
"hash": "040d8d8b1913fb25fef5f995054ada332db4d7c32e322e5344fe53264caf124d",
"miner": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"confirmations": 71,
"height": 11,
"time": 1543911621,
"txcount": 1
},
  {
"hash": "0f07a552f2801a198cd5d3f2c2e989379bb60427d3ad4bc4fc22c0060014dc79",
"miner": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"confirmations": 70,
"height": 12,
"time": 1543911637,
"txcount": 1
}
],
}

```

***List blocks 8, 14 and 23***

Pass this as a parameter:
```
{
  "block_number":"8,14,23"
}
```
The output will be something like this:
```
{
"status": 200,
"list_blocks": [
  {
"hash": "0ff1c0dd9ae284766e1150d1eee8b4dc34bae6e75935849f4b41e0e720337270",
"miner": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"confirmations": 74,
"height": 8,
"time": 1543911597,
"txcount": 1
},
  {
"hash": "08294da3838341b76bc8003dd891f4156b08748a20c45517960d229eac10e525",
"miner": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"confirmations": 68,
"height": 14,
"time": 1543911653,
"txcount": 1
},
  {
"hash": "09e6467214f9bd1e0696a9e146cdb635a898c6f325d1af0eba7dd00fc12f6ee0",
"miner": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"confirmations": 59,
"height": 23,
"time": 1543911745,
"txcount": 1
}
],
}
```
***Note:***
The blocks parameter can contain a comma-delimited list or array of block heights, hashes, height ranges (e.g. 100-200) or -n for the most recent n blocks. Alternatively, pass an object {"starttime":...,"endtime":...} for blocks whose timestamps are in the given range.

## 7. Peer info
Use `get /api/v1/peer_info` for information about the other nodes to which this node is connected. The output will be something like this:

```
{
"status": 200,
"peer_info": [
  {
"id": 5,
"addr": "169.63.131.125:61172",
"addrlocal": "169.63.131.118:43376",
"services": "0000000000000001",
"lastsend": 1543919288,
"lastrecv": 1543919288,
"bytessent": 24378,
"bytesrecv": 22834,
"conntime": 1543915962,
"pingtime": 0.06828,
"version": 70002,
"subver": "/MultiChain:0.1.0.11/",
"handshakelocal": "1Qr572HfZyxmburpA6fQY4Nu2k7uWVR5dwwBoe",
"handshake": "1aMiTQjLXABeoKtVgBcr5zzVXtT1eRvRTfY3RJ",
"inbound": false,
"startingheight": 81,
"banscore": 0,
"synced_headers": 81,
"synced_blocks": 81,
"inflight": [],
"whitelisted": false
},
  {
"id": 6,
"addr": "10.188.200.228:61172",
"addrlocal": "10.188.200.225:59178",
"services": "0000000000000001",
"lastsend": 1543919289,
"lastrecv": 1543919289,
"bytessent": 22920,
"bytesrecv": 22895,
"conntime": 1543915963,
"pingtime": 0.067716,
"version": 70002,
"subver": "/MultiChain:0.1.0.11/",
"handshakelocal": "1Qr572HfZyxmburpA6fQY4Nu2k7uWVR5dwwBoe",
"handshake": "1aMiTQjLXABeoKtVgBcr5zzVXtT1eRvRTfY3RJ",
"inbound": false,
"startingheight": 81,
"banscore": 0,
"synced_headers": 81,
"synced_blocks": 81,
"inflight": [],
"whitelisted": false
},
  {
"id": 7,
"addr": "52.172.139.41:61172",
"addrlocal": "169.63.131.118:57018",
"services": "0000000000000001",
"lastsend": 1543919290,
"lastrecv": 1543919291,
"bytessent": 22804,
"bytesrecv": 22926,
"conntime": 1543915964,
"pingtime": 0.261546,
"version": 70002,
"subver": "/MultiChain:0.1.0.11/",
"handshakelocal": "1Qr572HfZyxmburpA6fQY4Nu2k7uWVR5dwwBoe",
"handshake": "1QzSTNf9pCBCPGxSFHYWEzdkCWiKeThgv4Hkmt",
"inbound": false,
"startingheight": 81,
"banscore": 0,
"synced_headers": 81,
"synced_blocks": 81,
"inflight": [],
"whitelisted": false
}
],
}
```

***Note:*** 
This includes handshake and handshakelocal fields showing the remote and local address used during the handshaking for that connection.
