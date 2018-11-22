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
  "blockchain_params": 
  {
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
    "network-message-start": "f2c2dde5",
    "address-pubkeyhash-version": "00e56c20",
    "address-scripthash-version": "056f212c",
    "private-key-version": "80736e72",
    "address-checksum-value": "042695a6",
    "genesis-pubkey": "0203f2047224b87a0e8fffa61a4741d13cb215e1735b16570eacb2c3729aa129aa",
    "genesis-version": 1,
    "genesis-timestamp": 1542714998,
    "genesis-nbits": 537919487,
    "genesis-nonce": 11,
    "genesis-pubkey-hash": "f77c8e6f155b95a2a4aed30c99bca230871d9971",
    "genesis-hash": "00aec9c0e03aed13dc678e9306bd78f71536b240725ce6ffaf8abc0fc64e5651",
    "chain-params-hash": "487a00663455e9bf54e7e2ecdefd9e7ed8e2d0b5f781e72807d987e3970a2db0"
  }
}
```

## 2. Runtime parameters
To get a selection of this node's runtime parameters (these are set when the node starts up), use `get /api/v1/runtime_params`

![Runtime parameters](http://www.primechaintech.com/img/api_documentation/runtime_params.png)

```
{
"runtime_params": 
  {
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
  "handshakelocal": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
  "bantx": "",
  "lockblock": "",
  "hideknownopdrops": false,
  "maxshowndata": 16384,
  "miningrequirespeers": true,
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

![Blockchain information](http://www.primechaintech.com/img/api_documentation/blockchain_info.png)

```
{
"blockchain_params": 
  [
    {
      "version": "1.0.6",
      "nodeversion": 10006901,
      "protocolversion": 10010,
      "chainname": "primechain-api",
      "description": "MultiChain primechain-api",
      "protocol": "multichain",
      "port": 61172,
      "setupblocks": 60,
      "nodeaddress": "primechain-api@10.1.3.5:61172",
      "burnaddress": "1XXXXXXXa5XXXXXXidXXXXXXPuXXXXXXRMNLPi",
      "incomingpaused": false,
      "miningpaused": false,
      "walletversion": 60000,
      "balance": 0,
      "walletdbversion": 2,
      "reindex": false,
      "blocks": 59,
      "timeoffset": 0,
      "connections": 0,
      "proxy": "",
      "difficulty": 6e-8,
      "testnet": false,
      "keypoololdest": 1534763559,
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
      "blocks_": 59,
      "headers": 59,
      "bestblockhash": "00385c95a6be9b0bcade6404c608583e89100716485ffcf015dd3e10883ad525",
      "difficulty_": 6e-8,
      "verificationprogress": 1,
      "chainwork": "0000000000000000000000000000000000000000000000000000000000003c00",
      "chainrewards": 0
    }
  ],
}
```
***Notes:***
1. The `bestblockhash` of the most recent block on the active chain can be compared across nodes to check if they are perfectly synchronized.
2. The `burnaddress` is an address with no known private key. Assets can be sent to the `burnaddress` to make them provably unspendable. 
3. The `nodeaddress` can be passed to other nodes for connecting. 
4. The `setupblocks` field gives the length in blocks of the setup phase in which some consensus constraints are not applied.

## 4. Memory pool information
The memory pool contains transactions that the node has seen and validated, but which have not yet been confirmed on the active chain. To get information about the memory pool, use `get /api/v1/mempool_info`

![Memory pool information](http://www.primechaintech.com/img/api_documentation/mempool_info.png)

```
{
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

![Memory pool information](http://www.primechaintech.com/img/api_documentation/raw_mempool.png)

## 6. List blocks
Use `get /api/v1/list_blocks` for information about the blocks specified, on the active chain only.

***List blocks 10-12***

![List blocks 10 to 12](http://www.primechaintech.com/img/api_documentation/list_blocks.jpg)
```
{
"list_blocks": [
  {
"hash": "004968b902a48bea35aa9eaf805538b4dfc87a459d565c98d7073d2d46e0900e",
"miner": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
"confirmations": 50,
"height": 10,
"time": 1534147156,
"txcount": 1
},
  {
"hash": "007114db4305134280f3d258cb26e3a3e3fac3a7569845f60cc559586a58e480",
"miner": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
"confirmations": 49,
"height": 11,
"time": 1534147173,
"txcount": 1
},
  {
"hash": "007b00e2f671cdc5efbe66d19a1c63aba98ae79d9e46b97dee2fb520d2679d68",
"miner": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
"confirmations": 48,
"height": 12,
"time": 1534147185,
"txcount": 1
}
],
}
```

***List blocks 8, 14 and 23***

![List blocks 8, 14 and 23](http://www.primechaintech.com/img/api_documentation/list_blocks2.png)
```
{
"list_blocks": [
  {
"hash": "007cbc3d66d76ebd2e6510cc7bbb59dad1d9e78300d678089cc6645f8c65a17a",
"miner": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
"confirmations": 52,
"height": 8,
"time": 1534147125,
"txcount": 1
},
  {
"hash": "00291965ee0587f5d732810bba18b2384c15140d3f52e293b881557f171b2e2d",
"miner": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
"confirmations": 46,
"height": 14,
"time": 1534147213,
"txcount": 1
},
  {
"hash": "0052fa2f3c3b6b97fda9d6685f771142afbccefde10c532e8e838ca2ad7065f1",
"miner": "1Cema16ostGkWi1xkBq9HUQ8deDKV53ZxHjAu1",
"confirmations": 37,
"height": 23,
"time": 1534147339,
"txcount": 1
}
],
}
```
***Note:***
The blocks parameter can contain a comma-delimited list or array of block heights, hashes, height ranges (e.g. 100-200) or -n for the most recent n blocks. Alternatively, pass an object {"starttime":...,"endtime":...} for blocks whose timestamps are in the given range.

## 7. Peer info
Use `get /api/v1/peer_info` for information about the other nodes to which this node is connected.
```
```
***Note:*** 
This includes handshake and handshakelocal fields showing the remote and local address used during the handshaking for that connection.
