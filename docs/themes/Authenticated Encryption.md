tags: #symmetric #GCM #AEAD #encrypt-then-authenticate

# Authenticated Encryption

links: [[themes/Authenticated Encryption with Associated Data|Authenticated Encryption with Associated Data]] - [[107 AC1 TOC - Secure Channels|AC1 TOC - From Symmetric Encryption to Secure Channels]] - [[300 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]

---

Until now, we have considered how to obtain secrecy (using encryption) and integrity (using [[MAC|MACs]]) separately. The aim of *authenticated encryption* is to achieve both goals simultaneously.

> A private-key encryption scheme is an **authenticated encryption (AE) scheme** if it is CCA-Secure and unforgeable.

## Authenticated encryption with associated data

Often, a message $m$ requires both secrecy and integrity but various associated data (e.g. header information) sent along with the message requires integrity only. This schemes are called [[Authenticated Encryption with Associated Data|authenticated encryption with associated data (AEAD) schemes]].

## CCA Security vs. Authenticated Encryption

There is no reason to ever use a [[CCA-Security|CCA-secure]] scheme that is *not* also an authenticated encryption scheme, simply because we don't have any constructions of the former that are more efficient than constructions of the latter.

## Authenticated Encryption Schemes

**Encrypt-and-authenticate**

- encryption and message authentication are carried out independently
- even a strongly secure [[MAC]] does not guarantee any secrecy and so it is possible for the tag $t$ to leak information about $m$ to an eavesdropper

**Authenticate-then-encrypt**

- first compute tag, then encrypt message with tag
- there are two sources of potential decryption failure: the padding may be incorrect or the tag may not verify
- does not necessarily provide authenticated encryption

**Encrypt-then-authenticate**

- message is first encrypted an then a [[MAC]] is computed over the result
	- Encryption: $c \leftarrow Enc_{kE}(m)$ and $t \leftarrow Mac_{kM}(c)$, send pair $\langle c, t \rangle$
	- Decryption: if $Vrfy_{kM}(c, t) \neq 1$, output $Dec_{kE}(c)$
- with associated data $d$ simply change tag to: $t \leftarrow Mac_{kM}(d \| c)$

### The need for independent keys

> different instances of cryptographic primitives should always use independent keys!

## Standardized Schemes

### GCM (Galois Counter Mode)

- follows the *encrypt-then-authenticate* approach with [[Block Cipher#Counter (CTR) mode|CTR mode]] as the underlying encryption  scheme and [[Cryptographic MACs#GMAC (Galois Message Authentication Code)|GMAC]] as the underlying message authentication code.
- uses only one single key and the same IV for CTR-mode encryption and as the nonce for GMAC $\rightarrow$ Both these changes can be proven secure in GCM.
- a repeated IV would fail/drop secrecy and authenticity!

![[GCM.png]]

### CCM (Counter with CBC-MAC)

- follows the a*uthenticate-then-encrypt* approach with [[Block Cipher#Counter (CTR) mode|CTR mode]] as the underlying encryption scheme and [[MAC#CBC-MAC|CBC-MAC]] as the underlying message authentication code.
- uses only one single key but is proven secure
- **Drawback**: CCM is relatively slow and cannot be fully parallelized
- *Used in [[WPA2]]*

### ChaCha20-Poly1305

- relies on the *encrypt-then-authenticate* approach
- using the stream cipher ChaCha20 in [[Stream Cipher#Unsynchronized mode|unsynchronized mode]] and [[Cryptographic MACs#Poly1305|Poly1305]] as [[MAC]]

## Secure Communication Sessions

A **communication session** is a period of time during which the communicating parties maintain state. To ensure secure communication based on an AE scheme, the following attacks are still possible:

- **Re-ordering attack**: an attacker can swap the order of messages
- **Replay attack**: An attacker can replay a (valid) ciphertext $c$ sent previously by on of the parties.
- **Message-dropping attack**: An attacker may drop some of the messages sent between A and B.

$\rightarrow$ this attacks can be addressed using a **counter/ sequence number**

- **Reflection attack**: An attacker can take a ciphertext $c$ sent from A to B and send it back to A.

$\rightarrow$ this attack can be addressed using a **directionality bit**

---
links: [[themes/Authenticated Encryption with Associated Data|Authenticated Encryption with Associated Data]] - [[107 AC1 TOC - Secure Channels|AC1 TOC - From Symmetric Encryption to Secure Channels]] - [[300 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]
