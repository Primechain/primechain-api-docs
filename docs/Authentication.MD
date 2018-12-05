# Blockchain based authentication

[1. Onboarding a user](#1-onboarding-a-user)   
[2. Authentication](#2-authentication)   

## 1. Onboarding a user
A user can be an individual, a company, a device etc and can be on-boarded using using `post /api/v1/onboard_user` and passing the following parameters:
1. The user identifier e.g. name, account number, IMIE number, serial number, CIN etc.
2. The user description
```
{
  "user_identifier": "1234567890",
  "user_description": "Primechain Technologies Private Limited"
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
  "response": 
    {
      "primechain_address": "1HpE8ZwqDyckgmnEnsHBkigsGDhvoYqQXXGBYj",
      "primechain_private_key": "V7vznRFfAMCGbzayvAcHsePBJEaoswLmtGXGCgLiNNDe86uJ1AZaqsci",
      "primechain_public_key": "022b031af75d871f44e0cad222c0beb6b2753e3a28697b62917b1dfa4bbde14519",
      "tx_id": "64645e8b59df078be0cdb2d5986e468d31bc4d1089feb164b5278106ce6ce0f3",
      "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAgpX9L2fIk8syLtsF7BQG gB1vIeZgK8brEwU8GDyJlhPa1Axf0B+sjh7wgqGMpCZd9LpFwxJQEkrWiR63Nn3o OVXJ1/b3Gw91Jy5B6zJMOTM/ojCtEfA5X9KP3U5ETR5s1fHFrql5zOnj00hiUX3u bb143kVbneclu+kIGXvHB1Du5NF+rkeN2FPXHwUxbxWSF+Imp6yVQ3OjH9uXVZH3 VAWt/7dcn+Pb1FreK4wIIFX/CeqQ3+KC5XPc8f4HbO1MuaU2TkczbQxZHU7LdzIf ag422lQlivu/4EV1rcyz9j5c9DjrN38tH+WfQRb2CstEf3tCrd93ZAiCGkK/x5qd HwIDAQAB -----END PUBLIC KEY-----",
      "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCClf0vZ8iTyzIu 2wXsFAaAHW8h5mArxusTBTwYPImWE9rUDF/QH6yOHvCCoYykJl30ukXDElASStaJ Hrc2feg5VcnX9vcbD3UnLkHrMkw5Mz+iMK0R8Dlf0o/dTkRNHmzV8cWuqXnM6ePT SGJRfe5tvXjeRVud5yW76QgZe8cHUO7k0X6uR43YU9cfBTFvFZIX4ianrJVDc6Mf 25dVkfdUBa3/t1yf49vUWt4rjAggVf8J6pDf4oLlc9zx/gds7Uy5pTZORzNtDFkd Tst3Mh9qDjbaVCWK+7/gRXWtzLP2Plz0OOs3fy0f5Z9BFvYKy0R/e0Kt33dkCIIa Qr/Hmp0fAgMBAAECggEAJc6C9NyZR6DGsKYcutK5ZxIegLQQF9yJZoJXebTdKKQq 8MV8X+crsCHpBAj9jPDGtvnPBMEiiYk9P4mzBYXCXAcoXuxTcnQxONy9nPh89PqP a8en88+W7NUrbakhQSqT3AUZdI4Ag4EbwqnsPSe2hfMbMU7nTXoEhLjc7XPWlZk7 jbQZwivjhm5y8Kol1YKBCKBbSQqDgu1tqb1J+X7md5OMZyMaIzgNZmf+Y2YB//pS 1khYDd8w7GOyGs45p7CehPWBNqDW0IwvzZiRNCgDNkJLgvA5+NPiFIEWaEGBZwYm vi6ZTe51xoqDa8rbH7wSbIjwvnd1q9VqufaSwXG9EQKBgQD8JzoTdp+vDso386BT GZF+NmvgMs0Dtoc8FdC3CLXarU46V6rwHbMpC57u2L4cSWUpemiUxTKMjppKm/bO 0YugCiShH08QexoTcQdzaIPduEqdqCneEhUHpR1gyGgowKVr0FrHGit/CUHt5JK+ l2u+NA+nIV8DUytIBMK6XTTo+wKBgQCEk/yCXcMnzWx10IXxy1oOR5sVPsysDn1F 8NOJBb6Qitd0l3W58vtlYxDDRCxtqUdqc6Te9VMEgvzjLJpVUcPCd7LMVmtrwcr6 cZU1uTtkm8Bj8HZBMpvvFb2W3H02SFuHYlhjCOcnNRnNt78jT/sIboItHDC9azFi IxUnVaqrLQKBgQDftW2xFu1VQqnmOh9jmquabm4G2wtI4AfbJv+lY/Tzrg5ZdK4T mkX5hHXdMi54qiU2R4PBebL/QQVibDzsALz/oAAfcseSt6TK2tzhZziW3YpVlXyP qTs/LR6DX0oJ3eDlZlUjj/RHIM99X+1RasYMWeQJQ3IoYQFlQ9P/w/HNQQKBgFrD gZSyoj+mmEFUH884e4/ZH+f8lVyZktQGGpvtLdiA5R4x7uv92HRBzSERlCUDRhwv zcjCRTKKhpz0VThiANYq4mKYK3SbON4aUp90D6BCLQV+g0cBYdXdmW0lyCcYhGj8 QCyU1MN3zBGVYSrIv8C2/zHo4clcEHPyNrI2KOCFAoGAdw6mncyn26cqiSjssaG3 4Fqwl/aCuFWj7ruXOENMb2n1icg1Athk2jz44W3XTPj1MLPUZqPVyUlJDBddmhvl nwG3qQU/w0+BlvIFtW/7j5tMJ21bDZ7S5g6Bix7soeZNuRZK0z2ihOsSclXmtdmH vb05+Q8ZdbPR2iEhz2qs2UQ= -----END PRIVATE KEY-----"
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

### Step 1

The entity retrieves the 'RSA public key' of the verifier using `post /api/v1/get_rsa_key` and passing the 'primechain address' of the verifier as a parameter.
```
{
  "primechain_ address": "aaa"
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
