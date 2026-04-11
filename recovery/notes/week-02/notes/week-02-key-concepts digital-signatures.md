Why verification succeeds before tampering?

Verification succeeds before tampering because the digital signature matches the exact file that was originally signed. When the verification command was run, OpenSSL calculated a hash of the file and compared to the signed hash. Since the file has not changed, the hashes match and the signature verifies successfully. 

Why verification fails after modification?

The digital signature is tied to the original hash that was created when the file was signed. Once the file is changed, the newly calculated hash no longer matches the signed hash. This caused the signature verification to fail.

Why digital signatures require both hashing and asymmetric cryptography?

Digital signatures require hashing and asymmetric cryptography because each part serves a different purpose. Hashing creates a unique fingerprint of the file to detect any changes. Asymmetric cryptography is then used to sign that hash with a private key and verify it with a public key. 

How this relates to certificate signing in PKI?

This process is the same when Certificate Authorities sign digital certificates in PKI. The certificate data is first hashed and then signed using the CA’s private key. The system that receive the certificate will use the CA’s public key to verify the signature. If the verification succeeds, the certificate is trusted. This process provides both integrity and authenticity.
