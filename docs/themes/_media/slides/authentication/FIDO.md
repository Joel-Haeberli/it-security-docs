tags: #auth 

# FIDO

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## FIDO

### FIDO Goals

- Getting rid of passwords
- Using asymmetric crypto
- Having different authentication facets
- Decoupling authenticator and authentication protocol
- Supporting different kinds of authenticators

### FIDO2

- **WebAuthn**
	- Web Authentication is the protocol between the client (browser) and the relying party (server)
	- Backwards compatible with legacy FIDO Universal 2nd Factor (U2F)
- CTAP
	- Client to Authenticator Protocol is based on U2F

![[yubikey.png]]

### WebAuthn Registration Flow

![[webauthn.png]]

RP Info: Relying Party Info (e.g. domain name, etc.)
Attestation: Cryptographic statement that verifies a key pair was generated y a legitimate device (often includes certificates)


### WebAuthn Authentication Flow

![[webauthn2.png]]

User verification: PIN, fingerprint, hw key (yubikey)
RP ID: Relying Party Identifier

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]