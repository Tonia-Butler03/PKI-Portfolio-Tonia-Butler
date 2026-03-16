1. Why the Hash Changed After a Small Modification

The hash changed because cryptographic hashing reacts to even the smallest change in the data. When the file was modified, the SHA-256 algorithm generated a completely different hash value. This process helps systems detect when data has been altered.

2. Why Hashing Does NOT Provide Confidentiality

Hashing does not provide confidentiality because it does not hide or encrypt the original data. The purpose of hashing is to create a unique fingerprint of the data for verification. The file itself can still be read unless encryption is used.

3. What Security Property Hashing Provides

Hashing provides the security property of data integrity. It allows systems to confirm that data has not been changed or tampered with. If the hash value changes, it means the contents of the file were altered.

4. Where Hashing Is Used in PKI Systems

Hashing is used in PKI systems for things like certificate signatures, file verification, and code signing. Hashing is also used to confirm the integrity of files and software before they are trusted or installed.

