tags: #PKCS 

# PKCS\#11

links: [[615 SPA TOC - YubiKey|SPA TOC - YubiKey]] - [[themes/000 Index|Index]]

---

See all relevant PKCS standards [[PKCS|here]].

The **PKCS\#11** (Cryptoki) standard defines a platform-independent API to access cryptographic tokens, such as hardware security modules (HSM).

Many applications support the standard:

- Firefox
- Thunderbird
- OpenSSH
- OpenVPN
- Oracle and IBM DB2 Databases (for transparent data encryption)
- ...

## Stack

- Application with PKCS#11 support. Note that most token come with their own PKCS#11 library.
- The PKCS#11 library is normally supporting a certain app on a certain token.
- PC/SC is a generic «Personal Computer/Smart Card» layer supporting the communication via APDU (Application Protocol Data Unit) commands.
- Generally a driver is used for the low level communication (USB, NFC, Bluetooth, ...) to the token.
- The token needs an app installed, that supports the commands of the PKCS#11 library. Normally app and PKCS#11 library is a matching pair.

![[Pasted image 20240124112418.png]]

## APDU Commands

APDU (Application Protocol Data Unit) commands are used in smart card technologies. They facilitate communication between a smart card and an external device, like a card reader. These commands are essential in applications such as EMV (Europay, MasterCard, and Visa) chip-based credit cards, SIM cards in mobile phones, identity verification systems, and secure access control.

![[Pasted image 20240124124108.png]]

- **Yellow**: Header
- **Green**: Body
- **CLA**: Class
- **INS**: Instruction
- **P1-P2**: Parameter 1 and 2
- **Lc**: Length of the data in bytes
- **Data**: Command data or Response data
- **Le**: Maximum number of response bytes expected
- **SW1-SW2**: Command processing status

## Protocol

The ISO/IEC 7816 standard is commonly used across various smart cards like SIM cards, credit cards, smart identity cards, and devices like YubiKey. This standard defines the physical characteristics, communication protocols, and APDU commands for interaction with smart cards.

## Intention

The primary intention of the PKCS#11 API is to provide a standard interface for applications to interact with cryptographic tokens. The API allows applications to perform cryptographic operations like encryption, decryption, digital signing, and key management without needing to understand the details of the underlying hardware.

## Key export

Generally, extracting keys from a smart card or HSM is designed to be difficult or impossible, for security reasons. These devices are meant to securely generate, store, and handle cryptographic keys. However, some HSMs or smart cards may allow the export of certain keys under specific conditions, often wrapped with another key and subject to stringent security policies.

---
links: [[615 SPA TOC - YubiKey|SPA TOC - YubiKey]] - [[themes/000 Index|Index]]