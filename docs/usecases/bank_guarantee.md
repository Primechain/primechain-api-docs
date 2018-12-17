# Bank guarantee

Through a bank guarantee, a bank promises to cover a loss if a borrower defaults. 

***Types of guarantees:***
1. Advance Payment Guarantee
2. Bid Bond Guarantee
3. Confirmed Payment Order 
4. Credit Security Bond
5. Deferred Payment Guarantee
6. Financial Guarantee
7. Foreign Bank Guarantee
8. Performance Bond 
9. Performance Guarantee
10. Rental Guarantee
11. Warranty bond 

***Some of the benefits of using blockchain for issuing bank guarantees are:*** 
1.	Each document is digitally signed by the member bank.
2.	Regulator nodes enable real-time supervision by the authorities.
3.	The system is API driven and can easily be integrated with the banks' core banking and other legacy systems

[1. Creating a bank guarantee on the blockchain](#1-creating-a-bank-guarantee-on-the-blockchain)


## 1. Creating a bank guarantee on the blockchain
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
      "guarantee_amount_words": "Twenty Two million"
      "guarantee_amount_figures": "22,000,000.00"
      "guarantee_date_of_issue": "17-December-2018"
      "guarantee_date_of_maturity": "16-March-2019"
      "guarantee_beneficiary": "Nicole Corporation"
      "guarantee_details": 
      "
        On behalf of our client, Nicole Corporation, for value received, we, Global Bank, hereby irrevocably and unconditionally and without protest or notification, promise to pay against this, our irrevocable bank guarantee, to the order of Nicole Corporation, as beneficiary, on the maturity date, the sum of Twenty Two million united states dollars ($22,000,000.00 usd), upon their first written demand for payment hereunder. Such payment shall be made without set-off, free and clear of any deductions, charges, fees, levies, taxes or withholdings of any nature.
      
        This bank guarantee is tranferable, without payment of any transfer fees.

        This bank guarantee is issued in accordance with the uniform customs and practices for bank guarantees, as set forth by the International Chamber of Commerce, Paris, France, latest revision of ICC 500 publication.

        This bank guarantee shall be governed by and construed in accordance with the laws of the Republic of India and is free and clear of any lien and encumbrances and is of non-criminal origin.
      "
      "authorized_bank_officer_name": "bbb"
      "authorized_bank_officer_title": "bbb"
      "authorized_bank_officer_telephone": "bbb"
      "authorized_bank_officer_facsimile": "bbb"
      "authorized_bank_officer_e": "bbb"      
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
2. the id of the transaction in which the digital signature, hash and the signer's primechain address were published to the DATA_SIGNSTURE_MASTERLIST stream
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
