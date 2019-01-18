# Encryption Engine

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

The Encryption Engine provides symmetric (AES) and asymmetric (RSA) encryption functions – secure key generation, encryption and decryption.

***Table of contents***   
[1. Generating key pairs](#1-generating-key-pairs)   
[2. Symmetric encryption and decryption](#2-symmetric-encryption-and-decryption)   
[3. Asymmetric encryption and decryption](#3-asymmetric-encryption-and-decryption)   


# 1. Generating key pairs

To generate key pairs, use `post /api/v1/onboard_user` and pass the following parameters:
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
"primechain_address": "1PSJu3HNWKUUDrFuczZFF7RpjzW91d3ePM33P2",
"primechain_private_key": "VF9AuAEj9raiz49WPFT5ggUWpqnuLW5fTfUWTcgpES3fnSvMaAtihcb3",
"primechain_public_key": "03cab61a93838185f4a1380de31e085348ae7b3692bf4c00f0aaf83c3436d0c4b3",
"tx_id": "b411225ccc2c35a01d5cee462e51a3ea9ec7c51fc2cca7c47c12aad98e67d22c",
"rsa_public_key": "-----BEGIN PUBLIC KEY----- MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAg1dT58+qisllAGP1baoe SWH++VJY7JGC4ztxJTk1IV5bBYgHGIbZfrGKklVkwy4Yufwafz6FMYfM1Xn9JxKL N8kcQeOQaRHv/x2jgp2wnBE5MHblLctx0W6mHZPwW/cSomp/i7ulOqJqJD5A9Bll inDEV7Yrj8N6tyWD1vpTi8Al7mTVUp+QWPC8hYKZBm9dWH5XKRF5Z9wEHwvk9tQp wnETPMGEY2N/t4wWzaqGIP9SjZUobYgt9djv2GuOvaGzapjLUKwD1ZhR+x7NOKnb zoE5mOYenUfQXDPCQMULZCS19yISon4fjVnepYALAJEyrsFJnO/MGemyXO5x4H4d /QIDAQAB -----END PUBLIC KEY-----",
"rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCDV1Pnz6qKyWUA Y/Vtqh5JYf75UljskYLjO3ElOTUhXlsFiAcYhtl+sYqSVWTDLhi5/Bp/PoUxh8zV ef0nEos3yRxB45BpEe//HaOCnbCcETkwduUty3HRbqYdk/Bb9xKian+Lu6U6omok PkD0GWWKcMRXtiuPw3q3JYPW+lOLwCXuZNVSn5BY8LyFgpkGb11YflcpEXln3AQf C+T21CnCcRM8wYRjY3+3jBbNqoYg/1KNlShtiC312O/Ya469obNqmMtQrAPVmFH7 Hs04qdvOgTmY5h6dR9BcM8JAxQtkJLX3IhKifh+NWd6lgAsAkTKuwUmc78wZ6bJc 7nHgfh39AgMBAAECggEAcgB51us892xp29XnsQGJel6yB0z/3I9NEdmFky69vDH/ RaTVq+dYn4yRYAT5CiVX1w9JHIty5xQdqmpRXvnMl2ZbvaE9tsWYEFN0mqovIrgc cMGymXZOW9/0FhZT+i9SIGHaRbphZ6yT/tN+Y6IrrefFtPBtjUK6oH/SmOX9YH3o 6FVu9n4C9kE1k8qO1raVmWXjQxkHs86kpuCNFr2SgxeW5ZMR4oF7V4Jf8tsY8oGp SHrQZ/QixFOuhYCvx28U2GFwr0RUjyvzXs299UyLIRQd7RwoZLB+De/sXV/r2i6V r8aIaDj/3drYeQ1JLO8ipmL0oLkS/3mTsIRfopAZ4QKBgQDlMBE1ehRqCu6NTim0 6gA/Te71oNOj2+dDgzxW1UmoQ5ABm497Zs1KKh1EeyjPz6yLXTIk8J7Hf3QPqbGu Phwf/85d9fstL51i64wByvkyW8P/iliQ0GXqjIUpjgLM+LCGAAxvKf90C/OXhiRf 2PeY5L1Ij6EnVq0EnxymypLzmQKBgQCStNtCAXujt9UefjjS0vy0YhNLqADekOjL AapR3t7ZdvL9OFRVmhB6jkRIWKiM+++vzyzZMxhhVaSuh6Dz9h+ewFhEf04iTiZg ms2tgFGwowtbSmSl+gaIBwSVHoNJuoJAXNgwxuW3s7NkxDgMMHf9ZF+bmTbPrNPQ 9wgZC3O8BQKBgG/iqWQL9w9VyuOc9utlGT3OVAwBuZBS+HGTDc/uTAkjAphmUwOR SkMckDEwVtosrjVTB/nUpg8Kf6Rt2VoQ5DYS8bIZNcf3aMQz7aOqbUFSXzrPVTFN K5P3icKhm2hpN/QS7f8O57DFbOPaDsPj7evsLyPPSoMj409QRfJ/DoJxAoGAHW4Q igY4IlivdSWHCqvuq9T83/F88ykIuijEXRYjiGZ3SlrxeBam9Z7yjbzTWyzzIUaj TZMVcfk3RxfILwiRwUv+qQcMyo743epQFl0mhhO/JHohBLbKdqFJxwxO9AxpMrYt XGOaE6cF9tHyGGfkuj1XfKRYvYKDH2lfA38roW0CgYArWB95GNf8PHcbcz8x/Drm c+bdL0uyotcqhN4NuARpn7LKCHW+CS8TgIJUKT9DLCWSxTnNQOlIeFkZV+mSLn8G 2IrlKgv6xeenDHgmV9avEURJDNgoMubC8rhwpMS3Uc2/C4coag3112Yc1J/BPD+m 1ePmZkdrRp4CdxOyPVtBKQ== -----END PRIVATE KEY-----"
}
}
```

# 2. Symmetric encryption and decryption 
For AES symmetric encryption use `post /api/v1/encrypt_data_aes` and pass the data as the parameter:
```
{
  "data": "I fear not the man who has practiced 10,000 kicks once, but I fear the man who has practiced one kick 10,000 times."
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

# 3. Asymmetric encryption and decryption 
Asymmetric encryption is done using `post /api/v1/encrypt_data_rsa` and passing the following parameters:   
1. `data`, which is data to be encrypted
2. `rsa_public_key` of the recipient 

```
{
  "data": "Hello",
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

Asymmetric decryption is done using `post /api/v1/decrypt_data_rsa` and passing the following parameters:   

1. `rsa_private_key` of the recipient
2. `encrypted_data_rsa` - the encrypted data
```
{
  "rsa_private_key": "-----BEGIN PRIVATE KEY----- MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCTJ1tsj7rzONGa nSftiyw3AptSXUjMESqCbRGn+6257xU099lpbtiufCYQ7uM73f0LT/ECBrITq9Hl VPuwi1e4wrC8/QOjPFa1QYZygcRmAibNJckaiZmmvb4zpN1b6RuKxRQpuMgClC+c aWH3dm9eJFOy8yTELUt/xaSPnZXtd2fs7anW0aD+PjC/vyRP3AnrvEScGawakZRl lg8AxmuPRauxqS9Pm+rC2Qa6bY4j15E2UHuqAOy46vECbePLHXuz606LZJqyfUbL AdCZTqdikJKxW/rLAYIwfnEsYBZPeCUYLHabCMCL79BulJchaiuXPOVk5HbEj7zj h3IPFtYxAgMBAAECggEAY8GujK3zQqcmEPaw9qv+UVyHBxMOIqkQdFKUQZiwcPfP HJVY4cyvP7oR5DDOAuu+e0i6TXFUj1lPdXRjG4+a7Dmvrq6nJKXm8gF1r3KhPbX/ r9sJtd/KNeszYbdGCOTCMxTfUlld3cGvdQ1LyIKVhPCDfTCvn/5EzF2j7WgbF1tm oKuZB69LoVRSQ+rW9egQUWX5OCIC2aPReoRQCpPW3hz+CCuxk387twqlbS4/YFlB fdzC8N80umFvRFB8+YrgLrE/AM+dfFf8XMbwQDO13V4E6S5zVohAAJddxq7Nsv+e 1aZK+3NxlrkrOFij0ApLVtugToIBIMsGKbXuc5g6sQKBgQD9VIXvkX9fvr7wFgQ8 BDqDwavhUfQ3GdsZgzEnLK4SUgB1ApC7xMgwXauN38AL3kZEqQZNnWciQY8bU3i1 EFdFQ7K9n7s8nM/d8N/rbFIndRICJUQh47UAKWNZRaCV/IVMLPVjjHCjaej9aOUP JsyqbGfFA62rRCXoCHSzVjlFfwKBgQCUtF+PA0kP/V8CkaNV0VdRa702s57tu6Tg Quk8SOH4Ame9TcBrP95bpxUzBKapBj/ncW8lJKDD7zLYTQalWUG+KX/17i6NPgD6 vq+FwoCaGskRQTw3AUbkfHj6u7Cn41EmvxIZ2KWLi8Hl4+W3o6/mnsuucEZDOPwy FTN5FW+cTwKBgG0RTvjt86ENRrenQvtz9p1zbMT9u99dSm+ZhDgRjIBmvbui9x1g g7APJCVZCB4T/Lzi6MvR0O12vF5PedC60FgJ5ZKuirZ17Sjo4/9AC77hMHesA8Fz gCIpr5Rn3dO1fM5nLN9HP9ebaaxw1O3JDqTxN1wjUUpDdO6JdXUg0leRAoGBAI4l FSspos+MDSPxf0ZrQ6Jq8IW3kXYCZoqQq06bBJYEBpIoHoTmmnDV+Ce6jG0JslBU WEATETH6Foo4pt+rwHI8TTsSoKEW4ezOFg4wbKnibMz3pM2XhOKoMSTMAQObAVme T3kxZJ1NzN0pyc6Ow3gZ1u06GY/sivZ82aUm3nd1AoGAIqGOv9GiNYWJIdsdGmhI YS93Qj3Pw6ZSTqGTW4FYM9f4tawEWaGFGBL2CBYEp9nUTUBEAq8HJes0bimeScGn Tawewg84U4oiHuyTbtwIi5PkB+XIKfGaXU3SMaHYHiORRe7BhQwWKHpLdob4JJtm CdNBuN+I1w9yaWG1TeWVjk8= -----END PRIVATE KEY-----",
  "encrypted_data_rsa": "acN4z1AbYKHbuK5Tixi+AgYwg/3XMqVxU3UJmZrXcRuSXYSPyDLrB7+BQeiazfcFk9WxpnvT8nXHkQ6Hz2rTUF1K1Lv5XM33iQMqdRUa9WzQGJS9IakS5TSw+OpxhCR0KWa1kJ4XIa6QHwCGqUQrUo7WXTV9k/Lb55eLZh9bINy6LAAeYQfQX7LZMVCuC7lmJcUAkDTYuccgZdtAc1BCHl0ODq7rcMSLpr/M0h+tjKE6fuGP9AuB7NznoAy+7yf9toy67DNIWAeQXptTq8ukBJ6AzBTerUbTrbwOWlBWOyVcnsyPkXRtPUNryu5Jvqlw6//w0Fc9FG3dM+lmuzWQ5A=="
}
```
The output is the decrypted data.
```
{
  "status": 200,
  "decrypted_data": "Hello"
}
```
---
Have a query? Email us on info@primechain.in
