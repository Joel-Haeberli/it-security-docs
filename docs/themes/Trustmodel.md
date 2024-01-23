tags: #SPA #certificates
 
# Trustmodel

links: [[611 SPA TOC - Certificates and PKI|SPA TOC - Certificates and PKI]] - [[themes/000 Index|Index]]

---

This topic was already handled in [[Trust Model|AC2 DPKI - Trust Model]]. In this document we will summarize the direct talking point from the module SPA.

## Certificate Trust Model

There are 3 different certificate trust models:

**Direct Trust**

The parties exchange their public keys directly. The trust is established by mapping the keys to an identity

**Web of Trust**

Each party can trust other parties. Decentralized trust model. Each public key can be signed by multiple parties.

**Hierarchical Trust**

Trustworthy authorities certify public keys. Each node only accept public keys by their trusted authorities.

## Web of Trust

![[web-of-trust 1.png]]

- The web of trust concept is used in OpenPGP-compatible systems (PGP, GnuPG, etc.)
- Decentralized trust model
- Relays on entities trust each other

**Problems**

- No efficient way to revoke a key
- Uncertain level of trust
- No automation

---
links: [[611 SPA TOC - Certificates and PKI|SPA TOC - Certificates and PKI]] - [[themes/000 Index|Index]]