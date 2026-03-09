# Week 01 Lab — Key Pair Generation

## Screenshot Evidence

If using OpenSSL:
1. Capture a screenshot showing:
  - The command used to generate the private key
  - The command used to extract the public key
2. Save it as:

**assets/screenshots/week-01/keypair-generation.png**

3. Embed the screenshot below:



**![Key Pair Generation](../../assets/screenshots/week-01/keypair-generation.png)**

If using a browser-based generator, capture the generated key pair screen (redact sensitive portions of the private key before committing).

---

## Key Identification
**Which file is the public key?**
128 Dec 17 2018 Public

**Which file is the private key?**
1675 Mar 8 14:38 private.key

---

## Key Properties
Briefly describe:
- What makes the public key safe to share
  The public key is safe to share becasue it is designed for encryption or signiture verification tool. It is created using a one-way mathamatical function which makes it difficult to reverse-engineer the privite key from it.
  
- What makes the private key sensitive
  The private key is sensitive becasue it is the component of the key pair that allows data to be decrypted and proves verification. It acts as the sole, irrevocable proof of ownership for digital assets, encrypted data, or identity. 

---

## Security Scenario
What would happen if someone obtained your private key?

Explain the risk in terms of:
  - Identity
  - Impersonation
  - Trust
    
The privite key is the sensetive component of the key pair. If someone obtains your private key, they can steal your digital identity, impersonate you in secure communications, and break the trust that PKI systems rely on. For example, a malcious actor could use the real owners idenity to decrept and access secure data or systems. If the privite key is compromised, then trust is broken and communications or signitures are no longer authentic. 


---

## Observations
Document three observations from this lab

### Observation 1
<!-- What did you notice about key generation? -->
During key generation, I observed that the system creates a pair of cryptographic keys at the same time: a public key and a private key. These keys are mathematically linked, but the private key cannot be easily accessed from the public key.


### Observation 2
<!-- What did you notice about key size or format? -->
Key generation produces keys with specific sizes, such as 2048 or 4096 bits, which determine the strength of the encryption.

### Observation 3
<!-- What did you notice about how the keys differ? -->
I observed that the private key is longer and more sensitive (RSA), and it is stored securely on the system. The public key can be distributed openly, appearing inside a digital certificate that websites or systems share during secure communications.

---

## Reflection
In 3–5 sentences, explain:

Why must the private key remain secret in a PKI system?
PKI relies heavily on trust between users, systems, and certificate authorities. If a private key is compromised, that trust is broken. In other words, the private key is the sensative component of the key pair, falling into the wrong hands could result in attackers compromising a system's confidentiality, integrity and availability.

Focus on how identity is tied to possession of the private key.
Identity is tied to possession of the private key because only the legitimate owner should have access to it. A digital certificate contains identifying information that helps to prove identity. When a system proves it has the private key, it proves ownership of the certificate and the identity associated with it.
