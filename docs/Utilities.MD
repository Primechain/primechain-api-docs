# Utilities

[1. Upgrading Primechain-API](#1-upgrading-primechain-api)   
[2. Create passwords](#2-create-passwords)   
[3. Create UUID](#3-create-uuid)   

## 1. Upgrading Primechain-API
Login to the server and execute the following commands:
```
sudo su apiuser
cd ~/primechain-api && pm2 stop 0 && git pull && pm2 start 0
```


## 2. Create passwords
To get a list of random passwords, use `get /api/v1/get_password`
```
{
"simple_8_character": "dATpflEQ",
"complex_8_character": "$H28p0g0",
"simple_20_character": "7hRKKeg3R7BNnSlcMgFY",
"complex_20_character": "ai&iTmQg8zsTRk&hQ5Li",
"simple_32_character": "VnqhijGRyswF8zgjvSsyvI5F7duSON28",
"complex_32_character": "kfcZU8G1RJvmcB-xuElCIuGoShm2YcoT",
"simple_40_character": "Dk3oo2rA1o8dqBaFXkZ2IEykDepD0VvdMIGOS5vo",
"complex_40_character": "0Q%$zj&B-bXZW3V2tn!GWhvGiEjf&q8p-SP^reur"
}
```
## 3. Create UUID
To get a universally unique identifier (UUID), use `get /api/v1/uuid`
```
{
"uuid": "aa5fcef5-ffc7-45c9-85a2-357f0d0057fc"
}
```
