# Lab — 03-certificate-chain

## Overview
This lab focused on understanding how certificate chains establish trust in PKI systems. I investigated how a leaf certificate, intermediate certificate, and root certificate work together to validate identity. The goal was to see how trust is built and verified using OpenSSL.

What PKI concept or system behavior were you investigating

I was investigating how certificate chains establish trust within a PKI system. This includes understanding how a leaf certificate, intermediate certificate, and root certificate are connected through issuer and subject relationships. I also explored how systems validate certificates. Overall, the lab showed how trust is verified behind the scenes when accessing secure websites.

## Environment
Document the environment used to complete the lab.

- Operating System:Windows
- Terminal Used:Git Bash
- OpenSSL Version (if applicable):3.4.4

---

## Steps Performed

1.Retrieved the certificate chain from a live website using OpenSSL.
2.Separated the certificates into server, intermediate, and root files.
3.Verified the certificate chain using OpenSSL and analyzed the results Pem:ok.

---

## Results

The key outputs included the OpenSSL command results showing the certificate chain for github.com. I observed important fields such as the subject (CN=github.com), issuer (Sectigo intermediate), and the root authority (USERTrust). The verification result showed server.pem: OK when using the intermediate certificate, confirming the chain was valid. This demonstrated how the certificate chain successfully links back to a trusted root.

![Certificate Chain Output](../../assets/screenshots/week-03/lab-03-certificate-chain.png)

## Key Findings

• The leaf certificate belonged to github.com
• The intermediate certificate was issued by Sectigo
• The root certificate was part of the USERTrust network
• Certificate verification succeeded when using the intermediate with the system trust store-I received support to acess the results using the trust store.


---

## Explanation
The results matter because the issuer field connects each certificate in the chain, allowing systems to verify trust step by step. The certificate chain validates successfully when each certificate is signed by a trusted authority and links back to a trusted root. If there is a misconfiguration, such as using the wrong root certificate, the chain breaks and validation fails. This process is critical for TLS because it ensures secure and trusted communication between users and websites.


## Challenges / Troubleshooting
One challenge I encountered was a verification failure due to using the wrong root certificate. I resolved this by analyzing the issuer and subject fields to understand the correct chain relationship. I also used the system trust store to successfully validate the certificate.

## Artifacts

• server.pem
• intermediate.pem
• root.pem


CVI PKI Career Pathway — Foundations Phase
