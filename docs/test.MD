# Blockchain based authentication

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
"primechain_address": "1HvGxDqC6u9rmL8y5KUCrK6VeDu1FCbotcqoZJ",
"primechain_private_key": "V7qoHKPfQc94zJXmrUmqPiFin5BrDbc9A1GASqVi7phHs5qgtoic6NHT",
"primechain_public_key": "0295e71fb842152960130859ff74d92487e8e8da37e78e6ba8af38afe2c08a68cf",
"tx_id": "911b8f91ba10c389db12718310e6a9d6d70eb4756e5a1877e091774fb00eff9d",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAgz1B0KRqUx7GGFh429EJ RE1TzapV0/SWnX5Z6q2ZXtzUa/kken0Zhceq2OBdWQspuNQT7EOsxp7xZrxSjxmy gc4+OBlVknqTJ49hLPPo5bZ7SBLHBadrv9XMIIgQXsEntpYWzydEOrct63FdBygG Kf/GBGH06tcpcH5SbrrI7EpCwuRu7qCjIYmRhA3eu5xo9Wi5TOfV2QAOq9ia0cU3 +jQ8PRL/MNIT+5dm7B4lwo4WY6isTa6fd2UX94Wi6uOSsEEj0F7XIJ41L4owlpHv WEulkEJWLzzmsDAemoQ+H/HzXmfHnZKLVexDGxbDX2MGzy9txaWElEOSJD6DXVhG zQIDAQAB -----END PUBLIC KEY-----",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCDPUHQpGpTHsYY WHjb0QlETVPNqlXT9JadflnqrZle3NRr+SR6fRmFx6rY4F1ZCym41BPsQ6zGnvFm vFKPGbKBzj44GVWSepMnj2Es8+jltntIEscFp2u/1cwgiBBewSe2lhbPJ0Q6ty3r cV0HKAYp/8YEYfTq1ylwflJuusjsSkLC5G7uoKMhiZGEDd67nGj1aLlM59XZAA6r 2JrRxTf6NDw9Ev8w0hP7l2bsHiXCjhZjqKxNrp93ZRf3haLq45KwQSPQXtcgnjUv ijCWke9YS6WQQlYvPOawMB6ahD4f8fNeZ8edkotV7EMbFsNfYwbPL23FpYSUQ5Ik PoNdWEbNAgMBAAECggEAKt86/c6IEUkvS0qziJN75H0iUEBBs3DmNuLMutYlEREw r2j/Gqh9Su+UBy8cL3dvFLrrGzZsXaIUmAwTKD4ryy21s5vLEYPLSJQVGZtATLJV CZFgxJ8RmuRbv5DTUDDnKUVUhC1+o3Oto4kv66OOh+/PHyVk3caV+fK6OQP5mP6d IP/XU3sU2ynyBo2UKwf3jXgUdojfx/eSrj4Pu1BozAbmaRECr8+lc4pMLIYpB47G yRWJO9LjcNG2fhj495/+3MrwypOXhZyUSHoI6KiVNRz4WCgXJQ5efXUDXrov8mM7 05y5a+8w/RQi2EOj8QSl6YujEgxiGWnDT5I02R+goQKBgQDIPibMaWEg/QN+VeOU HaQeIItS3NaSrAHLw4qcsuvEB+87nTT+TxL5bxQIGEAh41ZmfFnHZIkXBI/5lQpa RV61JlzS+owFfUXB8JEfqpzrPEgUnDx12xTG76YqwnMbgOKP8wIea1WL97U25avr jLFL3vMx5+nnX72PPWsRmSzlBQKBgQCnyFltJmI3m6voDijS8z/yeL97qsZwo/Fs UZsz/zU8762pd01R0BrmIvRff9ZX/Cg+6v/NipKVQjYLDTHKqo24WmL/2i72gDmQ oxcKBp3b2hPiAx7EtHgN0Vtwh2T2OlbVFxbreCKPavjnr3ZwgGg0L6C64ibZFEmX yyZgkTyFKQKBgQCMLSYP9r0t0LD/YbTc3Rskk/e0XDBBoPPo5sxEAeSV6FAK1XRh io1n2+CUAhXzIyg6ulZHBRQK7wCy4SjMJL+15FMaxpX6ycVpjLSrDE6pRhvXgb+5 aVJUKTOTv2fBGyp/Rsh27wCF6TQMaB8/18/NoxdwGj9d32HdwksPmMEa2QKBgG25 ZVovTu4E3TBeCi6iq8A7XSZX8Xx6iokG+VPQ45UdPVnlTmhhiyXT2DKYHKnfmsZC 0tUteV0pNsSVdWmPjizw12tw2WOVSZAgSBHjb9r2TChzV+zWBOksb/swYENytZSX jAKjxx45m9uQcQlzwDHYr+lnunYegV5Gmatvb7+5AoGBAKzmJSonyC3KJQRUQcPc ay3MaPaUE7BtGWkYVEILjAGsGeruBB7uYSMhJqxM6Mws1QpGf4WPVBSYgtM3Z3d4 nhUpNETaxlHUZF3X9CLXCqQO/U4MBP94K/URbyff9nFoPLCeFNONRXELxaDrvcjK ZNfg3vvsd0USatehpj7dAOP6 -----END PRIVATE KEY-----"
}
}
```
The following are automatically published to the AUTH_USERS_MASTERLIST datastream:
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

In this guide, we presume that Noodle Bank is the verifier and Samairah Nagpal is the requester. Their primechain addresses are: `12pdAHR1Jurv7oSULBxDE7QPBUfDKtAg5t4u3v` (Noodle Bank) and `1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn` (Samairah).

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
    "string": "kaPYzPoOBv3wcDjLPpj23jl7JJLrgUBFNyYFt2NvPazaBlKBbg3SqgvFZtVzNmJtnUgLcQrglERswfuYwPwisywP54nMuo5HzXw0D2Kztqzy44K0zJs0upZlQjwEnWhGpKwtHFKqVrIUwCpPY83ZolRsurHSk76kWoNukxIntiXmkeDzWe0YYtsUBcIG41BieiIGO9n5DmXFow1L6l91hQL1T6fdafALJX9sZIDNPVlyalb7dOJyHxBH0lkykxt19VbTb4dZCWn68YkzYxhpp0AFtbF6bMBinZCbkbmsZPAhQx44k5fEksv6UDz8bj9H8thTxUXXVZTB3msdbHgZrOhfzAFHyTEA7IBVSrz8CdsU1XeEFHnYZZ6ogxQ0ZfacO6v9SdXzG8McK0mTr4BHeWQXmVMXmzKnCMZrH8KnXvBGyCsBhOnjvP7yVoEtf2xIqwPQ9jcvIf3NNZVqtAxL0utoZ3KB1DQ9NgZpTPCsSr8mffEzH2264urIOzGIs0j9",
    "timestamp": 1544011513,
    "hash": "NokbI+G2Pk4/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q=="
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
  "data": "NokbI+G2Pk4/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q==",
  "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSMswu6s2N2Ars4y6WyA 9OqWPRrx/5+6CFKa0cFak42xjWCQ5JBI8CSal8sQiebCNMCxpGwLcdFHv5ufJOt2 He3jzgU8hw1kPjzw+ONryz88flVqVXwTv2Yzd93IEvDl4rAIADDarso0McA6wvAz KfjQcoYcl1iHGxcFYUgUzDOZNStw8vPWJ7cogJZRuQTolN1X8BMczWJvXEeaLBCT HEt9QBTEGDsJqNBYLZkSEBA3ozS+02jE6fg7DpMU2KhbVO4MtTlmXvjM31+95Mk3 9XDSESLP0l8Nosd79L33r5Q38enfL8KCs6AYY18qvPIRE28IYFLzkzCvV5TJfTnG mQIDAQAB -----END PUBLIC KEY-----"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
{
"status": 200,
"encrypted_data_rsa": "K+stxqVtxVfsZnLCanbOiQLw0D5WcJ3BEx/uif7go9FLtUfqXp30yTani4UemS6x6WqVS+E7GaK04uO0NBiIkAkQNlv7TidL3fnMuYRHfXivZ8zjrGyP2YCMw82kRWUi91DbEbgGeHp4Dt90KXCy6THUMyolPKp2QpWV0HDmeaIt/RitmWeKBYc1Uko1cYfGZOuukn6576hz9XEoBl6qMCHdPtenT+3kgBPjvH71/GaRH/8VWadY1z2jIUkhhfuAymU/C593CJAnw2kpgUjKpyXpEFqGQmJgrAyfSiQx57sdagXYTcDPuXova8HSYRZwK6n6siVDok6fr4pR5tYvhA=="
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
  "encrypted_data_rsa": "K+stxqVtxVfsZnLCanbOiQLw0D5WcJ3BEx/uif7go9FLtUfqXp30yTani4UemS6x6WqVS+E7GaK04uO0NBiIkAkQNlv7TidL3fnMuYRHfXivZ8zjrGyP2YCMw82kRWUi91DbEbgGeHp4Dt90KXCy6THUMyolPKp2QpWV0HDmeaIt/RitmWeKBYc1Uko1cYfGZOuukn6576hz9XEoBl6qMCHdPtenT+3kgBPjvH71/GaRH/8VWadY1z2jIUkhhfuAymU/C593CJAnw2kpgUjKpyXpEFqGQmJgrAyfSiQx57sdagXYTcDPuXova8HSYRZwK6n6siVDok6fr4pR5tYvhA=="
}
```
The output is the decrypted data, which in this case is the hash.
```
{
"status": 200,
"decrypted_data": "NokbI+G2Pk4/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q=="
}
```

### Step 9 - Signing of the hash by the requester
Samairah signs the decrypted data using her 'primechain private key'. For this she uses `post /api/v1/create_signature` and passes the following parameters:
1. The data to be signed   
2. Samairah's private key
```
{
  "data": "/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q==",
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
           "data":"NokbI+G2Pk4/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q=="
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
      "data":"NokbI+G2Pk4/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q=="
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
   "data":"NokbI+G2Pk4/c2jZl2i8Y/QJgbGVZ0A8/yTEAEAowNv5oUc3NJ/I7zETqhNgcxsWgfldJEx8NRP+T6fTqwFM3Q=="
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
