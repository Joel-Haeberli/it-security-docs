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

### Challenge Response

By using asymmetric crypto we can authenticate users with a challenge. The relying party (server) send a challenge initially to register. This challenge is signed by the clients private key and the client sends back their public key + signed challenge. From now on the relying party can send challenges and the client can sign them with the privat key. If the signature matches with the public key on the server the client is logged in.

### Attestation

Attestation is used to credibly demonstrate the origin or type of authenticator and validate the integrity of the information it produces. The Android KeyStore can attest keys by using a Google root certificate (which never leaves the TEE). By doing that and providing the X509 certificate chain to the relying party it can be sure that the key is stored on hardware. (The RP needs to configure the public Google root keys for that of course) This is similar for Android Protected Confirmation where we can attest that a specific message was shown on a Trusted User Interface.

### FIDO2

- **WebAuthn**
	- Web Authentication is the protocol between the client (browser) and the relying party (server)
	- Backwards compatible with legacy FIDO Universal 2nd Factor (U2F)
- CTAP
	- Client to Authenticator Protocol is based on U2F
	- Supports USB, NFC, Bluetooth
	- Using Bluetooth you can use your Smartphone to store the private keys on it's secure hardware. 

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