# Blockchain administration

Blockchain parameters(Blockchain parameters)

[Blockchain parameters](#Blockchain-parameters)
[Runtime parameters](#Runtime-parameters)


## 1. Blockchain parameters

Use `get /api/v1/blockchain_params` to view the blockchain parameters:

```
{
"blockchain_params": 
  {
  "chain-protocol": "multichain",
  "chain-description": "MultiChain primechain-api",
  "root-stream-name": "root",
  "root-stream-open": false,
  "chain-is-testnet": false,
  "target-block-time": 15,
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
  "mining-requires-peers": true,
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
  "skip-pow-check": false,
  "pow-minimum-bits": 8,
  "target-adjust-freq": -1,
  "allow-min-difficulty-blocks": false,
  "only-accept-std-txs": true,
  "max-std-tx-size": 100000000,
  "max-std-op-returns-count": 1024,
  "max-std-op-return-size": 67108864,
  "max-std-op-drops-count": 100,
  "max-std-element-size": 32768,
  "chain-name": "primechain-api",
  "protocol-version": 10010,
  "network-message-start": "ffe9d7f8",
  "address-pubkeyhash-version": "00f4614c",
  "address-scripthash-version": "052fa093",
  "private-key-version": "80b27b1b",
  "address-checksum-value": "5b67e62a",
  "genesis-pubkey": "0266f1068c2cd4681af9c60ca502d9cbea34bcc33a697cbe443df63d79214a011d",
  "genesis-version": 1,
  "genesis-timestamp": 1534147023,
  "genesis-nbits": 536936447,
  "genesis-nonce": 124,
  "genesis-pubkey-hash": "5634ca7dda9a13802c5bfc2231954dfa9cc0ea48",
  "genesis-hash": "002d48159826212d459db0f96a165dbd3d61b941a4015f5cbdef87c9c6402e19",
  "chain-params-hash": "f72fef0aedf346e7f01033a1580247660c75a9af9aae3b50d66f663089d15592"
  }
}
```

## 2. Runtime parameters
To get a selection of this node's runtime parameters (these are set when the node starts up), use `get /api/v1/runtime_params`

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
