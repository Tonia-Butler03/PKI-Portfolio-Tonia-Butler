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

1. First, I created a directory within the lab repository to store the hashing artifacts and generated a test file containing a short message. 
2. Next, I used OpenSSL to generate a SHA-256 hash of the file and saved the hash output for reference. 
3. Last, I modified the contents of the file and generated a second SHA-256 hash, this showed how the hash value changed. 

---

## Results
Include the important outputs or findings from the lab.

assets/screenshots/Assests screenshot week 02 Hashing-Modified.png

assets/screenshots/Assests screenshot week 02 Hashing-Tampered.png

assets/screenshots/Assests screenshot week 02 Hashing-Text.png

assets/screenshots/Assests screenshot week 02 MKDIR-Hashing.png

---

## Key Findings
Document the most important observations from the lab.

•  The SHA-256 hash produced a fixed-length hexadecimal value that served as a digital fingerprint for the file.

•  When comparing the two hash outputs it was confirmed that even a small change to a file results in different hash values, this highlight the effect of cryptographic hashing.

---

## Explanation
Explain **why the results matter**.

These results matter because cryptographic hashing is used to verify data integrity in PKI systems. If a file or message is altered, the hash value changes, allowing systems to detect tampering. This process is used in digital signatures, certificates, and software verification to ensure that data has not been modified and to ensure integrity.

---

## Challenges / Troubleshooting
Document any issues encountered during the lab and how you resolved them.

One challenge that I encountered during the lab was receiving a “No such file or directory” error when attempting to generate the hash. This occurred because the command was executed from the wrong directory. The issue was resolved by connecting the correct folder to the repository before running the OpenSSL command.

## Artifacts
List the files generated during this lab.

- screenshots stored in assets/

---

CVI PKI Career Pathway — Foundations Phase
