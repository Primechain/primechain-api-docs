# The electronic signature process

Let's take a simple example. 

## Step 1: Key generation
Rajnikant generates two keys, a public key and private key. These keys are nothing but extremely large numbers. Although the keys are mathematically related, it is "computationally infeasible"  to obtain the private key by using the public key. A signature created by Rajnikant’s private key can be verified using Rajnikant’s public key. 

Rajnikant's ***public*** key
```
03954458fe54151b32a035e6179b18a74cb027b0201404c522a41efdc043f0a138
```
Rajnikant's ***private*** key
```
VAV9DaTL8S4WjVCiezmGRTASH26GNmuaDVkee2jamZKVyWDLjMPE32R1
```
Rajnikant shares his public key with the whole world (through his website, blog, email etc.) but keeps his private key to himself. 

## Step 2: Computing the hash 
Now, Rajnikant wants to share his research on "self driving cars" with his friend Scarlett Johansson. To do this,  he creates a pdf file with details on his research. 

Rajnikant computes the hash of the pdf document containing his research. A one-way hash function takes an input (e.g. a PDF file, a video, an email, a string etc.) and produces a fixed-length output e.g. 160-bits. The hash function ensures that if the information is changed in any way – even by just one bit – an entirely different output value is produced.

Let's check out the sha512 hashes for three words - sanya, SANYA and Sanya.

The cryptographic hash for the word ***sanya*** is: 
```
a3627caf1e1aba8fb69509234a1a2ec5118e8b005ae68a66c0e601e4da868b83f3e765dd37463795f6f28ebc972ed38fcbe1160cedd6bee6c94ed073477b55c4
```
The cryptographic hash for the word ***SANYA*** is: 
```
70ea752fe0f800a374f2334c6e91efda445c8c01c812e6cd728156657360d76898f2d998ee412280c1ecb331f2690b500b6fc0ad916bb31311fc6b6203641496
```
The cryptographic hash for the word ***Sanya*** is: 
```
473c7793d15f3924439d5f00dd7dc4332e9dc47b2c2fbc31103e5bb55c211f836ad254ba61910d04f4168c107a6fbd7e979c4ad9e519ee9d57bdddd09b291a8c
```

It can be seen that by changing the case of the letter ***S***, from small to capital, an entirely different hash value is generated. What must be kept in mind is that irrespective of the size of the input, the hash output will always be of the same size. 

Two things must be borne in mind with regard to one-way hash functions:  
1.	It is computationally infeasible to find two different input messages that will yield the same hash output.  
2.	It is computationally infeasible to reconstruct the original message from its hash output.

## Step 3: Signing the document
Rajnikant now "electronically signs" the pdf. For this, his software takes the hash and Rajnikant's private key and uses an algorithm to compute the electronic signature for the file:
```
IK+0M1DdcCnjIzVB4j997WusLlglq3rhBFsqEsuxkOZ7XwseQR2yJQ9/eOp/h/a6lt38iTu4aYceSx1yE1oUYIs=
```
#### Step 4: Verifying the signature
Rajnikant emails the pdf and the electronic signature to Scarlet. She takes the document and computes the hash. Since the hash function software will always produce the same hash result for a particular message, she computes this as the hash:
```
a6ad1e35fc2e7e9de940c7adc520266641a09983940c1392cc16db535e91dae74b799f520dabfdf0883b143cf792343a44d62d2396d532bb597584bec598241b
```
She takes Rajnikant's public key, the document hash & the digital signature and uses an algorithm to verify the digital signature.
```
"pubkey": "03954458fe54151b32a035e6179b18a74cb027b0201404c522a41efdc043f0a138",
"signature": "IK+0M1DdcCnjIzVB4j997WusLlglq3rhBFsqEsuxkOZ7XwseQR2yJQ9/eOp/h/a6lt38iTu4aYceSx1yE1oUYIs=",
"hash": "c14fa6ea73269522b3362c637e9d90de39f58ac7696536019b7a3f2e0741e606"
```
If the signature is verified, it means that:
* the document has been signed by Rajnikant
* the document has not been altered in any way

From a legal point of view, electronic signature creation & verification achieves the following: 

1. ***Signer authentication:*** A person’s electronic signature cannot be forged. This means that if an electronic signature can be verified by Rajnikant’s public key, then it must have been created by Rajnikant’s private key. The digital signature verification process thus authenticates the identity of the signer. 

2. ***Message authentication:*** An electronic signature is based upon the hash value of the actual message. Thus an electronic signature is unique for each message and automatically authenticates the message. 

3. ***Affirmative act:*** The process of electronic signature creation requires the signer to use his private key (usually by entering a password). This overt act alerts the signer that he is initiating a transaction that may have legal consequences. 
