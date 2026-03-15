# Lab — Symmetric Encryption

## Overview
The purpose of this lab was to understand how symmetric encryption works and how it protects sensitive data. Symmetric encryption uses a single secret key to both encrypt and decrypt information. During the lab, plaintext was converted into unreadable ciphertext and then decrypted back to its original form. This demonstrated how encryption provides confidentiality, which is a key component of the CIA triad and the PKI process.

What PKI concept or system behavior were you investigating?
In this lab, I was investigating how symmetric encryption is used to protect data confidentiality within cryptography. The lab demonstrated how a single shared key is used to encrypt plaintext into ciphertext and then decrypt it back to its original form. This shows how encryption protects sensitive data and supports secure communication within PKI systems.

---

## Environment
Document the environment used to complete the lab.

- Operating System: Windows OS
- Terminal Used:Windows GIT
- OpenSSL Version (if applicable):3.44

---

## Steps Performed
Summarize the key steps you performed to complete the lab.

Do **not copy the lab instructions**.  
Describe what you actually did.

1.First, I creted an artifacts directory and a brnach of the CVI Labs. I orginally used Powershell for the CVI process, then I used the terminal GIT becasue the commands were to long on PS causing errors. I transtioned to GIT to crete files for encrypted and decrypted contents.

2.Next, I convereted plain text into cypiher text, encrypting data and I created a password to protect the confidentiality of the data.

3.Last, I decrypted the data and used the password to verify and confirm the integrity of the contents, this step confirmed that there was no difference and the contents were authentic.

---

## Results
Include the important outputs or findings from the lab.

Encryption/Plain text
Tonia@ToniaB03 MINGW64 ~
$ openssl enc -aes-256-cbc -salt -pbkdf2 -in labs/02-week-02-cryptography-fundamentals/submissions/encrypted/plaintext.txt -out labs/02-week-02-cryptography-fundamentals/sbmissions/encrypted/plaintext.txt.enc
enter AES-256-CBC encryption password:

Verifying - enter AES-256-CBC encryption password:

Tonia@ToniaB03 MINGW64 ~
$ ls labs/02-week-02-cryptography-fundamentals/submissions/encrypted
plaintext.txt  plaintext.txt.enc

Tonia@ToniaB03 MINGW64 ~
$ cat labs/02-week-02-cryptography-fundamentals/submissions/encrypted/plaintext.txt.enc
Salted__F▒▒
:,SSv9RXa'G    _51$iI|▒+[ ▒▒G*▒▒▒]^fgx&Wu{▒▒&ynw

Decryption
Tonia@ToniaB03 MINGW64 ~
$ openssl enc -d -aes-256-cbc -pbkdf2 -in labs/02-week-02-cryptography-fundamentals/submissions/encrypted/plaintext.txt.enc -out labs/02-week-02-cryptography-fundamentals/submissions/encrypted/plaintext.decrypted.txt
enter AES-256-CBC decryption password:


Tonia@ToniaB03 MINGW64 ~
$ diff labs/02-week-02-cryptography-fundamentals/submissions/encrypted/plaintext.txt labs/02-week-02-cryptography-fundamentals/submissions/encrypted/plaintext.decrypted.txt

Tonia@ToniaB03 MINGW64 ~
$

Tonia@ToniaB03 MINGW64 ~
$ ls labs/02-week-02-cryptography-fundamentals/submissions/encrypted
plaintext.decrypted.txt  plaintext.txt  plaintext.txt.enc

If you include screenshots, store them in the **assets folder** and reference them here.

assets/screenshots/Assests screenshot week 02 Decryption.png

assets/screenshots/Assests screenshot week 02 MKDIR.png

assets/screenshots/Assests screenshot week 02 Encryption.png

---

## Key Findings
Document the most important observations from the lab.


• The key finding was trust in the encryption process, meaning that only the correct password can decrypt the encrypted file.

• AES-256 encryption successfully transformed readable plaintext into unreadable ciphertext.

• The encrypted file appeared as random binary data, confirming that the original message was protected

---

## Explanation
Explain **why the results matter**.

These results matter because symmetric encryption plays a critical role in protecting sensitive data during transmission and storage. AES encryption ensures confidentiality by converting readable plaintext into ciphertext that cannot be understood without the correct key. With TLS, symmetric encryption is used because it is fast and efficient for protecting large amounts of data after a secure key exchange occurs. This process ensures that data remains private and secure between communicating systems.

Examples:

- Why the issuer is important in PKI
- Why SAN is required for modern TLS validation
- Why the certificate chain validates successfully
- Why a misconfiguration would cause a failure

---

## Challenges / Troubleshooting
Document any issues encountered during the lab and how you resolved them.
During the lab, a few issues occurred while executing commands in the terminal.

• Initially, OpenSSL commands failed because they were executed in PowerShell where the command formatting was incorrect. This was resolved by installing and using Git Bash.

• A password verification error occurred during encryption because the password entered during verification did not match the original password. Re-running the command and entering the same password resolved the issue.

---

## Artifacts
List the files generated during this lab.
- screenshots stored in assets/

---

CVI PKI Career Pathway — Foundations Phase
