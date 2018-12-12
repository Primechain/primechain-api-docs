# Blockchain based authentication

Primechain-API combines the power of blockchain technology with public key cryptography to enable:
1. Secure authentication and identification of smart-phones and other devices
2. Securing & encrypting online communications
3. Password-less login systems
4. Preventing fake emails & phishing
5. Authenticating DNS records & preventing spoofing attacks
7. Electronic signatures

Blockchain based authentication has some special features:
1. Signing and decryption keys stay on the device.
2. Verification and encryption keys are stored on the blockchain.
3. Protects against critical cyber attacks such as phishing, man-in-the-middle, replay attacks.


## [1. Onboarding a user](#1-onboarding-a-user)   
[1.1 User has multiple devices](#11-user-has-multiple-devices)   
[1.2 Multiple users share the same device](#12-multiple-users-share-the-same-device)   

## [2. Authentication](#2-authentication)   
[Optional - Use of symmetric encryption](#optional---use-of-symmetric-encryption)   
[Step 1 - Retrieving the RSA public key of the verifier](#step-1---retrieving-the-rsa-public-key-of-the-verifier)   
[Step 2 - Encrypting the blockchain address of the requester](#step-2---encrypting-the-blockchain-address-of-the-requester)   
[Step 3 - Sending the encrypted blockchain address to the verifier](#step-3---sending-the-encrypted-blockchain-address-to-the-verifier)   
[Step 4 - Decrypting the encrypted blockchain address](#step-4---decrypting-the-encrypted-blockchain-address)   
[Step 5 - Retrieving the RSA public key of the requester](#step-5---retrieving-the-rsa-public-key-of-the-requester)   
[Step 6 - Generating a random string and timestamp and hash](#step-6---generating-a-random-string-and-timestamp-and-hash)   
[Step 7 - Sending the hash to the requester](#step-7---sending-the-hash-to-the-requester)   
[Step 8 - Decryption of the hash](#step-8---decryption-of-the-hash)    
[Step 9 - Signing of the hash by the requester](#step-9---signing-of-the-hash-by-the-requester)   
[Step 10 - Creating the encrypted envelope](#step-10---creating-the-encrypted-envelope)   
[Step 11 - Sending the encrypted envelope to the verifier](#step-11---sending-the-encrypted-envelope-to-the-verifier)   
[Step 12 - Decrypting of the encrypted envelope by the verifier](#step-12---decrypting-of-the-encrypted-envelope-by-the-verifier)   
[Step 13 - Verification of the digital signature](#step-13---verification-of-the-digital-signature)   

# 1. Onboarding a user
A user can be an individual, a company, a device etc and can be on-boarded using `post /api/v1/onboard_user` and passing the following parameters:
1. The user identifier e.g. name, account number, IMEI number, IP address, serial number, CIN etc.
2. The user description 
```
{
  "user_identifier": "23792387",
  "user_description": "Samairah Nagpal's Noodle Bank app on her iPad"
}
```
The output is:   
1. the new user's primechain address    
2. the new user's primechain private key    
3. the new user's primechain public key   
4. the relevant transaction id   
5. the new user's RSA public key   
6. the new user's RSA private key   

```
{
"status": 200,
"response": {
"primechain_address": "16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA",
"primechain_private_key": "VECSuwoYmF8LHpBy67eV6NbHqBYBuG74dEaE7435xUcS9FGQ48WdXfjc",
"primechain_public_key": "021c2d2e89d68a7cd4505f2464c26d2ace9ced3433f57ac619a9c52fc907042309",
"tx_id": "ef3f1cde044f0a16382230d4e700143da3ef5138a2bfb60791c05461a0ff1de2",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiB49uOAIfw2nGsueboVL +CWPYqiYS/+pYrUjoCe3owwn395o68IPmYDm2NCYk17Dwx2bDW5/B4OFgznw+eSe Hg1K2RrCQbwArKssjez04VtVBODowv/h8usq6R/g1zsA/YtZTLHMR0tdr9Ton0Op GBbc/qsgAo76OJvGcy7dwCXcbzVkscjURiVQ8Grn+yvpS5DQW0fsklUoX6UO8esT lF1u+TFDaizMu5i1bl/CibiRzc5iT/E907ynBc2PZApcices8Eera8Ye8kGG2cz5 LIuf49OfTlq5zRQQLzrHSF5Tg4cVmxOH4XU3sbfPNxnvTVCBONq59LYvGsNBXuDH hQIDAQAB -----END PUBLIC KEY-----",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCIHj244Ah/Daca y55uhUv4JY9iqJhL/6litSOgJ7ejDCff3mjrwg+ZgObY0JiTXsPDHZsNbn8Hg4WD OfD55J4eDUrZGsJBvACsqyyN7PThW1UE4OjC/+Hy6yrpH+DXOwD9i1lMscxHS12v 1OifQ6kYFtz+qyACjvo4m8ZzLt3AJdxvNWSxyNRGJVDwauf7K+lLkNBbR+ySVShf pQ7x6xOUXW75MUNqLMy7mLVuX8KJuJHNzmJP8T3TvKcFzY9kClyJx6zwR6trxh7y QYbZzPksi5/j059OWrnNFBAvOsdIXlODhxWbE4fhdText883Ge9NUIE42rn0ti8a w0Fe4MeFAgMBAAECggEAJvWw6OeGxwbbW3oIYM3aTq5BehWTcb09eDksdzym/Q4P o63/Deu/l0ojyM77vMKU+ZXRuWh1B2uHnWXKKVxcPXHEiJt2GmZ7MvDTkdPOy2ne zcSqGpYuz96rq4oqSrBiui9WYfNJ6uYRbLBd3Kf7ECALJQFJ6jGOQQGlLXaulb5U n5aYSsoEh+LcAgouI2Hu9AC+OCv3owynKL8HiWlLbR8yJJ5zaE9egiGWn/VbFu1g EA1wzVXyG2bIFghzt6bexg7DIDqsBOwLHD1lLE3WTgPCmDM2zoOxX5PlDKdFDVG8 Mnt/18FO5xiCpAC7ZMFA2Vd8udKvQd0LSxOVA8MZSQKBgQDVyKyXhLvt8KxepGhs /VmXn+AHLLL6w69Z3Vb1gj/oF8nZjJmN3ETcXKt861UqM23Q4WDhmDhRduWE1hXh elw3jVHkDMQn4Ke5Kv/rZ8aszm+fZKgCjB2AF7nUaJ+cU/oSWHFpk+/S/KZWiHWc mVkDxoBhXCi/6QyLLB8WJGwaewKBgQCi/1zwo/9z3CCKEn8baQkReUDmifaG4PVs ZEAsz0WQ/bphRBQllwoL6xXTTuGAczfoEonSyH+jfm2sLcysMRpyAAPI2Q//d+b2 AFm+eBH/45TGKvfD7klYj830sSzYaA6i/Z2DziG7fmC/auJmgtT1wQ5UMjD3Oghk lCxzn6oF/wKBgGyR/Gz6wQJG/xMVhd8MD2r8i6a5IbBOnwgRa69FVbVGF4G/cOBl pCcRfRn03gyPj87MFwqa5scgjdGXdAdNv/WKdLNPdHMYGbXlS5E+49ww/ulBEj4w 8G50HjDsbVrUHyUf+4D1248YNlWt+aTtEBLlxZ8sUZmc/nzTjHoPR0NvAoGAFSKr uIBrdWiLx5uSY8mA5YUlhz9IekDdUgrFz4mo6Z4c9tPPEPi+0sDO+bF2yCMokq0k tfJNqrOQIQ1nRsSvOy0JUJfk3Sl9B1UQTgRfwSCPgAq+SeeyFwu+lwYKXJ1RmIzu SdMGyLsgbHG9nbFFUACSjRRdCRG7WN9lzDBd6Z0CgYAeg3Be/Kox+anF2pRulDa3 Ro9UiVPrsJQv/0qKO8vLsJyDyCFmaut2v1XPQm1c50gaQ5Crn/a1IavgVyoU5Kl8 RQJsaS/5ZgA5Hm1XIdv6edCNn8bvFw6927aC5BsRuwFzPzplplfJ2fQRQpBtpJN+ E4ZylXnYyCN1ar3WSp6/eQ== -----END PRIVATE KEY-----"
}
}
```
The following are automatically published to the `AUTH_USERS_MASTERLIST` datastream:
1. new user's identifier
2. new user's description
1. new user's primechain address    
2. new user's primechain public key  
3. new user's RSA public key   

The newly created user's primechain private key and RSA private key are not published to any datastream.

## 1.1 User has multiple devices

If Samairah uses the Noodle Bank app on multiple devices, multiple on-boarding will be required e.g. 
```
{
  "user_identifier": "112345867",
  "user_description": "Samairah Nagpal's Noodle Bank app on her Android phone"
}
```

```
{
  "user_identifier": "112345867",
  "user_description": "Samairah Nagpal's Noodle Bank app on her iPhone"
}
```

```
{
  "user_identifier": "112345867",
  "user_description": "Samairah Nagpal's Noodle Bank app on her Windows tab"
}
```

## 1.2 Multiple users share the same device
If Samairah and her sister Sanya both have Noodle Bank accounts and use the same device, multiple on-boarding will be required e.g. 
```
{
  "user_identifier": "112345867",
  "user_description": "Samairah Nagpal's Noodle Bank app on her Android phone"
}
```
```
{
  "user_identifier": "222345867",
  "user_description": "Sanya Nagpal's Noodle Bank app on her Android phone"
}
```

# 2. Authentication
Authentication is a 13-step process. The user being authenticated is referred to as 'requester' and the user carrying out the authentication is referred to as the 'verifier'.

In this guide, we presume that Noodle Bank is the verifier and Samairah Nagpal is the requester. Their primechain addresses are: 
* `17SEyDKEwvA46U1FTUVVZWYgnR4X4L576vVAbp` (Noodle Bank) and    
* `16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA` (Samairah)

### Optional - Use of symmetric encryption
At any stage, you may optionally use AES symmetric encryption using `post /api/v1/encrypt_data_aes` and passing the data as the parameter:
```
{
  "data":"I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```
The output is the:
1. AES password   
2. AES initialization vector   
3. The AES authentication tag   
4. The encrypted data   
```
{
"status": 200,
"response": {
"aes_password": "o9tgRCETlHLZdNhlKKgdDshgiwvujn84",
"aes_iv": "LdjZLovqIkL3",
"aes_tag": {
"type": "Buffer",
"data": [
  210,
  255,
  136,
  213,
  61,
  82,
  117,
  102,
  222,
  62,
  93,
  134,
  245,
  113,
  100,
  82
],
},
"encrypted_data_aes": "4896275f060be692d50406292602e6cb53a6d30426c11b0658a8dc31ed196ef4841ffa8b9c8d6315f8798387f93157aa35bb5d280bf208d2bc645e2e184f0ea551a372b924b329b391b6ecf75f3fec3a1760ae306de25d3bc36cc30bf93cc9e3988c743c6925f109b6760bca77826bfd7673563b99"
}
}
```
To decrypt, use `post /api/v1/decrypt_data_aes` and pass the following parameters
1. Encrypted data
2. AES password   
2. AES initialization vector   
3. The AES authentication tag   
```
{
  "encrypted_data_aes": "4896275f060be692d50406292602e6cb53a6d30426c11b0658a8dc31ed196ef4841ffa8b9c8d6315f8798387f93157aa35bb5d280bf208d2bc645e2e184f0ea551a372b924b329b391b6ecf75f3fec3a1760ae306de25d3bc36cc30bf93cc9e3988c743c6925f109b6760bca77826bfd7673563b99",
  "aes_password": "o9tgRCETlHLZdNhlKKgdDshgiwvujn84",
    "aes_iv": "LdjZLovqIkL3",
    "aes_tag": 
      {
        "type": "Buffer",
        "data": 
        [
          210,
          255,
          136,
          213,
          61,
          82,
          117,
          102,
          222,
          62,
          93,
          134,
          245,
          113,
          100,
          82
        ]
      }
}

```
The output will be the decrypted data.
```
{
"status": 200,
"response": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
}
```

### Step 1 - Retrieving the RSA public key of the verifier

Samairah retrieves Noodle Bank's 'RSA public key' using `post /api/v1/get_rsa_key` and passing Noodle's 'primechain address' as a parameter.
```
{
  "primechain_address": "17SEyDKEwvA46U1FTUVVZWYgnR4X4L576vVAbp"
}
```
The output is Noodle Bank's 'RSA public key'.
```
{
"status": 200,
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkydbbI+68zjRmp0n7Yss NwKbUl1IzBEqgm0Rp/utue8VNPfZaW7YrnwmEO7jO939C0/xAgayE6vR5VT7sItX uMKwvP0DozxWtUGGcoHEZgImzSXJGomZpr2+M6TdW+kbisUUKbjIApQvnGlh93Zv XiRTsvMkxC1Lf8Wkj52V7Xdn7O2p1tGg/j4wv78kT9wJ67xEnBmsGpGUZZYPAMZr j0WrsakvT5vqwtkGum2OI9eRNlB7qgDsuOrxAm3jyx17s+tOi2Sasn1GywHQmU6n YpCSsVv6ywGCMH5xLGAWT3glGCx2mwjAi+/QbpSXIWorlzzlZOR2xI+844dyDxbW MQIDAQAB -----END PUBLIC KEY-----"
}
```

### Step 2 - Encrypting the blockchain address of the requester
Samairah encrypts her own 'primechain address' with Noodle Bank's 'RSA public key'. This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is Samairah's 'primechain address'   
2. `rsa_public_key` of Noodle Bank 

```
{
  "data": "16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA",
  "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkydbbI+68zjRmp0n7Yss NwKbUl1IzBEqgm0Rp/utue8VNPfZaW7YrnwmEO7jO939C0/xAgayE6vR5VT7sItX uMKwvP0DozxWtUGGcoHEZgImzSXJGomZpr2+M6TdW+kbisUUKbjIApQvnGlh93Zv XiRTsvMkxC1Lf8Wkj52V7Xdn7O2p1tGg/j4wv78kT9wJ67xEnBmsGpGUZZYPAMZr j0WrsakvT5vqwtkGum2OI9eRNlB7qgDsuOrxAm3jyx17s+tOi2Sasn1GywHQmU6n YpCSsVv6ywGCMH5xLGAWT3glGCx2mwjAi+/QbpSXIWorlzzlZOR2xI+844dyDxbW MQIDAQAB -----END PUBLIC KEY-----"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
{
"status": 200,
"encrypted_data_rsa": "acN4z1AbYKHbuK5Tixi+AgYwg/3XMqVxU3UJmZrXcRuSXYSPyDLrB7+BQeiazfcFk9WxpnvT8nXHkQ6Hz2rTUF1K1Lv5XM33iQMqdRUa9WzQGJS9IakS5TSw+OpxhCR0KWa1kJ4XIa6QHwCGqUQrUo7WXTV9k/Lb55eLZh9bINy6LAAeYQfQX7LZMVCuC7lmJcUAkDTYuccgZdtAc1BCHl0ODq7rcMSLpr/M0h+tjKE6fuGP9AuB7NznoAy+7yf9toy67DNIWAeQXptTq8ukBJ6AzBTerUbTrbwOWlBWOyVcnsyPkXRtPUNryu5Jvqlw6//w0Fc9FG3dM+lmuzWQ5A=="
}
```

### Step 3 - Sending the encrypted blockchain address to the verifier
Samairah sends the `encrypted_data_rsa` to Noodle Bank.

### Step 4 - Decrypting the encrypted blockchain address
Noodle Bank uses `post /api/v1/decrypt_data_rsa` to decrypt the `encrypted_data_rsa`. The parameters are:
1. Noodle Bank's RSA private key
2. The `encrypted_data_rsa`
```
{
  "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCTJ1tsj7rzONGa nSftiyw3AptSXUjMESqCbRGn+6257xU099lpbtiufCYQ7uM73f0LT/ECBrITq9Hl VPuwi1e4wrC8/QOjPFa1QYZygcRmAibNJckaiZmmvb4zpN1b6RuKxRQpuMgClC+c aWH3dm9eJFOy8yTELUt/xaSPnZXtd2fs7anW0aD+PjC/vyRP3AnrvEScGawakZRl lg8AxmuPRauxqS9Pm+rC2Qa6bY4j15E2UHuqAOy46vECbePLHXuz606LZJqyfUbL AdCZTqdikJKxW/rLAYIwfnEsYBZPeCUYLHabCMCL79BulJchaiuXPOVk5HbEj7zj h3IPFtYxAgMBAAECggEAY8GujK3zQqcmEPaw9qv+UVyHBxMOIqkQdFKUQZiwcPfP HJVY4cyvP7oR5DDOAuu+e0i6TXFUj1lPdXRjG4+a7Dmvrq6nJKXm8gF1r3KhPbX/ r9sJtd/KNeszYbdGCOTCMxTfUlld3cGvdQ1LyIKVhPCDfTCvn/5EzF2j7WgbF1tm oKuZB69LoVRSQ+rW9egQUWX5OCIC2aPReoRQCpPW3hz+CCuxk387twqlbS4/YFlB fdzC8N80umFvRFB8+YrgLrE/AM+dfFf8XMbwQDO13V4E6S5zVohAAJddxq7Nsv+e 1aZK+3NxlrkrOFij0ApLVtugToIBIMsGKbXuc5g6sQKBgQD9VIXvkX9fvr7wFgQ8 BDqDwavhUfQ3GdsZgzEnLK4SUgB1ApC7xMgwXauN38AL3kZEqQZNnWciQY8bU3i1 EFdFQ7K9n7s8nM/d8N/rbFIndRICJUQh47UAKWNZRaCV/IVMLPVjjHCjaej9aOUP JsyqbGfFA62rRCXoCHSzVjlFfwKBgQCUtF+PA0kP/V8CkaNV0VdRa702s57tu6Tg Quk8SOH4Ame9TcBrP95bpxUzBKapBj/ncW8lJKDD7zLYTQalWUG+KX/17i6NPgD6 vq+FwoCaGskRQTw3AUbkfHj6u7Cn41EmvxIZ2KWLi8Hl4+W3o6/mnsuucEZDOPwy FTN5FW+cTwKBgG0RTvjt86ENRrenQvtz9p1zbMT9u99dSm+ZhDgRjIBmvbui9x1g g7APJCVZCB4T/Lzi6MvR0O12vF5PedC60FgJ5ZKuirZ17Sjo4/9AC77hMHesA8Fz gCIpr5Rn3dO1fM5nLN9HP9ebaaxw1O3JDqTxN1wjUUpDdO6JdXUg0leRAoGBAI4l FSspos+MDSPxf0ZrQ6Jq8IW3kXYCZoqQq06bBJYEBpIoHoTmmnDV+Ce6jG0JslBU WEATETH6Foo4pt+rwHI8TTsSoKEW4ezOFg4wbKnibMz3pM2XhOKoMSTMAQObAVme T3kxZJ1NzN0pyc6Ow3gZ1u06GY/sivZ82aUm3nd1AoGAIqGOv9GiNYWJIdsdGmhI YS93Qj3Pw6ZSTqGTW4FYM9f4tawEWaGFGBL2CBYEp9nUTUBEAq8HJes0bimeScGn Tawewg84U4oiHuyTbtwIi5PkB+XIKfGaXU3SMaHYHiORRe7BhQwWKHpLdob4JJtm CdNBuN+I1w9yaWG1TeWVjk8= -----END PRIVATE KEY-----",
  "encrypted_data_rsa": "acN4z1AbYKHbuK5Tixi+AgYwg/3XMqVxU3UJmZrXcRuSXYSPyDLrB7+BQeiazfcFk9WxpnvT8nXHkQ6Hz2rTUF1K1Lv5XM33iQMqdRUa9WzQGJS9IakS5TSw+OpxhCR0KWa1kJ4XIa6QHwCGqUQrUo7WXTV9k/Lb55eLZh9bINy6LAAeYQfQX7LZMVCuC7lmJcUAkDTYuccgZdtAc1BCHl0ODq7rcMSLpr/M0h+tjKE6fuGP9AuB7NznoAy+7yf9toy67DNIWAeQXptTq8ukBJ6AzBTerUbTrbwOWlBWOyVcnsyPkXRtPUNryu5Jvqlw6//w0Fc9FG3dM+lmuzWQ5A=="
}
```
The output is the decrypted data, which in this case is Samairah's 'primechain address'.
```
{
"status": 200,
"decrypted_data": "16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA"
}
```

### Step 5 - Retrieving the RSA public key of the requester
Noodle Bank retrieves Samairah's 'RSA public key' using `post /api/v1/get_rsa_key` and passing Samairah's 'primechain address' as a parameter.
```
{
  "primechain_address": "16g8d8U3K3PbcvY6LYafgZ23JrnxRXwZqBP8sA"
}
```
The output is the 'RSA public key' of the requester.
```
{
"status": 200,
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAiB49uOAIfw2nGsueboVL +CWPYqiYS/+pYrUjoCe3owwn395o68IPmYDm2NCYk17Dwx2bDW5/B4OFgznw+eSe Hg1K2RrCQbwArKssjez04VtVBODowv/h8usq6R/g1zsA/YtZTLHMR0tdr9Ton0Op GBbc/qsgAo76OJvGcy7dwCXcbzVkscjURiVQ8Grn+yvpS5DQW0fsklUoX6UO8esT lF1u+TFDaizMu5i1bl/CibiRzc5iT/E907ynBc2PZApcices8Eera8Ye8kGG2cz5 LIuf49OfTlq5zRQQLzrHSF5Tg4cVmxOH4XU3sbfPNxnvTVCBONq59LYvGsNBXuDH hQIDAQAB -----END PUBLIC KEY-----"
}
```

### Step 6 - Generating a random string and timestamp and hash
Noodle Bank generates a 512-character random string and the current GMT timestamp. For this it uses `get /api/v1/create_string_timestamp` and gets an output like:
```
{
"status": 200,
"response": {
"string": "mroHlYTyC5gtYD3NcvS0vKG0rIrQOOF1DmdfMl5NCFBg7Xi0Yf9xsKSN987OUwcnSKfoGn6qZAOg7m87C3BzgpGL8WYcPlLfDgJhBl88THhfhGjIxnkOdrGtiiWzWBdRbQvRsj9FBc5q6kPQHJ8tXuZt3LRnN09JTEAMDZWoVj0ChTAn8AjN8sYbiIpTmEZRHoFGz1bvVNSlkEBNd2ju9G10MkkFcsezOpckT6pityTGvVPvYS5Zh8MjLOP7KhoW1GTYb7mRyMCsoJso6yxQ1Q2TRZOq4N0BMeajUBaLeubMpk7Dq1qado9Dk6xSvLFkBzsnj3BO7rT5T6M2zB8j8Zusf90vtu8e51CJNG1tbiBFXijuiQJt51Qi6sXYaCAX89FNmXDKCICNAlwnuttYc8N5AgYoUtnFBVQ4Uxsu3gueNlRq9qOFrD9LZ3P8dnVv7oCng1CjK4jNELUOzQFfFtikGu1j5OOw5IcqGNXhDGalUzQZ2eqWpiznzheE8W6a",
"timestamp": 1544601150,
"hash": "e7d0265f614a53dada9ecbe2555930cb4cfc3fc1accf6afb18b35a3619baff59f0dce692edcd51e2284fb8f72cecaf75a6ab5e6cdbfabafcbc1020f606d6fd82"
}
}
```
Note: The `hash` is the SHA-512 hash of `string^timestamp`  

The `string` and `timestamp` are stored in Noodle Bank's private database.

The `hash` is encrypted with Samairah's RSA public key and sent to her. This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is the hash   
2. `rsa_public_key` of Samairah
```
{
	"data": "e7d0265f614a53dada9ecbe2555930cb4cfc3fc1accf6afb18b35a3619baff59f0dce692edcd51e2284fb8f72cecaf75a6ab5e6cdbfabafcbc1020f606d6fd82",
	"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAjAcsDs6uRwW2EpqRwmOt ZYXPID+rWvcV3ZKmGUr4mUictf/RVk0/o8Q/pGbeeKqfNXTBfvAh4ZcaFmXP3p98 5JtSXS/tDw8/6nkZjLHbb3RDYSGhwMzd5DAkNILd0wwqh1QCdrlda7n4ZXrU77dg CRoWBPwUY8ItZSgOHFhdmU7acmI4iNNPKRfDPzJ5PefquqFrKQCbK7yVL1DnKPX7 56XowLHpYrutlYr9ZaOgZKWaA6NR8ThVVdyhTpU3FhigwdR5UGtAjVU08Ot14H9F 6rUyqtHINjfTQyMxDYiwVmfcAW0UJ1Nsp/ZkBOAUG+FOymHtYTsNbtacMkPi2O16 WwIDAQAB -----END PUBLIC KEY-----"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
{
"status": 200,
"encrypted_data_rsa": "HuQ6xjyEN9nayNAHg34enp89It2e10iew0mh3zyc7ZSMtz/i6weuai+PrLdR+LL3KbITQSJZHA1XDkKNvz7GmV6eDSX7meZWMXQJDVpBYeQYV+v38bGlAFOTmGosCeaK+CeLFYPkC6J1SKulHU07hSNdO4BGkek0/au87ztK2RLo5E7qUjGOtxbfu5zMQEYBghNhXVxfD2jO+Jr8zzkoRPeq7yfKtYtjtR68u6emIkRJIh08KHXZarplHFeDnaJ1onqZMWYB0BbBSJDVt06S4PFzceMk5pdF5MwUe9y8OSzdeD0jsmGfG/YLEtpNSc2IxCO0OtYgw3XbWbnbZvVntA=="
}
```

### Step 7 - Sending the hash to the requester
Noodle Bank sends the `encrypted_data_rsa` to Samairah.

### Step 8 - Decryption of the hash
Samairah decrypts the encrypted value using her own RSA private key. Samairah uses `post /api/v1/decrypt_data_rsa` to decrypt the `encrypted_data_rsa`. The parameters are:
1. Samairah's RSA private key
2. The `encrypted_data_rsa`
```
{
	"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCMBywOzq5HBbYS mpHCY61lhc8gP6ta9xXdkqYZSviZSJy1/9FWTT+jxD+kZt54qp81dMF+8CHhlxoW Zc/en3zkm1JdL+0PDz/qeRmMsdtvdENhIaHAzN3kMCQ0gt3TDCqHVAJ2uV1rufhl etTvt2AJGhYE/BRjwi1lKA4cWF2ZTtpyYjiI008pF8M/Mnk95+q6oWspAJsrvJUv UOco9fvnpejAseliu62Viv1lo6BkpZoDo1HxOFVV3KFOlTcWGKDB1HlQa0CNVTTw 63Xgf0XqtTKq0cg2N9NDIzENiLBWZ9wBbRQnU2yn9mQE4BQb4U7KYe1hOw1u1pwy Q+LY7XpbAgMBAAECggEBAIE2YQ5s496/w2pZXaVuC2SCXEYa2ol/NZsXptPyHYJ8 wbckD8y+TbpV7pBLKIFamL1gNulmty0PHNCMNIvuyfW96fv5rJvX65f3FX+B48Zu F3r66OMbaKoXTmFyXTVRpbDo8bkShcVRf4hNF074/NKJUsZYwovnc7JDivnXBM/g z1KtiR+IzUUBjO/6Vsax6Fdw30tzBhV18serm0Kqa1Fgk8gJrrnfWHm7aQQUj+PE BhwMtFGU89p1bJ4CML9x/NC5aPjpQSg1XfWbB3vn/K2Iea498q+jjSlOLrhGef4e MydqPMwiQ3UxkYvO431kB5UITxZHf9mYm7ucY02hnNkCgYEA8CqQFL1B2ARMVPqp hEgDk6CAfE9kkMmC5G9yBXitfYoT9BirIAhYjiXtoiXVrY8Wv0fsArF/Re7DtgeP qBkeeYLz5TKncVVbSuFak6xpA2DomKDUTFCvZf5A0pcNbclO85Lt1AbbLtBkOmaY V8dZVDdFC0W2PfUSpFMnusXLeOcCgYEAlUKDWVX4tWj2Pr58nBxWu4ySMTHlFNVT HjMGA17jsrNrQFRw3+aWxjamTEUvxczvegj2o+XpQLaG7hCz46t0yWOrvvEVPgpp njlVo+Zx1mZwZO1FESE3FENtNTeeScZOvE6OZ39xyalF2BlNY9BSxbx1YHbz0wog dyuFqxP9AG0CgYEAhOG36JGyrbfrGBW812EVAYiLrrwq02V7k7MJ7ncP3ucYFTXU 8RtNDBF2QwIWETqbhmhf8DmPRv1NshjK5mJHl0nacpUtSirFIVBA0nZRgDoNV+2c qUD3W0JrUVmcZ4M7uM8x4d+NRICvBBUh82dsSIlwHUWMCQnhL6SG1fN8mj8CgYBg OehKUPWtpsSSQOY/EroL4Z1iX+NrYfhbENQAmk07qRYs/ANlJdjwYs0lgLlC0VNW nq67jX6qPMKSemwvDBuXtk1EJVLnk3jyC86dgvTDH3m4Z4tOdtZ2lt2yIHBI6bNb DV4bdXtbYmjn37AX+HdUiaI2lZmt5ep2SbW8TH+gpQKBgG3j7+t5N9wsCMv0JuS3 k1Kx2gY2tJfn3+JWd5FNPh5HUwD+gkJyuX2sJSKk8o3xHvxcM/2SCHoqLHUdXbQ9 q0AEVEwy6XV1wsJ+6ASoA+CbcL3mllIbB1E+fYiA4km9RabHwTbh82rogsOUMPXm 9qVefyQneafYs+zz1RuX0ya3 -----END PRIVATE KEY-----",
	"encrypted_data_rsa": "HuQ6xjyEN9nayNAHg34enp89It2e10iew0mh3zyc7ZSMtz/i6weuai+PrLdR+LL3KbITQSJZHA1XDkKNvz7GmV6eDSX7meZWMXQJDVpBYeQYV+v38bGlAFOTmGosCeaK+CeLFYPkC6J1SKulHU07hSNdO4BGkek0/au87ztK2RLo5E7qUjGOtxbfu5zMQEYBghNhXVxfD2jO+Jr8zzkoRPeq7yfKtYtjtR68u6emIkRJIh08KHXZarplHFeDnaJ1onqZMWYB0BbBSJDVt06S4PFzceMk5pdF5MwUe9y8OSzdeD0jsmGfG/YLEtpNSc2IxCO0OtYgw3XbWbnbZvVntA=="
}
```
The output is the decrypted data, which in this case is the hash.
```
{
"status": 200,
"decrypted_data": "e7d0265f614a53dada9ecbe2555930cb4cfc3fc1accf6afb18b35a3619baff59f0dce692edcd51e2284fb8f72cecaf75a6ab5e6cdbfabafcbc1020f606d6fd82"
}
```

### Step 9 - Signing of the hash by the requester
Samairah signs the hash using her 'primechain private key'. For this she uses `post /api/v1/create_signature` and passes the following parameters:
1. The data to be signed (hash in this case)   
2. Samairah's private key
```
{
  "data": "e7d0265f614a53dada9ecbe2555930cb4cfc3fc1accf6afb18b35a3619baff59f0dce692edcd51e2284fb8f72cecaf75a6ab5e6cdbfabafcbc1020f606d6fd82",
  "primechain_private_key": "VEjwBWC6mgp8CNFPguZwt997rB5JCExQzB7wavwgKSZimBmaeKwPWdKH"
}
```
The output is the digital signature.
```
{
"status": 200,
"signature": "H60blR7quU3GD5S3Apdh1uqM7ydEzMNRiQNAtKi6uOkdMhO14bjZpopURvbCoRKCsXusBRL7Yx03QiW0lvHO554="
}
```

### Step 10 - Creating the encrypted envelope
Samairah creates an 'encrypted envelope' containing the following:
1. the digital signature 
2. Samairah's primechain address
3. the data that has been signed (hash in this case)

This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`
2. `rsa_public_key` of Noodle Bank
```
{
  "data": 
        {
           "signature":"H3i7JTbIfwe/jf05z3ea+O/Ljl0DHLg7MzTc4RE6FRd7M79SLGgq1zzuPkzffXHjecbcAMLtjHqoxUVRskSHfmQ=" ,
           "primechain_address":"1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn", 
         "data":"d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8"    
         },
  "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1XUamZGgGBIKgUdXW35b 9V1PQ6jjv87erZY6XxW1RvdSBxfnYKIF+6FgTX1x/Rz54ynZagTA0CkdkYp+yKrG U53Cg/4vNl6MV2Ky/YgrBr1pOZzo89AyAt7u0lAPmkOXsewVTSSfQteQN4UoCtKh fPPgGiMlgKNvbH0pl3mD7USqI3Zo9VLm+P4qdyPG75mSu4t6i+xLWQOe9FtYUaR+ dy8OB8PBGIgkx3Q9Ik0xtBNTcYRAunJXULFy0T2xvmv73PS1OrJgNwXHEm/IDI+/ 5amvxtQirt7VBeubfQIyBcBGKSve2BRs2Fuw1ftZ4usSmgUTMZSi2NUU1Fhw1vQo WwIDAQAB -----END PUBLIC KEY-----"
}

```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
{
"status": 200,
"encrypted_data_rsa": "KVzEEUAnMZMLFMK0FV+GHI6B4fY5q49zf9l6BNt4LXOJBVba/J0y1g5SX1K4Ol0S8p7z+0yOWUkXllU6wu99Sw6VntCJJK21zlyKGEtqGpReEXsS42ibXY+wMmoEU/aVd84pLIbfSAc5vBP5OpvmMD3/JPiPtDFqqIuEnadAerjoCwWpBsdxBm+YWB0nOpwabz7rpamjvrsS3Q3f3p67T+a/CM9JzrZxwG/UBbqbxWU2dPfpy7YuqFSLEuQj0DAPOOv3hCcaIQAXdWejcURyxTB7ZIpos+od5Wnsx/2e6ANMHgSJqCiLAs0xzOa8uLeLV8hFQk9HoKSB412kTR4PESL6n3NqRkQh403ui5EvP02j5bF+B7i/xA7EQfuVIj8F28woH3pOJ4rrKGPl7J11VV8R6OoQbo6d4n6tIQDdS2mpYcjzdpEWeM7PGCB0mRRDxJaToBV35Z5WvBPVO/ug1Eh4eQP+7YlTVEliDjEggX2GrEH945kK3oCxsDwysmR1w5fQUeguflejMYvSOHrcIVOl/0Z/t1WFtD6TYVcs4xKYiPKPbdzlm85S3q4ArlNi3yo47zLWYvGs11QbiOvetTDhSYKSq8YiTgbPC9vDhZVgxvNbZe+k9psQOvtljF0WjYarmuHGyQTv9vpY7eziEnSHCPH++LKwF+RkwMVOmJM="
}
```

### Step 11 - Sending the encrypted envelope to the verifier
Samairah sends the encrypted envelope to Noodle Bank.

### Step 12 - Decrypting of the encrypted envelope by the verifier
Noodle Bank uses `post /api/v1/decrypt_data_rsa` to decrypt the `encrypted_data_rsa`. The parameters are:
1. Noodle Bank's RSA private key
2. The `encrypted_data_rsa`
```
{
  "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEugIBADANBgkqhkiG9w0BAQEFAASCBKQwggSgAgEAAoIBAQDVdRqZkaAYEgqB R1dbflv1XU9DqOO/zt6tljpfFbVG91IHF+dgogX7oWBNfXH9HPnjKdlqBMDQKR2R in7IqsZTncKD/i82XoxXYrL9iCsGvWk5nOjz0DIC3u7SUA+aQ5ex7BVNJJ9C15A3 hSgK0qF88+AaIyWAo29sfSmXeYPtRKojdmj1Uub4/ip3I8bvmZK7i3qL7EtZA570 W1hRpH53Lw4Hw8EYiCTHdD0iTTG0E1NxhEC6cldQsXLRPbG+a/vc9LU6smA3BccS b8gMj7/lqa/G1CKu3tUF65t9AjIFwEYpK97YFGzYW7DV+1ni6xKaBRMxlKLY1RTU WHDW9ChbAgMBAAECgf8RgomsD0YSs2gpMrD30GW6uuzFoBUOpumdU7V2F1HHgII6 ErvoMWJMQfCkaqXvHXFiMQykpb8rVDQYvEOqMlgSg95w9WjqDNd2U6JbKdBdvSvk jfqOBYYUtjThC7A79096SON2cIqf8Q7jfwjJ2n1kwpyfiEKLStzZCWtgAZfQ3qq5 wgatNWHWTjokVukWvK3zMamPEP9dOw97/Oo6i6wT/VeKM8d/p5fKoEUNSEBYzJkp CoxGIFpy8s1X3QvxJB9cLomY/JTrMsynIR7YimBmVAtlY2pndsXjC3aVR+WN6MtZ RCwzccA+JqmNiZr63MWIlKmCil/muGJG5UngbPECgYEA7wjahkoMSqyD4bt5ceFt FFMTb6qooW7DFj2ZVlr+NJ4DMieve0IhkOZenTGpSAGlyY7wJXnRCET2fTnEf0R7 OX+Nap/sVxAOaXRSupsvvauUjp2ETjhxSnZHhLPr3z9lj08lIDHUoo9QS5hbpwsK as2ojjLrKxEcaEGKHpeoqNkCgYEA5JuGiAnwj408jGudgJiQ146VJkYYT1UvKqn6 F7QVNg4OW4QckqBZRUwhEZSUBpluNQuLeO9EVDjQR16ZBBYgvEFQKLj0nJdcUz11 JiAsiQzrJIWPE/HM587QlTnr5xHcjyJuGnon/tyGdQptAd5dlsgQ/ctt7EypAfDr /7B+elMCgYBrt2SqUWIaoIVJyu7eV8SM/SbsEk6teLlnI1kfJiAZ2/76shGNDO8N WhLW6ZMsRLnOC6DCcpO1E0a0hby70UNqVMWIgArD7RNhiC7jsp0f7tsiLW96xEqh UI3ICkBHuUzt+K91Q59bphN8DWt36izGlmjXs7BwFuTjQm2YfaVeeQKBgCjo7BpM LRCDZeJ7H6RzqPfqPCatRIxt4hLweCDlySXzPf6Cldpnd5I/HWvX+uVzb5Vui3cI 2mF4CU28UAW7MACAb6fZ8WxUaeE7jktUVqPv++R9Qi1/h/uztv/9bYncWGwE7U8v rRievjETvI4pDPZ+twuz6+ftkBEY3CLVosyhAoGAdAIMNkZGPDdeWSGO6Zl3SBYf hhsFJc3nn9pNKhPgXZUvioAi+I9POljFJQgn9Y9OYYpp7b7L1lCP0D9cgOkju7UX DScZTRml7urq8lNqHR/dS8fKo4Z0JEowhmtUBH4clv5hOaY9EjG2w/kNZCdxDbJU b8SwjFWTl8KUu3O7N/g= -----END PRIVATE KEY-----",
  "encrypted_data_rsa": "KVzEEUAnMZMLFMK0FV+GHI6B4fY5q49zf9l6BNt4LXOJBVba/J0y1g5SX1K4Ol0S8p7z+0yOWUkXllU6wu99Sw6VntCJJK21zlyKGEtqGpReEXsS42ibXY+wMmoEU/aVd84pLIbfSAc5vBP5OpvmMD3/JPiPtDFqqIuEnadAerjoCwWpBsdxBm+YWB0nOpwabz7rpamjvrsS3Q3f3p67T+a/CM9JzrZxwG/UBbqbxWU2dPfpy7YuqFSLEuQj0DAPOOv3hCcaIQAXdWejcURyxTB7ZIpos+od5Wnsx/2e6ANMHgSJqCiLAs0xzOa8uLeLV8hFQk9HoKSB412kTR4PESL6n3NqRkQh403ui5EvP02j5bF+B7i/xA7EQfuVIj8F28woH3pOJ4rrKGPl7J11VV8R6OoQbo6d4n6tIQDdS2mpYcjzdpEWeM7PGCB0mRRDxJaToBV35Z5WvBPVO/ug1Eh4eQP+7YlTVEliDjEggX2GrEH945kK3oCxsDwysmR1w5fQUeguflejMYvSOHrcIVOl/0Z/t1WFtD6TYVcs4xKYiPKPbdzlm85S3q4ArlNi3yo47zLWYvGs11QbiOvetTDhSYKSq8YiTgbPC9vDhZVgxvNbZe+k9psQOvtljF0WjYarmuHGyQTv9vpY7eziEnSHCPH++LKwF+RkwMVOmJM="
}
```
The output is the decrypted data referred to as `decrypted_data`
```
{
  "status": 200,
  "decrypted_data": "     
    {
      "signature":"H3i7JTbIfwe/jf05z3ea+O/Ljl0DHLg7MzTc4RE6FRd7M79SLGgq1zzuPkzffXHjecbcAMLtjHqoxUVRskSHfmQ=",
      "primechain_address":"1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn",
      "data":"d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8"
     }"          
}
```
### Step 13 - Verification of the digital signature
Noodle Bank verifies the digital signature using `post /api/v1/verify_signature` and passes the following parameters:
1. The data to be verified   
2. Samairah's primechain address   
3. The signature
```
{
   "primechain_address":"1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn",
  "data":"d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8"
   "signature":"H3i7JTbIfwe/jf05z3ea+O/Ljl0DHLg7MzTc4RE6FRd7M79SLGgq1zzuPkzffXHjecbcAMLtjHqoxUVRskSHfmQ="
}
```
The output will be `true` if the signature is valid and `false` if the signature is invalid or if an error occurs.
```
{
"status": 200,
"response": true
}
```
```
{
"status": 200,
"response": false
}
```
If the signature is valid, the entity is verified.

Noodle Bank also uses the stored timestamp to confirm that the signature is returned within a pre-set interval e.g. 30 seconds.
