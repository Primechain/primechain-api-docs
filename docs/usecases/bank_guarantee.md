# Bank guarantee

Through a bank guarantee, a bank promises to cover a loss if a borrower defaults. Types of guarantees include Advance Payment Guarantee, Bid Bond Guarantee, Confirmed Payment Order, Credit Security Bond, Deferred Payment Guarantee, Financial Guarantee, Foreign Bank Guarantee, Performance Bond, Performance Guarantee, Rental Guarantee, and Warranty bond.

Some of the benefits of using blockchain for issuing bank guarantees are: (1) Each bank guarantee is digitally signed by the issuing bank; (2) Regulator nodes enable real-time supervision by the authorities; (3) The system is API driven and can easily be integrated with the banks' core banking and other legacy systems.


1. [Create, encrypt, sign and publish a bank guarantee to the blockchain](#1-create-encrypt-sign-and-publish-a-bank-guarantee-to-the-blockchain)

2. [Decrypt, verify and retrieve a bank guarantee from the blockchain](#2-decrypt-verify-and-retrieve-a-bank-guarantee-from-the-blockchain)


## 1. Create, encrypt, sign and publish a bank guarantee to the blockchain
To create a bank guarantee on the blockchain, use `post /api/v1/encrypt_sign_store_data` and pass 2 parameters: 
1. the bank guarantee data 
2. the primechain address of the bank issuing the guarantee

Sample input
```
{
  "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2",
  "data": 
    {
      "guarantee_number": "ASDRE76464",
      "guarantee_currency": "USD",
      "guarantee_amount_words": "Twenty Two million",
      "guarantee_amount_figures": "22,000,000.00",
      "guarantee_date_of_issue": "17-December-2018",
      "guarantee_date_of_maturity": "16-March-2019",
      "guarantee_beneficiary": "Nicole Corporation",
      "guarantee_details": "On behalf of our client, Nicole Corporation, for value received, we, Global Bank, hereby irrevocably and unconditionally and without protest or notification, promise to pay against this, our irrevocable bank guarantee, to the order of Nicole Corporation, as beneficiary, on the maturity date, the sum of Twenty Two million United States Dollars ($22,000,000.00 USD), upon their first written demand for payment hereunder. Such payment shall be made without set-off, free and clear of any deductions, charges, fees, levies, taxes or withholdings of any nature. This bank guarantee is transferable, without payment of any transfer fees. This bank guarantee is issued in accordance with the uniform customs and practices for bank guarantees, as set forth by the International Chamber of Commerce, Paris, France, latest revision of ICC 500 publication. This bank guarantee shall be governed by and construed in accordance with the laws of the Republic of India and is free and clear of any lien and encumbrances and is of non-criminal origin.",
      "authorized_bank_officer_name": "Nicole Kidman",
      "authorized_bank_officer_title": "Vice President",
      "authorized_bank_officer_telephone": "230950934545",
      "authorized_bank_officer_facsimile": "367645455624",
      "authorized_bank_officer_email": "nicole@example.com"      
    }
}
```
This is what happens:   

### Step 1: Hash computation
The SHA-512 hash of the bank guarantee is computed.

### Step 2: Signing
The hash is signed using the private key of the issuing bank (using the ECDSA algorithm).

### Step 3: Storing the signature
The following are published to the `DATA_SIGNATURE_MASTERLIST` stream:
1. the digital signature
2. the hash
3. the primechain address of the issuing bank 

### Step 4: Encrypting the data
The data is encrypted using the AES (Advanced Encryption Standard) algorithm and the following are generated: 
1. the encrypted version of the data
2. the AES password
3. the Initialization Vector (IV)   
4. the Authentication Tag (tag)

### Step 5: Storing the encrypted data
The encrypted data and the tag are published to the `DATA_MASTERLIST` stream

### Step 6: Output 
The following is the output:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the issuer's primechain address were published to the DATA_SIGNATURE_MASTERLIST stream
3. The digital signature
3. The AES password
4. The Initialization Vector (IV)

```
{
"status": 200,
"response": 
  {
    "tx_id_enc_data": "a8441a8e8fe52c6f84941fd1f08f774ecbf0dc9edf9fd18e9f9d20f1d2945940",
    "tx_id_signature": "8f15a1b3bc4cbeeae89ea28e77982ac7baa04c45870d9d40086b799ad795487f",
    "signature": "H523zhPwR1gdPn2R0/JlfTJLWB5HaII96vJcDx4qy8f2StF1AE6Qfft8lqE2IoDd2czj5cW8i9ZJLaWXu7KkEyE=",
    "aes_password": "5M1qnsYeRmSvlwNtZ8oJiHC0g9ucVrgc",
    "aes_iv": "zNc59qnYapAw"
  }
}
```

## 2. Decrypt, verify and retrieve a bank guarantee from the blockchain
To retrieve a bank guarantee from the blockchain, use `post /api/v1/decrypt_download_data` and pass these values:
1. the id of the transaction in which the encrypted data and tag were published to the DATA_MASTERLIST stream
2. the id of the transaction in which the digital signature, hash and the issuers's primechain address were published to the DATA_SIGNATURE_MASTERLIST stream
3. The AES password
4. The Initialization Vector (IV)

```
{
    "tx_id_enc_data": "b40cb6e4b95e72510413cd20030c3ea7052ef1dea8deb9340efb5e39d05f8394",
    "tx_id_signature": "3f06f98af6b7acbb9b7ec26f7c692bf39b999fc645cce5f969ca5467470fc235",
    "aes_password": "R1E3GYxjAc0Gfa8xEqRNtOdJfWErOBz7",
    "aes_iv": "VioxHPgIDj7F"
}
```
This is what happens:   

### Step 1: Retrieval of signing data 
The digital signature, hash and the primechain address of the issuing bank are retrieved from the DATA_SIGNATURE_MASTERLIST stream.

### Step 2: Retrieval of encrypted data 
The encrypted data and tag are retrieved from the DATA_MASTERLIST stream.

### Step 3: Decryption
The encrypted data is decrypted.

### Step 4: Verification
The digital signature is verified

### Step 5: Output
The output will be the bank guarantee and the details of the signer.
```
{
  "status": 200,
  "response": 
    {
      "data": 
        {
          "guarantee_number": "ASDRE76464",
          "guarantee_currency": "USD",
          "guarantee_amount_words": "Twenty Two million",
          "guarantee_amount_figures": "22,000,000.00",
          "guarantee_date_of_issue": "17-December-2018",
          "guarantee_date_of_maturity": "16-March-2019",
          "guarantee_beneficiary": "Nicole Corporation",
          "guarantee_details": "On behalf of our client, Nicole Corporation, for value received, we, Global Bank, hereby irrevocably and unconditionally and without protest or notification, promise to pay against this, our irrevocable bank guarantee, to the order of Nicole Corporation, as beneficiary, on the maturity date, the sum of Twenty Two million United States Dollars ($22,000,000.00 USD), upon their first written demand for payment hereunder. Such payment shall be made without set-off, free and clear of any deductions, charges, fees, levies, taxes or withholdings of any nature. This bank guarantee is transferable, without payment of any transfer fees. This bank guarantee is issued in accordance with the uniform customs and practices for bank guarantees, as set forth by the International Chamber of Commerce, Paris, France, latest revision of ICC 500 publication. This bank guarantee shall be governed by and construed in accordance with the laws of the Republic of India and is free and clear of any lien and encumbrances and is of non-criminal origin.",
          "authorized_bank_officer_name": "Nicole Kidman",
          "authorized_bank_officer_title": "Vice President",
          "authorized_bank_officer_telephone": "230950934545",
          "authorized_bank_officer_facsimile": "367645455624",
          "authorized_bank_officer_email": "nicole@example.com"
        },
       "signer_detail": 
        {
          "name": "Noodle Bank Official Signer",
          "primechain_address": "1N9VtvZvP3rsw5Rf4Qpi12TWBaDoEwM2BAEsv2"
        },
        "signature_status": true
    }
}

```
