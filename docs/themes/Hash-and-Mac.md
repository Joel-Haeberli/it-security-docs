tags: #symmetric #MAC #hash

# Hash-and-Mac

links: [[105 AC1 TOC - Random Oracle & Applications|AC1 TOC - Random Oracle & Applications]] - [[300 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]

---

## General Construction

- use a fixed-length [[MAC]] for $l(n)$-bit messages and a collision-resistant [[Hash Functions|hash function]] with $l(n)$-bit output length
- Then we can authenticate an arbitrary-length message $m$ by using the MAC to authenticate the *hash* of $m$
- This is secure because the MAC ensures that the attacker cannot authenticate any new hash value, while collision resistance ensures that the attacker will be unable to find any new message that hashes to a previously used hash value

**Formal description**

- $Mac$:  takes as input the keys $k$ and $s$ and a message $m$, outputs $t \leftarrow Mac_k(H^s(m))$
- $Vrfy$: takes as input the keys $k$ and $s$, a message $m$ and a tag $t$, output 1 iff $Vrfy_k(H^s(m), t) \stackrel{?}{=} 1$

**Drawbacks**

- see [[Cryptographic MACs#Drawback of Hash-and-MAC Constructions|Drawback of Hash-and-MAC Constructions]]

## HMAC

- see [[Cryptographic MACs#HMAC (Hash-based Message Authentication Code)|HMAC]]

## Attacks

### Length-Extension Attack

- see article on [Github](https://github.com/marcelo140/length-extension)

The length-extension attack allows an attacker to extend the length of a given hash value, without knowing the original message or the secret key. This is a problematic when using the hash as MAC with construction $H(secret \parallel message)$.
By appending additional data to the hash output and calculating a new MAC, the attacker can generate valid MACs for extended messages, potentially leading to unauthorized access or forgery (without knowing the secret).

---
links: [[105 AC1 TOC - Random Oracle & Applications|AC1 TOC - Random Oracle & Applications]] - [[300 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]