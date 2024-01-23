tags: #auth 

# Kerberoasting

links: [[620 SPA TOC - Kerberos|SPA TOC - Kerberos]] - [[themes/000 Index|Index]]

---

## Kerberoasting

- Attack to extract service account credential hashes from AD for offline cracking
- Attacker only interacts with the KDC (DC), not with services

![[kerberos-22.png]]

- Requirements for an attacker to request an ST
	- Valid domain account (control over a user's machine or knowing a user's password)
		- The user does not need permissions for the target service (any account can request STs for any service)
	- Connection to KDC
	- SPN of target services (Attacker can query AD to find SPNs of services)
- Possible encryption algorithms used for ticket encryption
	- DES (not supported since 2008 R2 / Windows 7)
	- RC4 (MD4 for key derivation) <- best option for brute force
	- AES128 (PBKDF2 for key derivation)
	- AES256 (PBKDF2 for key derivation)
- Used algorithm depends on domain level, config, account type etc.
- KDC will always choose the highest mutually supported algorithm
- When requesting a ticket, the client specifies which algorithms it supports -> **Downgrade attack is possible** (DC older than WinServer 2019)
	- Downgrade attack even works, if the target account is configured to use AES only
	- With WinServer 2019, DCs ignore the clients cipher proposals

### Countermeasures

- Long passwords
- Restrict privileges of service account
- Only configure SPNs if required
- Use group managed service accounts (GMSA), that offer automatic password management
- Configure strong encryption: No DES / RC4 (relevant in WinServer 2019 and higher)
- Implement monitoring and check for excessive ticket requesting, especially with RC4

---
links: [[620 SPA TOC - Kerberos|SPA TOC - Kerberos]] - [[themes/000 Index|Index]]