# Lab — Hashing & Integrity
## Overview
Briefly describe the purpose of this lab in your own words.
The purpose of this lab was to understand how cryptographic hashing works and how it supports data integrity within PKI systems. In this lab, a SHA-256 hash was generated for a file, the file was changed, and a new hash was created to understand how a small change can result in a completely different hash. This exersise, shows how hashing can detect tampering of data. 

What PKI concept or system behavior were you investigating?

The PKI concept investigated in this lab was data integrity and how hash functions are used to verify that information has not been altered.

---

## Environment
Document the environment used to complete the lab.

- Operating System:Windows
- Terminal Used:GIT
- OpenSSL Version (if applicable):3.4.4

---

## Steps Performed
Summarize the key steps you performed to complete the lab.

Do **not copy the lab instructions**.  
Describe what you actually did.

1. First, I created a directory within the lab repository to store the hashing artifacts and generated a test file containing a short message. 
2. Next, I used OpenSSL to generate a SHA-256 hash of the file and saved the hash output for reference. 
3. Last, I modified the contents of the file and generated a second SHA-256 hash, this showed how the hash value changed. 

---

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
