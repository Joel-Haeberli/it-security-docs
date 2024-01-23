tags: #auth 

# ASREP Roasting

links: [[620 SPA TOC - Kerberos|SPA TOC - Kerberos]] - [[themes/000 Index|Index]]

---

## ASREP Roasting

- Attack to extract account credential hashes from AD for offline cracking
- Attacker only interacts with KDC (DC)
- Attack: With Pre-Authentication disabled for a user, anyone can request a TGT for this user
	- The TGT is encrypted with the users password hash -> brute force, same situation as [[Kerberoasting]]
- Requirements
	- Pre-authentication is disabled for the target account
	- Connection to KDC

### Countermeasures

- Do not disable pre-authentication
- Strong password policy
- Train users
- Restrict privileges
- Actively check for ASREP-roastable accounts
- Implement monitoring to look for TGT requests for ASREP-roastable accounts

---
links: [[620 SPA TOC - Kerberos|SPA TOC - Kerberos]] - [[themes/000 Index|Index]]