tags: #cryptocurrency #scaling

# SIGHASH Types

links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]

---

**Challenge**:

The problem with current signature verification process (OP_CHECKSIG) is that the signature is verified with the public key from the stack which means that, for each spending transaction only one key is able to sign the entire transaction by default. This denies collaborative creation of transactions. The SIGHASH Type works against this by allowing to specify another way of signing transactions. This type specifies which parts of the transaction are removed before the transaction is signed.

This mainly concerns in- and outputs. Fields not in in- or outputs are never removed (locktime and version fields). Input scripts are always removed. The removed parts are unsigned and can thus be changed by other participants. This gives us the ability to collaboratively build transactions.

SIGHASH Types:

- SIGHASH_ALL (default): Sings all inputs and outputs $\rightarrow$ this will lead to the behavior we had without the SIGHASH types $\rightarrow$ This is also the reason this is the default (remember [[Forks#Soft Forks|Soft Forks]]?)
- SIGHASH_NONE: Signs all inputs
- SIGHASH_SINGLE: Signs all inputs and the output of the current input
- SIGHASH_ANYONECANPAY: This means that only the current input will be signed.

Combining SIGHASH_ALL, SIGHASH_NONE and SIGHASH_SINGLE with SIGHASH_ANYONECANPAY results in additional types:

- ALL | ANYONECANPAY: Current input and all outputs are signed (crowdfunding)
- NONE | ANYONECANPAY: Current input but no outputs are signed
- SINGLE | ANYONECANPAY: Current input and the corresponding output is signed.

Using SIGHASH types for signature creation leads to following process (simplified):

1. Copy transaction
2. delete all fields according to the SIGHASH type
3. serialize remaining
4. append SIGHASH type
5. hash
6. create signature of the hash

With this we are now able to partially sign transactions if we want to. This makes the transactions more flexible and allows other usecases.

---
links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]