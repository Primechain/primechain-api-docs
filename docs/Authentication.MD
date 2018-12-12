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
* `12pdAHR1Jurv7oSULBxDE7QPBUfDKtAg5t4u3v` (Noodle Bank) and    
* `1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn` (Samairah)

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
"response": 
  {
    "aes_password": "S3N6GudzJJ8bhC6H7PzwlEKX5s7dUTjy",
    "aes_iv": "kMPCFmXF3DjF",
    "aes_tag": 
      {
        "type": "Buffer",
        "data": 
        [
          50,
          109,
          253,
          2,
          12,
          90,
          85,
          124,
          20,
          45,
          241,
          247,
          11,
          82,
          229,
          113
        ],
      },
    "encrypted_data_aes": "d3786f4a9f8f0e36475327b6f3a26d5c582ea31b87dae25a63bd2abecdd092287be32fac3205d56ddafa55d6f173a947a33bc417065f451bbffe7c0c62a7a2adedad0c14f842c05ad99fc9b36a20865c0f15b7e6a0b77b9c1538bf2a3a5b9c5ba6a510c73b072d8fbcee359575a1d253a05605be37"
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
  "encrypted_data_aes": "d3786f4a9f8f0e36475327b6f3a26d5c582ea31b87dae25a63bd2abecdd092287be32fac3205d56ddafa55d6f173a947a33bc417065f451bbffe7c0c62a7a2adedad0c14f842c05ad99fc9b36a20865c0f15b7e6a0b77b9c1538bf2a3a5b9c5ba6a510c73b072d8fbcee359575a1d253a05605be37",
  "aes_password": "S3N6GudzJJ8bhC6H7PzwlEKX5s7dUTjy",
    "aes_iv": "kMPCFmXF3DjF",
    "aes_tag": 
      {
        "type": "Buffer",
        "data": 
        [
          50,
          109,
          253,
          2,
          12,
          90,
          85,
          124,
          20,
          45,
          241,
          247,
          11,
          82,
          229,
          113
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
  "primechain_address": "12pdAHR1Jurv7oSULBxDE7QPBUfDKtAg5t4u3v"
}
```
The output is Noodle Bank's 'RSA public key'.
```
{
"status": 200,
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1XUamZGgGBIKgUdXW35b 9V1PQ6jjv87erZY6XxW1RvdSBxfnYKIF+6FgTX1x/Rz54ynZagTA0CkdkYp+yKrG U53Cg/4vNl6MV2Ky/YgrBr1pOZzo89AyAt7u0lAPmkOXsewVTSSfQteQN4UoCtKh fPPgGiMlgKNvbH0pl3mD7USqI3Zo9VLm+P4qdyPG75mSu4t6i+xLWQOe9FtYUaR+ dy8OB8PBGIgkx3Q9Ik0xtBNTcYRAunJXULFy0T2xvmv73PS1OrJgNwXHEm/IDI+/ 5amvxtQirt7VBeubfQIyBcBGKSve2BRs2Fuw1ftZ4usSmgUTMZSi2NUU1Fhw1vQo WwIDAQAB -----END PUBLIC KEY-----"
}
```

### Step 2 - Encrypting the blockchain address of the requester
Samairah encrypts her own 'primechain address' with Noodle Bank's 'RSA public key'. This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is Samairah's 'primechain address'   
2. `rsa_public_key` of Noodle Bank 

```
{
  "data": "1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn",
  "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1XUamZGgGBIKgUdXW35b 9V1PQ6jjv87erZY6XxW1RvdSBxfnYKIF+6FgTX1x/Rz54ynZagTA0CkdkYp+yKrG U53Cg/4vNl6MV2Ky/YgrBr1pOZzo89AyAt7u0lAPmkOXsewVTSSfQteQN4UoCtKh fPPgGiMlgKNvbH0pl3mD7USqI3Zo9VLm+P4qdyPG75mSu4t6i+xLWQOe9FtYUaR+ dy8OB8PBGIgkx3Q9Ik0xtBNTcYRAunJXULFy0T2xvmv73PS1OrJgNwXHEm/IDI+/ 5amvxtQirt7VBeubfQIyBcBGKSve2BRs2Fuw1ftZ4usSmgUTMZSi2NUU1Fhw1vQo WwIDAQAB -----END PUBLIC KEY-----"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
{
"status": 200,
"encrypted_data_rsa": "UiP5ggF10c9onAxpvCgO116XcnZx9oBZ7+odcUziubmnfashhtavDf6vAzZ24ZnLEwvZPWOexyV/xKCCpXzZb4fxCI5T1xQvIVRSxjqFVmoltrc74Xg6y8DPWkItKf5ahZJEZSp5Oi+3TbH/LxQ6MIpQo/5//5PdlGgrN1xMiWW9YLBZhL2oEw46wUdBVbZkR2BOsUIDRXVmy8OkC8Ouzb3zk0bcGbrsmCvinHArh+z2S5NaqgGX/Bl9FBBw7xGzINbWVvH99nRQNXXM3xgrBJm/DjGJW+t9x7OAAp5+RxzzgKxgTAA5J9fGMkkHFf0SKJBnJlI7TDti3/iuPAoztA=="
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
  "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEugIBADANBgkqhkiG9w0BAQEFAASCBKQwggSgAgEAAoIBAQDVdRqZkaAYEgqB R1dbflv1XU9DqOO/zt6tljpfFbVG91IHF+dgogX7oWBNfXH9HPnjKdlqBMDQKR2R in7IqsZTncKD/i82XoxXYrL9iCsGvWk5nOjz0DIC3u7SUA+aQ5ex7BVNJJ9C15A3 hSgK0qF88+AaIyWAo29sfSmXeYPtRKojdmj1Uub4/ip3I8bvmZK7i3qL7EtZA570 W1hRpH53Lw4Hw8EYiCTHdD0iTTG0E1NxhEC6cldQsXLRPbG+a/vc9LU6smA3BccS b8gMj7/lqa/G1CKu3tUF65t9AjIFwEYpK97YFGzYW7DV+1ni6xKaBRMxlKLY1RTU WHDW9ChbAgMBAAECgf8RgomsD0YSs2gpMrD30GW6uuzFoBUOpumdU7V2F1HHgII6 ErvoMWJMQfCkaqXvHXFiMQykpb8rVDQYvEOqMlgSg95w9WjqDNd2U6JbKdBdvSvk jfqOBYYUtjThC7A79096SON2cIqf8Q7jfwjJ2n1kwpyfiEKLStzZCWtgAZfQ3qq5 wgatNWHWTjokVukWvK3zMamPEP9dOw97/Oo6i6wT/VeKM8d/p5fKoEUNSEBYzJkp CoxGIFpy8s1X3QvxJB9cLomY/JTrMsynIR7YimBmVAtlY2pndsXjC3aVR+WN6MtZ RCwzccA+JqmNiZr63MWIlKmCil/muGJG5UngbPECgYEA7wjahkoMSqyD4bt5ceFt FFMTb6qooW7DFj2ZVlr+NJ4DMieve0IhkOZenTGpSAGlyY7wJXnRCET2fTnEf0R7 OX+Nap/sVxAOaXRSupsvvauUjp2ETjhxSnZHhLPr3z9lj08lIDHUoo9QS5hbpwsK as2ojjLrKxEcaEGKHpeoqNkCgYEA5JuGiAnwj408jGudgJiQ146VJkYYT1UvKqn6 F7QVNg4OW4QckqBZRUwhEZSUBpluNQuLeO9EVDjQR16ZBBYgvEFQKLj0nJdcUz11 JiAsiQzrJIWPE/HM587QlTnr5xHcjyJuGnon/tyGdQptAd5dlsgQ/ctt7EypAfDr /7B+elMCgYBrt2SqUWIaoIVJyu7eV8SM/SbsEk6teLlnI1kfJiAZ2/76shGNDO8N WhLW6ZMsRLnOC6DCcpO1E0a0hby70UNqVMWIgArD7RNhiC7jsp0f7tsiLW96xEqh UI3ICkBHuUzt+K91Q59bphN8DWt36izGlmjXs7BwFuTjQm2YfaVeeQKBgCjo7BpM LRCDZeJ7H6RzqPfqPCatRIxt4hLweCDlySXzPf6Cldpnd5I/HWvX+uVzb5Vui3cI 2mF4CU28UAW7MACAb6fZ8WxUaeE7jktUVqPv++R9Qi1/h/uztv/9bYncWGwE7U8v rRievjETvI4pDPZ+twuz6+ftkBEY3CLVosyhAoGAdAIMNkZGPDdeWSGO6Zl3SBYf hhsFJc3nn9pNKhPgXZUvioAi+I9POljFJQgn9Y9OYYpp7b7L1lCP0D9cgOkju7UX DScZTRml7urq8lNqHR/dS8fKo4Z0JEowhmtUBH4clv5hOaY9EjG2w/kNZCdxDbJU b8SwjFWTl8KUu3O7N/g= -----END PRIVATE KEY-----",
  "encrypted_data_rsa": "UiP5ggF10c9onAxpvCgO116XcnZx9oBZ7+odcUziubmnfashhtavDf6vAzZ24ZnLEwvZPWOexyV/xKCCpXzZb4fxCI5T1xQvIVRSxjqFVmoltrc74Xg6y8DPWkItKf5ahZJEZSp5Oi+3TbH/LxQ6MIpQo/5//5PdlGgrN1xMiWW9YLBZhL2oEw46wUdBVbZkR2BOsUIDRXVmy8OkC8Ouzb3zk0bcGbrsmCvinHArh+z2S5NaqgGX/Bl9FBBw7xGzINbWVvH99nRQNXXM3xgrBJm/DjGJW+t9x7OAAp5+RxzzgKxgTAA5J9fGMkkHFf0SKJBnJlI7TDti3/iuPAoztA=="
}
```
The output is the decrypted data, which in this case is Samairah's 'primechain address'.
```
{
"status": 200,
"decrypted_data": "1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn"
}
```

### Step 5 - Retrieving the RSA public key of the requester
Noodle Bank retrieves Samairah's 'RSA public key' using `post /api/v1/get_rsa_key` and passing Samairah's 'primechain address' as a parameter.
```
{
  "primechain_address": "1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn"
}
```
The output is the 'RSA public key' of the requester.
```
{
"status": 200,
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSMswu6s2N2Ars4y6WyA 9OqWPRrx/5+6CFKa0cFak42xjWCQ5JBI8CSal8sQiebCNMCxpGwLcdFHv5ufJOt2 He3jzgU8hw1kPjzw+ONryz88flVqVXwTv2Yzd93IEvDl4rAIADDarso0McA6wvAz KfjQcoYcl1iHGxcFYUgUzDOZNStw8vPWJ7cogJZRuQTolN1X8BMczWJvXEeaLBCT HEt9QBTEGDsJqNBYLZkSEBA3ozS+02jE6fg7DpMU2KhbVO4MtTlmXvjM31+95Mk3 9XDSESLP0l8Nosd79L33r5Q38enfL8KCs6AYY18qvPIRE28IYFLzkzCvV5TJfTnG mQIDAQAB -----END PUBLIC KEY-----"
}
```

### Step 6 - Generating a random string and timestamp and hash
Noodle Bank generates a 512-character random string and the current GMT timestamp. For this it uses `get /api/v1/create_string_timestamp` and gets an output like:
```
{
  "status": 200,
  "response": 
    {
      "string": "WN2kwi7Bi4OslUaGRHP427AE0NFXriDhayjFSZUnY7jkvaBdFlEg9or7OAlDQwkmPp3BoS5qbzK1bha9jqHuZUhMV8VM6POSz8YGHjtiQVEyPaejquIZqfdt8Wto3A4b5hRfYkOAGpzhNhGLCYuiDQqTzfZNy3gnpyOartX7z2NMpdz8Y3mOCtS3KtzRG2T9Ah2t9vMIW02IlZ7RgdkOZgG76rOhtdXQT8dMlMkI4o5mtkBUzq9Sdo8yZR7Th6TCYcGMsZiyuYLuSNr03NpJhS23RWfgb58YFH0AdEacHor0ebIAmmi7aXqMnCrHYZUo2M2EPdh3IuqEyVPAxHmp2nvgzMM5hNzw7fUowCxPC9q33SvYnsZC4EsCwyj6SywN1KGgwVPnvyCYTSQcbETZdlivt4XwlE7HwnNSUhJbufODUBoPiPubRCsWh4qacNdlducONVCtiIvbYxpKr3KLFIUtHMv5I8g0gcMJWinIrNV0c2XvKjkxKADV1BDqZA0X",
      "timestamp": 1544090758,
      "hash": "d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8"
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
  "data": "d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8",
  "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSMswu6s2N2Ars4y6WyA 9OqWPRrx/5+6CFKa0cFak42xjWCQ5JBI8CSal8sQiebCNMCxpGwLcdFHv5ufJOt2 He3jzgU8hw1kPjzw+ONryz88flVqVXwTv2Yzd93IEvDl4rAIADDarso0McA6wvAz KfjQcoYcl1iHGxcFYUgUzDOZNStw8vPWJ7cogJZRuQTolN1X8BMczWJvXEeaLBCT HEt9QBTEGDsJqNBYLZkSEBA3ozS+02jE6fg7DpMU2KhbVO4MtTlmXvjM31+95Mk3 9XDSESLP0l8Nosd79L33r5Q38enfL8KCs6AYY18qvPIRE28IYFLzkzCvV5TJfTnG mQIDAQAB -----END PUBLIC KEY-----"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
{
"status": 200,
"encrypted_data_rsa": "DuGcSUU9PuA8GVw0rgy/atvy9kWoQ4AD1q8jm1TrI4t61/IfBomajbfvAv93bOKKGLmUa8a6eJekxVySo6wwLsfy5CaAG1muA5AN9zOae72izTGDpvPC8c/iYAoC5V6wwwWuhH/CrCy2bDN5aKSI8lh9zgoAiKvEzKdMTCoMLOs3RzwOhzqT/yF7OsLM9cW3baFYgxrHtsOyAbEkG2DA0SR3XxDZtJIeLDXyZntqf7UQ7GJ6DGam4bnTe4UuUjNaApESWs/XlQFA1k7C7N9jooSNrvXcwIoMUdWNTJ3DY6KtxSCpwEaZrGuJrCnVZ5qEegCECAXilTccpf6ko+z7BA=="
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
  "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCRIyzC7qzY3YCu zjLpbID06pY9GvH/n7oIUprRwVqTjbGNYJDkkEjwJJqXyxCJ5sI0wLGkbAtx0Ue/ m58k63Yd7ePOBTyHDWQ+PPD442vLPzx+VWpVfBO/ZjN33cgS8OXisAgAMNquyjQx wDrC8DMp+NByhhyXWIcbFwVhSBTMM5k1K3Dy89YntyiAllG5BOiU3VfwExzNYm9c R5osEJMcS31AFMQYOwmo0FgtmRIQEDejNL7TaMTp+DsOkxTYqFtU7gy1OWZe+Mzf X73kyTf1cNIRIs/SXw2ix3v0vfevlDfx6d8vwoKzoBhjXyq88hETbwhgUvOTMK9X lMl9OcaZAgMBAAECggEADQob+2d2IAXGie38pPwameZ5mQPSuiSfkh/ZyP6WJKuW SB1k5yQPaYPgX8LeuYUB7btiOmN6o78psw1IPwjok8fLr7bIuVl6qBzRiYrlJF2K Ec+avhNnssp71UkXsJv0C2nFTj8VZp7EEbQzk1ABSMQR9jgWWYKaoNRwp0zSkYXt SDbWLIAMJQgsH42itg/9+MgGUtHReZMjzEHYqU1Re8I+O0Ayy51HW44zgjxck10g CsAQnCF7UWyagxvTtoQSoBHqVhRK7L40yUxvDB+Bv+Tq4XOSw+WaeBJLOqFngcsz NzzQThp4muauQv3HPr757hXuq+wHQhG/FpV6jQEAAQKBgQD96sF77LMwKwfOT1vH ER9aBNHv+xY/ULZM9HdMYtl7Mym91KDzxW/1zDKGzoUDZlNm2UnldIs0UlWozjOE 23AWGh/IO4PNbpS4Rz5rmCXh83EJYAmFa50iMQC611zsvra4Nc5u3EiDAf3I20wE YMfLew53yWvluGdEp7WWWtjrWQKBgQCSU/lU4RzLVNhYdxC0O/P9fE46RKI+Ygl3 TSItTSEPKw6H4GPmEhgqbyhLF26LMlv4y03VXLAGB/x8suFaUnJOyemkILm6SQmU RJlOcvY2CKpyJ21H/VmklslkugwUinyV48IRPiNyPi/TSPFQQBGL+9yIKThOogwm JqE8w/aNQQKBgQDs7YBdAiCxcXV3LNWWioOWm6jJJKE9szJn3DT1Mcd9DeCFIUKO NEykLkV3RH0ZDwIDlf09/eFmkO0c9ktcTOXpubauP9pcdjKPQOsdunqeu2leNh6s QB3/KXpk3U/4GHympo5ZI3MFy3XjVb042JWVaN23KFtlnwu9JEBsa5i9AQKBgFgi Le2avM4XJ0t5Q11bMuT9ZtyflB0AzXTGx4wDhaLuKw1Z8LGVOmrskpdP4KwEQ/MA +LtG3Vp0mvW8hBDz0Zd0872AXH1AGn3sJ25hvbvj0k15Q8/1X3XLwDdj+3yvwMRC 7xOVmqHnpMScjYPpYuguZbC5KwnpfmnIIJtJ6IlBAoGAEGuy6McpovKopghtqJ3B jtEGhVysu1UTqSOe4NcVvLUbT7SsIN+8xygWKAYAGuCE7AN6N6LDBa72KuzS0U+S iiO/j+t62FY8lY1vvI4YKXmwr7ONhPVjhRgIHjAx9IJ8P8hWAxC9i+n1oiK9ECWL 81kiQg+BuclnyJQ8MOHuu+8= -----END PRIVATE KEY-----",
  "encrypted_data_rsa": "DuGcSUU9PuA8GVw0rgy/atvy9kWoQ4AD1q8jm1TrI4t61/IfBomajbfvAv93bOKKGLmUa8a6eJekxVySo6wwLsfy5CaAG1muA5AN9zOae72izTGDpvPC8c/iYAoC5V6wwwWuhH/CrCy2bDN5aKSI8lh9zgoAiKvEzKdMTCoMLOs3RzwOhzqT/yF7OsLM9cW3baFYgxrHtsOyAbEkG2DA0SR3XxDZtJIeLDXyZntqf7UQ7GJ6DGam4bnTe4UuUjNaApESWs/XlQFA1k7C7N9jooSNrvXcwIoMUdWNTJ3DY6KtxSCpwEaZrGuJrCnVZ5qEegCECAXilTccpf6ko+z7BA=="
}
```
The output is the decrypted data, which in this case is the hash.
```
{
"status": 200,
"decrypted_data": "d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8"
}
```

### Step 9 - Signing of the hash by the requester
Samairah signs the hash using her 'primechain private key'. For this she uses `post /api/v1/create_signature` and passes the following parameters:
1. The data to be signed (hash in this case)   
2. Samairah's private key
```
{
  "data": "d7634a35369c47bf26055744032f85e0e6f1d3645f29c97674770cde95b6631db9a76fa2e93a018fec94e65ba11c752b8ca04403a3cf1b24c69412fc878e30c8",
  "primechain_private_key": "V9uvYCkvGFGcrq2ePqtgnxA4qHAdFThhAUEkCT2sMogXv2pmAZq7nu3A"
}
```
The output is the digital signature.
```
{
  "status": 200,
  "signature": "H3i7JTbIfwe/jf05z3ea+O/Ljl0DHLg7MzTc4RE6FRd7M79SLGgq1zzuPkzffXHjecbcAMLtjHqoxUVRskSHfmQ="
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
