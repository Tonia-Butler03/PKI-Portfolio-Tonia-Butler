 # Lab — 01-certificate-fields


## Overview

The purpose of this lab was to understand how to read and interpret the fields of an X.509 certificate. I investigated how certificates represent identity and trust in PKI systems by retrieving and analyzing a real certificate from a live website, google.com. By reviewing the key components of the certificate, I was able to validate the authenticity of the Certificate Authority (CA) and understand how trust is established.

What PKI concept or system behavior were you investigating?

I was investigating how X.509 certificates represent identity and establish trust in PKI systems. Specifically, I looked at how key fields like the issuer, subject, and public key are used to verify a certificate’s authenticity. This also helped me understand how certificate validation works during secure connections like HTTPS. Overall, I was exploring how trust is built and verified through certificate authentication.


## Environment
Document the environment used to complete the lab.

- Operating System:Windows
- Terminal Used:Bash
- OpenSSL Version (if applicable):3.4.4

---

## Steps Performed
1. First, I created a local directory to store my lab files. 
2. Then I used OpenSSL to connect to google.com and retrieve the certificate chain. I used the commands to produce and copy the leaf certificate. I saved it as a .pem file.
3. After that, I used OpenSSL to parse the certificate and view the readable output, this allowed me to identify key certificate fields.


---

## Results

![Certificate Output](assets sceentshot week 03 identity & trust attributes.png)

---

## Key Findings
The certificate was issued by Google Trust Services (WR2), which is an intermediate Certificate Authority
The public key algorithm used is Elliptic Curve (EC) the key size is smaller and the speed is faster
The certificate includes extensions such as Subject Alternative Name (SAN) for multiple domains
The certificate chain validated successfully, a trusted connection is showen


## Explanation
The issuer is important in PKI because it shows which trusted Certificate Authority signed the certificate, allowing systems to verify its authenticity. The SAN extension is required for TLS because it lists all domain names associated with the certificate. The certificate validates successfully because each certificate in the chain is trusted up to a root CA. If there were a misconfiguration, like an untrusted issuer or expired certificate, the connection would fail and therfore, would result in a insecure connecction.


## Challenges / Troubleshooting
I initially encountered a permission error when trying to create directories in the root folder, which I resolved by navigating to my user directory. I also got stuck in the nano editor and had difficulty exiting, which I resolved by closing and reopening the terminal. These issues helped me better understand terminal navigation and command usage.


## Artifacts
leaf_cert.pem
Screenshot of certificate output stored in assets/


---

CVI PKI Career Pathway — Foundations Phase
