tags: #auth 

# Passwords

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## Passwords

- Knowledge factor
- Considered insecure because of bad practices (low entropy, written down on paper, never changed, same pw for multiple services)
- **Online attack**: e.g. brute forcing through log in form (systems impose time-outs)
- **Offline attack**: Attacker has any number of attempts (dictionary attack or rainbow-table)

### Password strength

![[password-strength.png]]

### Password entropy

![[passwords.png]]

### Measurements against offline attacks

- Enforce password policy
- Only use passwords in protected channels -> TLS
- Salting with minimum  32 bits random data
- Protect password hashes against read access
- Use good hash functions

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]