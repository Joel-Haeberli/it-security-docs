tags: #web-security #broken-authentication

# Protection against Broken Authentication

links: [[503 WS TOC - Broken Authentication]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---

There are tons of measures that can be implemented in order to be secure:

- Prohibit brute force
	- set a maximum number of retries to login
- Authentication relies on secure communication and credential storage
- TLS should be used on all pages authenticated pages (just use it everywhere and give eavesdropper no chances)
- Store passwords hashed, using [[Password Based Key Derivation Function (PBKDF)]]
- Use well known session management and SSO solutions. Don't build your own. It's hard and you will most probably fuck it up
- Use one authentication mechanism and not more.
- Make the mechanism as easy as possible and as complex as needed.
- Force TLS (especially on login etc.)
- Destroy sessions and other relevant tokens on logout
- Expire relevant tokens
- Do not ask users for confirmation when it comes to session termination (but inform them).
- Do not use spoofable tokens as authentication (everything an attacker can see when eavesdropping should not be used to authenticate users. Such as IP, DNS, HTTP Referrer, etc.)
- Do not send passwords by email
- Use 2FA
- Specify a minimum complexity for passwords. The [NIST recommendations are a good starting point](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63-3.pdf)


---
links: [[503 WS TOC - Broken Authentication]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]