tags: #symmetric
links:  [[030 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]

---
# Hash Functions

> Hash functions are simply functions that take inputs of some length and *compress* them into short, fixed-length outputs.

Hash functions can be viewed as lying between the worlds of private- and public-key cryptography, because they have important applications in both settings.

### Collision Resistance

- a function $H$ is *collision resistant* if it is infeasible for any probabilistic polynomial-time algorithm to find a collision in $H$.
- The domain of a hash function is normally larger than their range $\rightarrow$ in this case collisions *must exist*, but such collisions should be hard to find.

### Keyed hash functions

- **Keyed hash functions**: $H$ takes as input a key $s$ and a string $x$ and outputs a string $\rightarrow$ the key is generally not kept secret!
- Cryptographic hash functions used in practice are generally *unkeyed* and have a fixed output length

### Weaker Notions of Security

**Second-preimage resistance**

We have $x$ and cannot find a $x'$ wich results to the same Hash $y$ for both $x$ and $x'$

**Preimage resistance**

$H$ is one-way, if we have $y$ ($y = H(x)$) we cannot go back to find a $x'$ to compute $y$

### Merkle-Damgård Transform

- maps inputs of arbitrary length to outputs of length $n$

![[merkle_damgard_transform.png]]

### Hash-and-MAC

- use a fixed-length MAC for $l(n)$-bit messages and a collision-resistant hash function with $l(n)$-bit output length
- Then we can authenticate an arbitrary-length message $m$ by using the MAC to authenticate the *hash* of $m$
- This is secure because the MAC ensures that the attacker cannot authenticate any new hash value, while collision resistance ensures that the attacker will be unable to find any new message that hashes to a previously used hash value

**Formal description**

- $Mac$:  takes as input the keys $k$ and $s$ and a message $m$, outputs $t \leftarrow Mac_k(H^s(m))$
- $Vrfy$: takes as inputthe keys $k$ and $s$, a message $m$ and a tag $t$, output 1 iff $Vrfy_k(H^s(m), t) \stackrel{?}{=} 1$

**Drawbacks**

- implementing two cryptography primitives: a hash function and a block cipher (for MAC)
- mismatch between the output length of hash functions and the block length of block ciphers $\rightarrow$ AES with 128-bit block, but hash has to be at least 256 bits for a meaningful collision resistance

### HMAC

- uses the Merkle-Damgård transform to compress arbitrary-length messages
- there is an "inner" and an "outer" hash evaluation with some fixed constants (ipad/opad) 

![[hmac.png]]


---
links:  [[030 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]