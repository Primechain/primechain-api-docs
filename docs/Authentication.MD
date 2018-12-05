# Blockchain based authentication

[1. Onboarding an entity](#1-onboarding-an-entity)   
[2. Authentication](#2-authentication)   

These end-points can be used to authenticate an entity (an individual, a company, a device) to an app, a website, an email account, a blockchain etc.

## 1. Onboarding an entity / verifier
An entity / verifier is onboarded by a bank (known as the onboarding bank) after due diligence (KYC process). The entity uses `get /api/v1/onboard_user` to generate the following:
1. a primechain address
2. a primechain private key
3. a primechain public key
4. transaction id
5. an RSA public key
6. an RSA private key

```
{
"status": 200,
"response": {
"primechain_address": "18WFbKrENxf7u1xwUXYrKzbZuU2Hh4d4GA4pM9",
"primechain_private_key": "VCaewXd7tWw1FyowD2SV5zTVTRCA1USVai3gWPp5zy4JJtmxhKVYw4UT",
"primechain_public_key": "0253b060c93ba01879bc1cceefe7cfe8aa7bd5c1a611064ac100e92ef5227efd8d",
"tx_id": "45fcc868c8d52d3f2cb2a0b2b389997cb625ae6d66594206956e045f15b9f721",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEApXnD9fvGxJSJ+Y7CnVE6 SqildolOyVtNK1f6SO9O/ksVzKahi9ZYIrMqZiF5UoUP8z2GlxnIEpdwhKoxH7KX Y1d6l4fE/0W3QH9eGCcmxvWncZiQJIwmWB4NqeKO1AIBE9hxk8ZhHEI68AMv1ptG L6J2HlFQ3z4us76pTbhsVZmAyQ+yc6g6sU4gGj7GDVyS1ZpIw+2O8ybNYfN8ieSU qZ56tA/OeSxaWKMl/JaDHuZ3kWzEfXfed+7WmFxXqHUpkf58W8pYsiLDlgfBlKWD Rxzflc/LGKjwS3d1ydHKvPRDJ0hqNf6DHO4AyoOfI3fnqdFc1psN/F+fnfYsm8z+ VwIDAQAB -----END PUBLIC KEY-----",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQClecP1+8bElIn5 jsKdUTpKqKV2iU7JW00rV/pI707+SxXMpqGL1lgisypmIXlShQ/zPYaXGcgSl3CE qjEfspdjV3qXh8T/RbdAf14YJybG9adxmJAkjCZYHg2p4o7UAgET2HGTxmEcQjrw Ay/Wm0YvonYeUVDfPi6zvqlNuGxVmYDJD7JzqDqxTiAaPsYNXJLVmkjD7Y7zJs1h 83yJ5JSpnnq0D855LFpYoyX8loMe5neRbMR9d9537taYXFeodSmR/nxbyliyIsOW B8GUpYNHHN+Vz8sYqPBLd3XJ0cq89EMnSGo1/oMc7gDKg58jd+ep0VzWmw38X5+d 9iybzP5XAgMBAAECggEBAJF7Fk/jRYN63Dstyegpi8grsR0f5sacoKHkvUT2MErd lJLSROD+V4paXoJgF5v3JGjDxNp/bij6P5BDWOD3UKWkOUGTuhx8HHp2ADHX6f2t 58K1ULTxCp0Z/wVHDC9Ue8II3wH+vU3s5IgzJRHWfcRPXu2UrDc5IjIhBBQyefxe iBIFsijtItFEH1JrlembFRnLq4eiVfwWZ7Arg2QD+GlEM0jDfxOP/h2fW3PguBgE 54qq5iZz8OZvMVzStgZ402WGo3FHmDhnxa5bkla8Jg/5n6qCrDW0IulqAZV1vYXX F4sLqPR3OMhlL5nmp9Ng5kBo9VxWPTccxEH5rXLqELECgYEA2mlfHk+7Z1bt6qhE wbuukbnbC6goZ3eigKXQZuut8/R/Xj766ZB16UtXA/kLqUtUKHtxXghEHxWSF+E7 2466/KTAF9M2PGbXW4vkO+gXfZGDPMwZInSn5sXBFukj0nuVmp+M1A0D+b8ELFTr QRy2yJ1V0odMsIq8Bz40yhX0m+0CgYEAwfQtf7MTGWaE2jxakmcXP5ChqzFWWuC8 nK5Cr3cilnKLR4Ph5cHktEJip4WtwXLVNuQRGLLGCuNKXErt5HHh8QGQ7DBzS9yJ wEBfv8dqUsBc1G8eO2kvclYEPDTXytTXR/kdPG10Sd5PGJfeJrFCBBdjrFZ85Qo7 P5bwPm8HItMCgYBxVHfMrKabSpoNRt7Wf+JnLz8f31OHzKX/hwqKPQR4L4ffiWJ8 yz7DnRo7r4CDidjTYKpElplyX6j8xxxeIsOX0Iz0T942nU5l7EKzawy1VUn5xBXO sSVmM3qrvrGdyA6quttCNLa5YopxzmZ71MBrfGhJ43bBrFtAjuCpc5cHSQKBgQCq iqQ/NxzCJu0GYC9bsB43HFurhhRikF4IfwnP87eMBmgFmCdXuWf6QK0ylE62XNyy CVQnHXsaM8U85f3L838yRahCpk+bEu5lB7WpkhUhclety48Pumun446Ryf09Mm2h saBNdAjeswVloJQL/a0In/Bapynm01pJjdTtcP8bVQKBgDKVN4eQtpCz6uEBX3QP KdioYh4AA6p4UqOvc+RNjCJ/d29oCMCnzwedvOJAl3YCNRnsSVtzAyc0XMeJpeXM Gwq4IVV3b+lptAtVtMKeUf4IM/EHKiEYh7bL+QoqpVE0XyKvWmn0SRRv5Vlu/9hY F2Pi1CSo3cDET/VVtnWWATva -----END PRIVATE KEY-----"
}
}
```

The following are published to the RSA_MASTERLIST datastream:
1. entity's primechain address,    
2. entity's primechain public key,    
3. entity's RSA public key    

The entity's primechain private key and RSA private key are known only to the entity.

## 2. Authentication
Authentication is a 10-step process:

### Step 1
The entity encrypts its primechain address with the RSA public key of the verifier and then sends this encrypted value to the verifier. The entity uses `post /api/v1/encrypt_data_rsa` and provides the following:

* the data to be encrypted (in this case, its primechain address)
* the RSA public key of the verifier

```
{
  "data": "18WFbKrENxf7u1xwUXYrKzbZuU2Hh4d4GA4pM9"
  "rsa_public_key": "aaaa",
}
```
The output is the encrypted value:

```
output
```

### Step 2
The verifier uses its RSA private key to decrypt the encrypted string received by it. For this it uses `post /api/v1/decrypt_data_rsa` and passes its own RSA private key and the encrypted data:
```
input
```

The output is the decrypted string (in this case the address of the entity to be verified).

```
output
```

### Step 3

The verifier then retreives the entity's RSA public key from the ENTITY_MASTERLIST datastream. For this it uses `hhh` and passes the following input:

The output is the RSA public key of the entity.
```
aaaa
```


### Step 4
The verifier generates a 512-character random string and the GMT timestamp. For this it uses `get /api/v1/create_string_timestamp` and gets an output like:
```
string^timestamp
```

The string along with the GMT timestamp are stored in the verifier's private database.

### Step 5
The verifier encrypts the string and the GMT timestamp with the entity's RSA public key.


### Step 6
The verifier sends the encrypted value to the entity.

### Step 7
The entity decrypts the encrypted value using its own RSA private key.

### Step 8
The entity signs the decrypted string using its primechain private key.

### Step 9
The entity encrypts the following with the RSA public key of the verifier:
* the digital signature 
* its primechain address

and sends this to the verifier.

### Step 10
The verifier verifies the digital signature using the entity's primechain address and the random string. The verifier also uses the stored timestamp to confirm that the signature is returned within a pre-set interval e.g. 30 seconds.

If the signature is valid, the entity is verified and the session can be started.
