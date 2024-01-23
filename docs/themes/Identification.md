tags: #auth 

# Identification

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## Identification

*Identity*: set of attributes that uniquely describes a person within a given context (email, address, ...)

*Identification*: process of ascertaining the identity of a person (passport, ID, ...)

*Goal*: uniquely identify the person and confirm attributes of identity

![[partial-identities.png]]

**Authentication**
- It's the proof of an asserted property
- If someone claims to be the owner of an email address then authentication is making sure this person actually owns this email address.
- Can rely on third part

**Authentication factors**
- Knowledge factor: Something the user knows (password, PIN, ...)
- Ownership factor: Something the user has (Security token, smart card, ...)
- Inherence factor: Something the user is or does (fingerprint, retinal pattern, ...)

**Types of authentication**
- Single-factor auth: Weakest level, only single factor is used
- Two-factor auth(2FA): Using 2 factors
- Multi-factor auth: Using two or more authentication factors
- **Strong auth**:
	- Multi-factor auth
	- Factors must be mutually independent (compromise of one factor does not lead to compromise of other factors)
	- At least one factor must be "non-reusable and non-replicable" (exception: inherence factor -> fingerprint etc.)
	- Can't be stolen off the internet

**Dynamic Linking**
Security requirement under EU law for electronic payments that ties the authentication code to the transaction amount and the payee's identity to prevent replay attack

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]