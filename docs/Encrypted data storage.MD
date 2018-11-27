# Encrypted data storage

1. [Encrypt, sign and upload data](#1-encrypt-sign-and-upload-data)
2. [Decrypt and download data](#2-decrypt-and-download-data)
3. [Encrypt, sign and upload file](#3-encrypt-sign-and-upload-file)
4. [Decrypt and download file](#4-decrypt-and-download-file)

## 1. Encrypt, sign and upload data
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_data` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
aaaaa
}
```
The output contains:
1. The transaction id of the transaction in which the dats was stored on the blockchain
2. The digital signature
3. The AES decryption key data - password and iv
```
bbbb
```

## 2. Decrypt and download data
To decrypt and download a file, use `post /api/v1/decrypt_download_data` and pass these values:
* The blockchain address using which the file was signed
* The transaction id of the transaction in which the dats was stored on the blockchain
* The AES decryption key data - password and iv
```
ccccc
```
The output will be the data.
```
dddd
```

## 3. Encrypt, sign and upload file
To encrypt and upload a file, use `post /api/v1/encrypt_sign_store_file` and pass the blockchain address (using which the file will be signed) and the file data.
```
{
  "primechain_address":"aaaaa",
  "file":"<your file>"
}
```
The output contains:
1. The transaction id of the transaction in which the dats was stored on the blockchain
2. The digital signature
3. The AES decryption key data - password and iv
```
eeeeee
```

## 4. Decrypt and download file
To decrypt and download a file, use `post /api/v1/decrypt_download_file` and pass these values:
* The blockchain address using which the file was signed
* The transaction id of the transaction in which the dats was stored on the blockchain
* The AES decryption key data - password and iv
```
fffffff
```
The file will get downloaded.
