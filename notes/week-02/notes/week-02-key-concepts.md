1. Why the encrypted file is unreadable?
   
The encrypted file is unreadable because Advanced Encryption Standard (AES) transforms plaintext into ciphertext using a cryptographic algorithm and a secret key. During this process, the data becomes scrambled and appears as random characters. Without the correct key, the contents cannot be interpreted or viewed. This symmetric encryption process supports the CIA triad by protecting confidentiality, ensuring that only authorized users with the correct key can access the original data.

2. What would happen if the wrong password were used?

If the wrong password is used during decryption, the system will either fail to decrypt the file or produce corrupted and meaningless output. This happens because the password is used to produce the encryption key, and an incorrect key cannot reverse the encryption process.

3. What security property does symmetric encryption provide?

Symmetric encryption primarily provides confidentiality. It protects data by ensuring that only individuals who are in possession of the correct key can access the original information. Symmetric encryption is very fast, which is why it’s used to protect large amounts of data . 

4. Why TLS uses symmetric encryption for data transfer?

TLS uses Symmetric encryption for data transfer because it is  fast and efficient, allowing systems to securely encrypt large volumes of data during communication. While asymmetric encryption is used during the handshake to securely exchange keys, symmetric encryption provides high-speed encryption for the actual session.



