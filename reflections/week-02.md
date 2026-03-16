# Week 2 Reflection


1. What did you learn this week?

This week I learned how hashing, symmetric encryption, and digital signatures work together to secure data. Hashing creates a unique fingerprint of a file so any small change can be detected. Symmetric encryption protects confidentiality by converting plaintext into unreadable ciphertext using a shared key. Digital signatures combine hashing and asymmetric cryptography to verify authenticity and ensure the data has not been modified.

2. What concept was most challenging?
   
The most challenging concept was understanding how digital signatures combine multiple cryptographic processes. It took some time to see how the hash of a file is signed with a private key and then verified using the public key. At first the steps felt separate, but I realized they work together. Once I practiced it in OpenSSL, the relationship between hashing and signatures made more sense.

3. Where does this concept appear in real-world systems?

These concepts appear everywhere in modern security systems. Hashing is used to verify file integrity and protect stored passwords. Symmetric encryption is used by TLS to securely transfer data across the internet because it is fast and efficient. Digital signatures are used in PKI systems to sign certificates, verify software updates, and confirm the identity of websites.
   
4. How would you explain this topic to a non-technical audience?

I would explain it as a way to keep information private and trustworthy when it moves across the internet. Encryption locks the information so only the right person can read it. Hashing is like a digital fingerprint that shows if something was changed. Digital signatures prove who sent the information and confirm that it has not been altered. 
   
5. What questions remain?
   
I would like to confirm my folder structure and the notes section. Do we provide one note for the lesson and three seperate notes for each lab?

---

## Professional Growth Check

- Did you document clearly? Yes
- Did you use structured formatting? 90% -I creted a Hashing folder an I am unable to remove if from my week 2 repo. 
- Was your commit message meaningful? Yes. 
