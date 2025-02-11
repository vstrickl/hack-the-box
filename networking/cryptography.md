# Cryptography

## Digital key processes used for encryption

### Symmetric Encryption
- known as secret key encryption
- a method that uses the same key to encrypt and decrypt the data
- Examples
    - Advanced Encryption Standard (AES) (considered the most secure)
    - Data Encryption Standard (DES)
- used to encrypt large amounts of data such as
    - Files on a hard drive
    - data sent over a network

#### Critical Actions
- distribution
- storage
- key exchange

### Asymmetric Encryption
- known as public-key encryption
- Uses two different keys
    - **public key**: used to encrypt the data
    - **private key**: used to decrypt the data
- Examples:
    - Rivest–Shamir–Adleman (RSA)
    - Pretty Good Privacy (PGP)
    - Elliptic Curve Cryptography (ECC)
- Applications that use it:
    - E-Signatures
    - SSL/TLS
    - VPNs
    - SSH
    - PKI
    - Cloud
- With the public key
    - opens up the possibility of authentication with digital signatures

## Data Encryption Standard (DES)
- a symmetric-key block cipher
- works as a combination of the one-time pad, permutation, and substitution ciphers applied to bit sequences
- uses the same key in both encrypting and decrypting data
- is 64 bits, with 8 bits used as a checksum
    - people always speaks of a key length of 56 bits when referring to DES
    - each 64-bit block of plaintext is encrypted to a 64-bit block of ciphertext to prevent the danger from frequency analysis
- **Triple DES / 3DES**: encrypts data more securely
    - is an extension of DES
    - considered more secure than the original DES 
    - provides greater security using three rounds of encryption
    - the three keys for encryption:
        - **1st key**: used to encrypt the data
        - **2nd key**: used to decrypt the data
        - **3rd key**: used to encrypt the data again

## Advanced Encryption Standard (AES)
- provides higher security
- uses longer key lengths
- the most widely used symmetric encryption technology
- Uses either of the following key lengths to encrypt and decrypt data:
    - 128-bit (AES-128)
    - 192-bit (AES-192)
    - 256-bit (AES-256)
- Is faster at encrypting and decrypting than DES because it:
    - has a more efficient algorithm structure
    - can be applied to multiple data blocks at once
- Applications & Protocols:
    - WLAN IEEE 802.11i
    - IPsec
    - SSH
    - VoIP
    - PGP
    - OpenSSL

## Cipher Modes
- the process by which a block cipher algorithm encrypts a plaintext message
- **block cipher algorithm**: encrypts data
    - uses fixed-size blocks of data (usually 64 or 128 bits)
- defines how these blocks are processed and combined to encrypt a message of any length

| Cipher Mode                      | Description |
|----------------------------------|-------------|
| Electronic Code Book (ECB) mode  | ECB mode is generally not recommended for use due to its susceptibility to certain types of attacks. Furthermore, it does not hide data patterns efficiently. As a result, statistical analysis can reveal elements of clear-text messages, for example, in web applications. |
| Cipher Block Chaining (CBC) mode | CBC mode is generally used to encrypt messages like disk encryption and e-mail communication. This is the default mode for AES and is also used in software like TrueCrypt, VeraCrypt, TLS, and SSL. |
| Cipher Feedback (CFB) mode       | CFB mode is well suited for real-time encryption of a data stream, e.g., network communication encryption or encryption/decryption of files in transit like Public-Key Cryptography Standards (PKCS) and Microsoft's BitLocker. |
| Output Feedback (OFB) mode       | OFB mode is also used to encrypt a data stream, e.g., to encrypt real-time communication. However, this mode is considered better for the data stream because of how the key stream is generated. We can find this mode in PKCS but also in the SSH protocol. |
| Counter (CTR) mode               | CTR mode encrypts real-time data streams AES uses, e.g., network communication, disk encryption, and other real-time scenarios where data is processed. An example of this would be IPsec or Microsoft's BitLocker. |
| Galois/Counter (GCM) mode        | GCM is used in cases where confidentiality and integrity need to be protected together, such as wireless communications, VPNs, and other secure communication protocols. |
