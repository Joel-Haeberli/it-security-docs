tags: #auth 

# One Time Password

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## One Time Password

![[OTP.png]]

### HMAC-based one-time password (HOTP)

- Client and server need a constant shared secret
- Synchronized counter on client and server which increments with each authentication attempt
![[HOTP.png]]
![[HOTP2.png]]

### Time-based one-time password (TOTP)

Same as HOTP but $C_T$ is used instead of a counter

![[TOTP.png]]

### Yubico OTP

- Requires Yubikey
- At manufacturing the Yubikey an AES key is generated and stored on the Yubikey and the authentication server of Yubico or service's own authentication server
- To generate an OTP ID, timestamp, counter, session usage counter and random string are used and encrypted with the AES key
- Authentication server can then verify the OTP with the AES key
- Authentication server also checks the counter to avoid replay attacks

### Caveats of OTP

- Beware of replay attacks -> counter
- Static OTP (e.g. SMS) aren't time or challenge based and have longer window of vulnerability
- Does not prevent MITM
- Susceptible against phishing attacks
- [[Authentication#Dynamic Linking|Dynamic Linking]] is not possible, OTP is too short to contain information about transaction

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]