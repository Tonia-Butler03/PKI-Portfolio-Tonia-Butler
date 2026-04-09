# Lab 01 — Generate a CSR and Simulate the Issuance Workflow

## Overview
In this lab, I simulated the certificate issuance process by generating a private key, creating a Certificate Signing Request (CSR), and issuing a self-signed certificate using OpenSSL.

The objective was to understand how identity is established in Public Key Infrastructure (PKI), specifically how a subject proves ownership of a private key and requests a certificate from a Certificate Authority (CA). This lab focused on the relationship between cryptographic keys, identity factors, and the trust model used in certificate-authentication.

---

## Steps Performed
1. First, I generated a private key using OpenSSL to establish a secure identity.
2. Then, I created a CSR using the private key and defined subject details (Common Name, Organization, Country).
3. Next, I used the private key to self-sign the CSR and generate a certificate.
4. Last, I inspected the certificate to review subject, issuer, and validity details.


## Results

-The private key was successfully generated and stored locally.
-A CSR was created containing the subject identity information
-The associated public key derived from the private key
-A self-signed certificate was issued with the following characteristics:
Subject and Issuer fields are identical, indicating no external CA signed the certificate
-Public key algorithm: RSA (2048-bit)
-Signature algorithm: SHA256 with RSA
-Defined validity window (Not Before / Not After)
-Certificate inspection confirmed that the CSR data was embedded into the final certificate.


![diff](../../../assets/screenshots/test_diff.png)
```
![validity](../../../assets/screenshots/test_vailditiy_period.png)
```
![csr](../../../assets/screenshots/test_csr.pem.png)
```
![cert](../../../assets/screenshots/test_cert.pem.png)
```

## Key Findings

The CSR is a structured request that binds identity attributes to a public key, but it does not establish trust on its own.

The private key is never transmitted it remains local, and it is proof of ownership during certificate issuance.

In a self-signed certificate, the issuing authority is the same as the subject, and it bypasses the external trust model.

The certificate signature provides integrity and authenticity by linking the issuer to the subject’s public key.

The validity period is enforced at the certificate level and is critical for lifecycle management and trust decisions.

I verified that the private key and issued certificate matched by extracting and comparing their public keys:

  openssl rsa -in test_key.pem -pubout -out key_pub.pem  
  openssl x509 -in test_cert.pem -pubkey -noout > cert_pub.pem  
  diff key_pub.pem cert_pub.pem  

The diff command returned no output, confirming that the certificate corresponds to the correct private key. This validation step is critical before deploying certificates.



---

## Explanation
This lab demonstrates the foundational PKI workflow: key generation → CSR → certificate issuance.

The CSR is a critical component because it proves possession of the private key while requesting identity validation. In a real-world PKI environment, the CSR would be submitted to a trusted Certificate Authority, which would validate the subject’s identity before issuing a signed certificate.

By self-signing the certificate in this lab, I simulated the CA role, but without external trust. As a result, while the certificate is technically valid, it is not trusted by default systems because it does not chain back to a trusted root CA.

This highlights a core principle of PKI:

Validity does not always mean Trust

A certificate can be valid but still untrusted if it is not  in a trusted certificate hierarchy.

This workflow directly connects to TLS, where servers present certificates to clients, and clients validate those certificates using a chain of trust to determine whether a secure connection can be established.

---

## Challenges / Troubleshooting
Encountered errors when using the -subj flag in Git Bash due to formatting and path parsing issues on Windows.
Verified each step using ls and OpenSSL inspection commands to confirm file creation before proceeding.


## Artifacts
test_key.pem — RSA private key used to establish identity
test_csr.pem — Certificate Signing Request containing subject information and public key
test_cert.pem — Self-signed X.509 certificate generated from the CSR
lab-01-generate-csr.md — Lab write-up
Screenshots 
---

*CVI PKI Career Pathway — Foundations Phase*
