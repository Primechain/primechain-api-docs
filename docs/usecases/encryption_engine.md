# Encryption Engine

[![Primechain API](https://img.shields.io/badge/Built%20by-Primechain-blue.svg)](http://www.primechaintech.com/)

The Encryption Engine provides symmetric (AES) and asymmetric (RSA) encryption functions – secure key generation, encryption and decryption.

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

# 2. Symmetric encryption
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
