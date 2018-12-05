# Blockchain based authentication

[1. Onboarding a user](#1-onboarding-a-user)   
[2. Authentication](#2-authentication)   

## 1. Onboarding a user
A user can be an individual, a company, a device etc and can be on-boarded using using `post /api/v1/onboard_user` and passing the following parameters:
1. The user identifier e.g. name, account number, IMIE number, serial number, CIN etc.
2. The user description
```
{
  "user_identifier": "23792387",
  "user_description": "Heat sensor installed at Zimblia Avenue"
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

## 2. Authentication
Authentication is a 13-step process. The user being authenticated is referred to as 'entity' and the user carrying out the authentication is referred to as the 'verifier'.

In this guide, we presume that Noodle Bank is the verifier and Samairah Nagpal is the entity. Their primechain addresses are: `12pdAHR1Jurv7oSULBxDE7QPBUfDKtAg5t4u3v` (Noodle Bank) and `1JfukBtEC2nvGGexKYkfhetuiDJ1FP74w461Gn` (Samairah).

### Step 1

Sanya retrieves Noodle's 'RSA public key' using `post /api/v1/get_rsa_key` and passing Noodle's 'primechain address' as a parameter.
```
{
  "primechain_ address": "12pdAHR1Jurv7oSULBxDE7QPBUfDKtAg5t4u3v"
}
```
The output is the 'RSA public key' of the verifier.


### Step 2
The entity encrypts its own 'primechain address' with the 'RSA public key' of the verifier. This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is the 'primechain address' of the entity   
2. `rsa_public_key` of the verifier   
```
{
  "data": "xxxx",
  "rsa_public_key": "aaaa"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
output
```

### Step 3
The entity sends the `encrypted_data_rsa` to the verifier. 

### Step 4
The verifier uses `post /api/v1/decrypt_data_rsa` to decrypt the `encrypted_data_rsa`. The parameters are:
1. The verifier's RSA private key
2. The `encrypted_data_rsa`
```
input
```
The output is the decrypted data referred to as `decrypted_data`
```
output
```

### Step 5
The verifier retrieves the 'RSA public key' of the entity using `post /api/v1/get_rsa_key` and passing the 'primechain address' of the entity as a parameter.
```
{
  "primechain_ address": "aaa"
}
```
The output is the 'RSA public key' of the entity.
```
aaaa
```

### Step 6
The verifier generates a 512-character random string and the GMT timestamp. For this it uses `get /api/v1/create_string_timestamp` and gets an output like:
```
string^timestamp
```
The 512-character random string along with the GMT timestamp are stored in the verifier's private database.

### Step 7
The verifier encrypts the 512-character random string along with the GMT timestamp with the entity's RSA public key. This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is the `primechain address` of the entity   
2. `rsa_public_key` of the verifier   
```
{
  "data": "xxxx",
  "rsa_public_key": "aaaa"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
output
```

### Step 8
The verifier sends the encrypted value to the entity.

### Step 9
The entity decrypts the encrypted value using its own RSA private key. The entity uses `post /api/v1/decrypt_data_rsa` to decrypt the `encrypted_data_rsa`. The parameters are:
1. The entity's RSA private key
2. The `encrypted_data_rsa`
```
input
```
The output is the decrypted data referred to as `decrypted_data`
```
output
```

### Step 10
The entity signs the decrypted data using its primechain private key. For this it uses `post /api/v1/sign_data` and passes the following parameters:
1. The data to be signed   
2. The private key of the entity (signer)   
```
input
```
The output is the digital signature.
```
output
```

### Step 11
The entity encrypts the following with the RSA public key of the verifier:
1. the digital signature 
2. the primechain address of the entity (signer)
3. the data that has been signed

This is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is the `primechain address` of the entity   
2. `rsa_public_key` of the verifier   
```
{
  "data": "xxxx",
  "rsa_public_key": "aaaa"
}
```
The output is the encrypted value referred to as `encrypted_data_rsa`:
```
output
```

### Step 12
The entity sends this encrypted data to the verifier.

### Step 13
The verifier verifies the digital signature using `post /api/v1/verify_signed_data` and passes the following parameters:
1. The data to be verified   
2. The primechain public key of the entity (signer)   
```
input
```
The output is:
```
output
```

The verifier also uses the stored timestamp to confirm that the signature is returned within a pre-set interval e.g. 30 seconds.

If the signature is valid, the entity is verified.
