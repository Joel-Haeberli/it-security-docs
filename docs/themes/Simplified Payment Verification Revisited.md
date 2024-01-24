tags: #cryptocurrency #protocol

# Simplified Payment Verification Revisited

links: [[405 DSS TOC - Evolving the Protocol|DSS TOC - Evolving the Protocol]] - [[themes/000 Index|Index]]

---

The Activation of BIP-66 ([Bitcoin Improvement Proposal](https://bips.dev/)) lead to an unexpected behaviour after a not upgraded miner mined an invalid block (which was expected by the change). A significant percentage of upgraded miners did then build on top of the invalid block. This led to an invalid chain of 6 blocks, which eventually died. The problem is that during the time this chain existed, SPV Nodes were vulnerable because full nodes processing the wrong chain gave invalid [[Authenticated Data Structures#Merkle Proof|Merkle Proofs]] to the [[From IncentiveCoin to Bitcoin#SimplifiedPaymentVerificationCoin / SPVCoin|SPV Nodes]] which should not have been given to them. This made it visible that trusting miners (full nodes) was a bad idea. This showed that Bitcoin can only be secure if block verification is sufficiently easy.

---
links: [[405 DSS TOC - Evolving the Protocol|DSS TOC - Evolving the Protocol]] - [[themes/000 Index|Index]]