tags: #distributed-systems-security  #blockchain

# Bitcoin Terms

links: [[400 DSS MOC|DSS MOC]] - [[themes/000 Index|Index]]

---

- **Collision resistance**: if its infeasible to find a collision for a hash function (except with negligible probability) $\rightarrow$ not collision impossibility (pigeonhole principle, if $s$ is size of hash space, try $s + 1$ inputs)
- **Pre-image resistance**: $H$ is one-way, for a given output $y$ it is infeasible to find an input $x$ with $h(x) = y$ except with negligible probability
- **Second pre-image resistance**: We have $x$ and cannot find a $x'$ which results to the same Hash $y$ for both $x$ and $x'$
- **Unforgeability**: an adversary should not be able to sign a message as Sender $S$ even if he has access to many signed messages by $S$ (unforgeability game)
- **Zooko's Triangle**: all known naming systems have at most two of the given three properties: *Secure*, *Memorable*, *Decentralized*
	- Bitcoin has properties *Secure* and *Decentralized*: public keys are not memorable but secure and everybodyy can create keypairs without permission from anyone
- **Bitcoin wallet**: collection of key pairs
- **Bitcoin address**: hash of a public key (plus checksum/encoding) $\rightarrow$ 160bits

---
links: [[400 DSS MOC|DSS MOC]] - [[themes/000 Index|Index]]