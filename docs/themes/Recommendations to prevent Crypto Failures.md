tags: #web-security #crypto-failures

# Recommendations to prevent Crypto Failures

links: [[504 WS TOC - Crypto Failures|WS TOC - Crypto Failures]] - [[themes/000 Index|Index]]

---

There are a lot of recommendations that can be considered to prevent cryptographic failures.

## Rely on strong cryptographic algorithms only

- Do not create your own algorithms
- use approved public algorithms as: AES, RSA, SHA-512, and so on (see [[100 AC1 MOC|symmetric]] and [[200 AC2 MOC|asymmetric]] cryptography)
- Algorithms used should have been designed involving crypto specialists
- Look for [FIPS 140-3](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.140-3.pdf) certified algorithms

## Handle keys with extra care

- Generate keys offline
- Store private keys with *extreme* care
- Store private keys encrypted using a passphrase or inside a password manager
- Do not let users access the key directly (create a REST API for functions requiring the key)
- Do not store the key for decrypting the private key where users can read it.
- Store passwords hashed and salted 

## Protect Infrastructure Credentials

- Use least privilege file system permissions and controls configurations
- Encrypt credentials

## Only store the sensitive data you need

- There is no need to store Credit Card Numbers
- Data you don't have cannot be stolen

## Cryptographically strong Randomness

- Random generators should be used
- Enough [[Entropy]]

## Ensure data integrity and authenticity

- Use cryptographic cipher modes that offer confidentiality and authenticity

## Lifecycle

- Maintain a lifecycle process specifying when and how keys are replaced and rolled over

---
links: [[504 WS TOC - Crypto Failures|WS TOC - Crypto Failures]] - [[themes/000 Index|Index]]