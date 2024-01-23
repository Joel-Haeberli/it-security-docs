tags: #auth 

# Passkey

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

Based on FIDO standards, passkeys are a replacement for passwords that provide faster, easier, and more secure sign-ins to websites and apps across a user’s devices. Unlike passwords, passkeys are always strong and phishing-resistant.​ Find more in the [FAQ](https://fidoalliance.org/passkeys/#faqs).

Passkeys are just [[FIDO]] credentials. Nothing new. 

- Passkeys is an authenticator for «Discoverable Credentials» based on the WebAuthn/FIDO2 standard. «Passkey support» is «WebAuthn support».
- Many Passkeys implementations (Android, iOS, Mac OSX, Microsoft) store the private keys on in password manager (i.e. on the cloud profile). These keys are not attested (and not in hardware).

Discoverable credentials means that the credentials are stored on the authenticator (and "accessible" via meta data). They enable a login flow where you don't event enter a user name (because your auth token knows that you have an account for the provided domain).

Example with Github (no username needed):

![[passkey.png]]

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]