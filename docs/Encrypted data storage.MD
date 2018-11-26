# Encrypted data storage

1. [Encrypt, sign and upload data](#1-encrypt-sign-and-upload-data)
2. [Decrypt and download data](#2-decrypt-and-download-data)
3. [Encrypt, sign and upload file](#1-encrypt-sign-and-upload-file)
4. [Decrypt and download file](#2-decrypt-and-download-file)

## 1. Encrypt, sign and upload data
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_data` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
  "address":"1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
  "file":"<your file>"
}
```
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
To decrypt and download a file, use `post /api/v1/decrypt_download_data` and pass these values:
* The blockchain address using which the file was signed
* The transaction id of the transaction in which the dats was stored on the blockchain
* The AES decryption key data - password and iv
```
{
  "address": "1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
  "txid": "6b0dd5214b67bf633cdedef33712580704139e94d03ac783af5f6657d76d718b",
  "password": "wYKTKWMDZXHMfSGiyGKgHVUuqdVVezgE",
  "iv": "Q68wBhkE9bwg"
}
```
The file will get downloaded.

## 3. Encrypt, sign and upload file
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_file` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
  "address":"1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
  "file":"<your file>"
}
```
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

## 4. Decrypt and download file
To decrypt and download a file, use `post /api/v1/decrypt_download_file` and pass these values:
* The blockchain address using which the file was signed
* The transaction id of the transaction in which the dats was stored on the blockchain
* The AES decryption key data - password and iv
```
{
  "address": "1b8yZEFmK2HSTKUm1rgKUDABPAq8CGRJYQWW2k",
  "txid": "6b0dd5214b67bf633cdedef33712580704139e94d03ac783af5f6657d76d718b",
  "password": "wYKTKWMDZXHMfSGiyGKgHVUuqdVVezgE",
  "iv": "Q68wBhkE9bwg"
}
```
The file will get downloaded.

