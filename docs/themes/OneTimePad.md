tags: #symmetric 
links:  [[Topic 2 - Security]], [[030 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]

---
# OneTimePad

- the key is as long as the message (and also the ciphertext has the same length)
- the OneTimePad is only secure if used once (with a given key)

#### Using OneTimePad twice

Adversary can learn the $XOR$ of the two messages (where they differ):
$c \oplus c' = (m \oplus k)\oplus (m' \oplus k) = m \oplus m'$

#### Limitations of Perfect Secrecy

Any perfectly secret encryption scheme must have a key space that is at least as large as the message space: $|K|\geq|M|$

---

### Definitions

- XOR (bitwise exclusive-or): $a \oplus b$

---
links:  [[Topic 2 - Security]], [[030 Modern Cryptography MOC|Modern Cryptography MOC]] - [[themes/000 Index|Index]]