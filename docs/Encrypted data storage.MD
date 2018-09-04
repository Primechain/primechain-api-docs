# Encrypted data storage.MD

1. [Encrypt, sign and upload data](#1-encrypt-sign-and-upload-data)
2. [Decrypt and download data](#2-decrypt-and-download-data)

## 1. Encrypt, sign and upload data
To encrypt and upload a file, use `encrypt_sign_store_data` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
"address":"1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
file:<your file>
}
```
![Encrypt, sign and upload data](http://www.primechaintech.com/img/api_documentation/encrypt_sign_store_data.png)

The output contains:
1. The transaction id of the transaction in which the dats was stored on the blockchain
2. The digital signature
3. The AES decryption key data - password and iv
```
{
"status": 200,
"transaction_id": "6b0dd5214b67bf633cdedef33712580704139e94d03ac783af5f6657d76d718b",
"signature": "H7nCV1EEdnWPs287G9xkHuAhfhtIBqrBce2r/FWAURG5EXzB4VR0J378LlGgQCC2I9NMPLB2Uc4j8hHVNaJl2RE=",
"password": "wYKTKWMDZXHMfSGiyGKgHVUuqdVVezgE",
"iv": "Q68wBhkE9bwg"
}
```

## 2. Decrypt and download data
To decrypt and download a file, use `decrypt_download_data`
