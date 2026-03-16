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



---

## Key Findings
Document the most important observations from the lab.

Examples:

- Certificate issuer
- Public key algorithm used
- Certificate extensions present
- Trust chain relationships
- Validation results

•  
•  
•  

---

## Explanation
Explain **why the results matter**.

Examples:

- Why the issuer is important in PKI
- Why SAN is required for modern TLS validation
- Why the certificate chain validates successfully
- Why a misconfiguration would cause a failure

---

## Challenges / Troubleshooting
Document any issues encountered during the lab and how you resolved them.

Examples:

- command errors
- missing intermediate certificates
- verification failures

---

## Artifacts
List the files generated during this lab.

Examples:

- leaf_cert.pem
- server.pem
- intermediate.pem
- root.pem
- screenshots stored in assets/

---

CVI PKI Career Pathway — Foundations Phase
