# Week 01 — Key Concepts

## PKI Explanation (3–5 Sentences)

Write a clear explanation of what PKI is in your own words.

Focus on:

- The problem PKI solves
  
Public Key Infrastructure (PKI) enables secure communication, identity verification, and data protection on networks such as the internet. It ensures authentication, uses encryption to protect data, and maintains data integrity during transmission. PKI is a foundational component of modern cybersecurity systems.

- The role of keys
  
keys are the cryptographic tools used to encrypt, decrypt, and verify information. They ensure that communication over networks like HTTPS websites are secure, private, and authentic. PKI relies on cryptography, which uses two related keys Public key for encyrption and verifing certificates and Privite keys that decrept data and cretes signitures. 

- The role of certificates

Digital certificates are electronic credentials used in PKI to verify the identity of websites, users, or devices. They contain a public key and identifying information and are issued by trusted Certificate Authorities. Certificates enable encrypted communication through TLS and establish trust on the internet.
  
- How trust is established
Trust in Public Key Infrastructure (PKI) is established through Certificate Authorities (CAs) that verify identities and issue digital certificates. These certificates create a chain of trust, linking a website or user’s certificate back to a trusted root certificate stored in a browser or operating system. The browser then uses cryptographic verification and digital signatures to confirm the certificate is valid and that secure communication can occur.
