# Password-less authentication

[1. Onboarding an entity](#1-onboarding-an-entity)   
[2. Authentication](#2-authentication)   

Code-named Primechain-AUTH, this system uses the native capabilities of the multichain blockchain along with RSA based asymmetric encryption to achieve a secure password-less authentication system. This can be used to authenticate an entity (an individual, a company, a device) to an app, a website, an email account, a blockchain etc.

## 1. Onboarding an entity
An entity is onboarded by a bank (known as the onboarding bank) after due diligence (KYC process). The entity is provided with an application that is capable of running a multichain cold node. As part of the onboarding process, the onboarding bank provides the entity the Primechain-MONEY blockchain's parameters file.

The entity uses `get /api/v1/onboard_user` to generate the following:
1. a primechain address
2. a primechain private key
3. a primechain public key
4. transaction id
5. an RSA public key
6. an RSA private key

```
{
"status": 200,
"response": 
  {
    "primechain_address": "1LSkxfMXyBZ6dkS5boJ4HqVUtg8HT23Th7BAD7",
    "primechain_private_key": "VAYsZsWm9bNZGUZxctwTfhRwxSbdtq7kpeGPweA3DwvNd8VWVEf5UhaK",
    "primechain_public_key": "039d308affe4a60dcaf4ba2e392d5ad2af6314a7921dfca12bfa83e1472f97cf4f",
    "tx_id": "1e44d8cdbeab525c0d8f72ce982074acecc4a9d57fbb1ad121b2554eca506bfc",
    "rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvr4r+1xpdqZYWUAvsMQ6 KHiLnSZjsO76BwZ//RWZtW2AMAcXZPttps6sbuiyANzslhpLQffrpYoLeQXdMmkB HyeJxwdYpfjjt/ab7ke0oMaSTOt+kuAeNLQZBXpN4BiZs96To3b9AcQzYHb5Y9Ty 6eQLHi27glaLmpZL+mQs9mR3SJTEoXoZZ7CGT54v6DB5sO3BrXrE0t8SP1TfD91C INrrlfrs8GGw+58wK6yQ88LQqHgXmbWoqF3lyg1oGgan1Sj0jBYp6RyMJ3HQvbml 5NwG1gpzDPjAF9NsZnowPF/vOBjpqI3fTFFiiW2A8txzpwphCyNUSvuJMFy2+GBj vwIDAQAB -----END PUBLIC KEY-----",
    "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQC+viv7XGl2plhZ QC+wxDooeIudJmOw7voHBn/9FZm1bYAwBxdk+22mzqxu6LIA3OyWGktB9+uligt5 Bd0yaQEfJ4nHB1il+OO39pvuR7SgxpJM636S4B40tBkFek3gGJmz3pOjdv0BxDNg dvlj1PLp5AseLbuCVoualkv6ZCz2ZHdIlMShehlnsIZPni/oMHmw7cGtesTS3xI/ VN8P3UIg2uuV+uzwYbD7nzArrJDzwtCoeBeZtaioXeXKDWgaBqfVKPSMFinpHIwn cdC9uaXk3AbWCnMM+MAX02xmejA8X+84GOmojd9MUWKJbYDy3HOnCmELI1RK+4kw XLb4YGO/AgMBAAECggEBAIdlBmNOna4TNfNklHWtVHsV1kSe03TsrZ3/ByrnAky+ hZeR8RFFR/h4C/5OPsxOBcImt/UDvsmqy6oEd5co4hrzPeGBXXOy0DHtY5IoZBcb 3Q2svBQV8lsG3Bv/TPgdfj0naTVHaSCv3KhEy5IJvsQ3k4zAebFzLXV16ki6gxAB 1nyfxHT5po2nBd6l01PU26tWXctVT99PKAogXgA24DYUbo6rvyiEJ6XFHZafyZ2T XbNH8vw3hYmm7S714lP3sbPUrbWuVq8dXikOwBVzPnYhye+WyMMkEHDtJFbj5Nsl e1nsKnvgd6y8BUsqFiZznRpvlO4nXw5TECSot3gkcMECgYEA533JDAQqMPlJTTqy X+yZ48xM80IfX7ctg+PQZOVos9GZtbN9wP0K1s48ylQM586HdcMOkjpbg3luTAiw mLtLzkzq+mEr9dzN5lPR0jO38ni692SCPnPxN/XGgNH3oPR1X7269WsFkFdXn6SZ yV5QY2l1lrrPW7K1106hQFBo5tUCgYEA0u/2Msyaurz0m+Jy/98xEZmDCjHYL4Fl AHX5RbrfF4FfYq8k6lTKU5XIg+Pgdnz9Cv/4vagFp0SdgIqJIpwAEYLskXckbFMp 5xQ5rRJJcEcxCmrK2yFYbaWm1+xWNPLklNoqgnteuutbqOFO+i+L0uG4oR6lKrT2 2y2JeTRtEkMCgYEAvfLo1YNVW3oyO7y+QRfT7qflPHY1aETWhDKa/S+BCowipIXz 2jfIfRodp6fwLwW5AVhczIA2N1uctacrwSduvIlBBtJVUBkumqCMuv7VIZEPWZCP js90T4bMq0ee+eOdrEHy9w4qMpZ4v/ZAeot5Sxlt85C2NXge3d0XU76nVUECgYAg ecVj6NBhs7nNTj36WviJByN/rFDmb3uHaKJqM+0pB0gSP3jlgwxrdgIbHDhwxamH ygUX3giQyiWdpraaV35DM+8MLlWzP9KRuzFuDgS0fqF0QyDcP/QHXZukXsSe/k5n BHfLAweAq7++7oFkT3GtlAcC917ihl4DPK2PtZydVQKBgH4pBHXWtA7ED4S8iC7y 6JOF3nAC6lTwyk0fV2+X1cPi4pff15gA9VJkbj/oCH6NlcsP3W14N8gFRVcw9IEd zx16xBjlZn0u15ICCVxpyunaglXqP/IK/57g4PN1o/6yEGjpbRiyNHEJWfNg4V0N wZ/fl1ZdsNyKm563Wcdq9Tuq -----END PRIVATE KEY-----"
    }
}
```

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
