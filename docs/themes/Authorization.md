tags: #auth 

# Authorization

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## Authorization

- specifying access rights / privileges to resources
- related to access control / policies
- bundling authentication and authorization is a **bad idea**
	- e.g. certificate contains the specific roles of the user

![[auth-vs-auth.png]]

**Authentication assurance / Level of Assurance (LoA)**: amount of certainty with which a claim to an identity can be trusted to be accurate

**Identity assurance**: level of identity assurance at initial verification process to ensure that the user is actually this person (email, address, ID, passport, ...)
![[LoA.png]]
![[assurance-matrix.png]]
![[quality-of-authentication.png]]

### Password

- Knowledge factor
- Considered insecure because of bad practices (low entropy, written down on paper, never changed, same pw for multiple services)
- **Online attack**: e.g. brute forcing through log in form (systems impose time-outs)
- **Offline attack**: Attacker has any number of attempts (dictionary attack or rainbow-table)

### Password strength

![[password-strength.png]]

### Password entropy

![[Pasted image 20240123133336.png]]

### Measurements against offline attacks

- Enforce password policy
- Only use passwords in protected channels -> TLS
- Salting with minimum  32 bits random data
- Protect password hashes against read access
- Use good hash functions

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]