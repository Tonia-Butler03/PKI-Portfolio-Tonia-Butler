# Lab — 02-certificate-extenstions

## Overview
The purpose of this lab was to understand how X.509 certificate extensions work and how they control how a certificate is used. I reviwed a real certificate to identify key extensions like SAN, Key Usage, and Extended Key Usage. This helped me see how certificates are validated and used in secure communication.
  
In this lab, I was investigating how certificate extensions define the rules and behavior of a certificate within a PKI system. I focused on how extensions like SAN, Key Usage, and Basic Constraints impact TLS validation and determine whether a certificate is trusted. This shows how PKI enforces security by controlling how certificates can be used. 
  
  
  
## Environment
Document the environment used to complete the lab.

- Operating System:Windows
- Terminal Used:Git Bash
- OpenSSL Version (if applicable):3.4.4

---

Steps Performed

1. I used OpenSSL to inspect the certificate that I previously retrieved and converted it into a readable format using the -text -noout command.
2. I reviewed the certificate output and located the X509v3 extensions section to identify key extensions like SAN, Key Usage, Extended Key Usage, and Basic Constraints.
3. I analyzed each extension to understand its purpose. The Subject Alternative Name (SAN) showed the domains the certificate is valid for, this is used during TLS validation. The Key Usage defined how the certificate can be perform, such as digital signatures. The Extended Key Usage specified that the certificate is used for TLS web server authentication. 



## Results


![Certificate Output](../../assets/screenshots/week-03/lab-02-certificate-extensions.png)

---

## Key Findings

• The certificate was issued by Google Trust Services, which acts as the Certificate Authority.

• The public key algorithm used is Elliptic Curve (EC) with a 256-bit key, showing modern and faster encryption.

• The certificate includes important extensions such as Subject Alternative Name (SAN), Key Usage, and Extended Key Usage.

• The SAN field contains multiple domains like *.google.com, confirming the certificate supports many services.

• The Basic Constraints shows CA:FALSE, meaning this is a leaf certificate and cannot issue other certificates.

• The Extended Key Usage confirms the certificate is used for authentication, supporting secure HTTPS connections.
 

## Explanation

These results matter because they show how trust and validation work in PKI systems. The issuer is important because it represents a trusted Certificate Authority that verifies the identity of the certificate. The SAN field is required for TLS validation because the browsers checks it to confirm the certificate matches the domain that a user is accessing. If the extension is misconfigured, the certificate could fail and the connection would not be secure.

---

## Challenges / Troubleshooting

During this lab, I initially ran into permission errors when trying to create directories because I was working from the root directory instead of my local repository. I resolved this by navigating to the correct GitHub project folder before running my commands. I also had to adjust file paths since I had previously moved the certificate to a different folder, which caused some “file not found” errors. Once I corrected the paths and confirmed my working directory, the commands executed successfully and I was able to complete the lab.


## Artifacts
leaf_cert.pem (copied and reused from Lab 01 for extension analysis)
certificate-extensions.md (analysis of certificate extensions)
Screenshot of OpenSSL certificate output stored in the assets folder

---

CVI PKI Career Pathway — Foundations Phase
