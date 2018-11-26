# Authentication

[1. Onboarding an entity](#1-onboarding-an-entity)
[2. Authentication](#2-authentication)

Code-named Primechain-AUTH, this system uses the native capabilities of the multichain blockchain along with RSA based asymmetric encryption to achieve a secure password-less authentication system. This can be used to authenticate an entity (an individual, a company, a device) to an app, a website, an email account, a blockchain etc.

## 1. Onboarding an entity
An entity is onboarded by a bank (known as the onboarding bank) after due diligence (KYC process). The entity is provided with an application that is capable of running a multichain cold node. As part of the onboarding process, the onboarding bank provides the entity the Primechain-MONEY blockchain's parameters file.

The entity uses `get /api/v1/onboard_user` to generate the following:
1. a primechain address
2. a primechain private key
3. a primechain public key
4. an RSA private key
5. an RSA public key

The entity's primechain address, primechain public key, RSA public key is published to the ENTITY_MASTERLIST datastream of Primechain-MONEY. The entity's primechain private key and RSA private key is known only to the entity.

## 2. Authentication
Authentication is a 10-step process:
1. The entity sends its primechain address to the verifier.
2. The verifier retrieves the entity's RSA public key from the ENTITY_MASTERLIST datastream of Primechain-MONEY.
3. The verifier generates a 32 character random string.
4. The random string along with the current timestamp is stored in the verifier's private database.
5. The verifier encrypts the string with the entity's RSA public key.
6. The verifier sends the encrypted string to the entity.
7. The entity decrypts the string using its RSA private key.
8. The entity signs the decrypted string using its primechain private key.
9. The entity sends the digital signature along with its primechain address to the verifier.
10. The verifier verifies the digital signature using the entity's primechain address and the random string. The verifier also uses the stored timestamp to confirm that the signature is returned within a pre-set interval e.g. 30 seconds.

If the signature is valid, the entity is verified and the session can be started.
