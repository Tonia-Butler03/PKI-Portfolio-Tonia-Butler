# Lab — Digital Signatures

## Overview
Briefly describe the purpose of this lab in your own words. 

The purpose of this lab was to understand how digital signatures protect data by ensuring integrity and authenticity. In this lab, I generated a key pair, signed a file with a private key, and verified the signature using the corresponding public key. I also observed how modifying the file caused the verification process to fail. This lab showed how digital signatures detect tampering and confirm the identity of the signer.

What PKI concept or system behavior were you investigating?

The PKI concept in this lab confirmed that digital signatures use hashing and asymmetric cryptography to verify the integrity and authenticity of data. This same process is used in the PKI process when Certificate Authorities sign digital certificates to establish trust.

---

## Environment
Document the environment used to complete the lab.

- Operating System:Windows
- Terminal Used:GIT
- OpenSSL Version (if applicable):3.4.4

---

## Steps Performed
Summarize the key steps you performed to complete the lab.


1. First, I created a directory in my repository to store the files for the digital signature lab.

2. Then, I created a text file that would act as the artifact to be signed.

3. Next, using OpenSSL, I generated an RSA private key and then extracted the corresponding public key.

4. I used the private key to create a digital signature for the text file.

5. I verified the signature using the public key and confirmed that the verification was successful.

6. Finally, I modified the file and ran the verification again the signature validation failed after the file was tampered with.
   


## Results
Include the important outputs or findings from the lab.

assets/screenshots/Assests screenshot week 02 MKDIR-Digital Signatures.png

assets/screenshots/Assests screenshot week 02 Private Key-Digital Signatures.png

assets/screenshots/Assests screenshot week 02 Public Key-Verifed Digital Signatures.png

assets/screenshots/Assests screenshot week 02 Tampered Digital Signatures.png

---

## Key Findings
Document the most important observations from the lab.

-The digital signature successfully verified when the original file remained unchanged.

-The signature verification failed after the file was modified, demonstrating that even small changes break the signature.

-The private key was used to create the digital signature, while the public key was used to verify it.

-This process demonstrates how digital signatures provide integrity and authenticity in cryptographic systems.


## Explanation
Explain **why the results matter**.

These results matter because digital signatures are a main component used to establish trust in PKI systems. The lab shows that a digital signature confirms both the integrity of a file and the authenticity of the signer. Integrity is important because it ensures the data has not been altered after it was signed. Authenticity is verified because only the owner of the private key can generate the signature, while anyone with the public key can verify it.

## Challenges / Troubleshooting
Document any issues encountered during the lab and how you resolved them.

One challenge encountered during the lab was ensuring the OpenSSL commands were entered correctly in the terminal. Some commands were initially written on multiple lines, which caused errors until they were combined into a single command. Another potential issue was making sure the file paths were correct within the repository so the files could be located by OpenSSL.


## Artifacts
List the files generated during this lab.

- screenshots stored in assets/

---

CVI PKI Career Pathway — Foundations Phase
