tags: #cryptocurrency #protocol

# Upgrades

links: [[405 DSS TOC - Evolving the Protocol|DSS TOC - Evolving the Protocol]] - [[themes/000 Index|Index]]

---

This section explains three significant upgrades to the Bitcoin protocol.

## How Bitcoin Upgrades

- **Early Upgrades (BIP34)**
	- the version field in the block header was used
	- miners signal readiness by producing block with a higher version number
	- if 95% of the previous 1000 blocks have the higher number, the new rules are activated
- **Upgrades Today (BIP9)**
	- today, the version field is interpreted as a bitfield
	- multiple protocol updates can happen in parallel, with each assigned one bit
	- Miners signal readiness by setting the bits for the protocol features they support
	- after some grace period, the bits can be reused for new upgrades

## Pay-To-Script-Hash (P2SH, 2012)

**Problem**:

Assume you want an amount of coins only spendable if some complex conditions are met. These conditions are specified by the sender of the transaction as part of the [[Bitcoin Scripts#Lock|Lock Script]]. Under normal circumstances this complexity shall be hidden from the sender. So it should be the responsibility of the recipient to specify the details of the [[Bitcoin Scripts#Lock|Lock Script]].

**Solution**:

The recipient hands the sender the hash of the lock script. The sender writes that hash into the output. When the recipient wants to spend the output he adds the actual [[Bitcoin Scripts#Lock|Lock Script]] (the *redeem script*) to his [[Bitcoin Scripts#Unlock|Unlock Script]]. The node software then ensures that the hash of the *redeem script* matches the hash in the output and the [[Bitcoin Scripts#Unlock|Unlock Script]] automatically unlocks the *redeem script*

![redeem-script](redeem_script.png)
The first validation is spent, when the sender sends the coin to the recipient and the second validation is done, if the recipient wants to eventually spend the coin.

## Segregated Witness (SegWit, 2017)

Increases block capacity and improves scalability by separating (or 'segregating') the digital signature (the 'witness') from the transaction data. This reduces the size of each transaction, allowing more transactions to fit in a block, and also solves transaction malleability, a security issue where slight changes to transaction data could change the transaction ID.

## Taproot (2021)

Introduces Schnorr signatures, replacing the existing ECDSA signatures. This change enables more efficient and private transactions, particularly benefiting complex transactions like those using smart contracts, by making them indistinguishable from regular transactions in terms of on-chain footprint. It enhances both privacy and efficiency in the Bitcoin network.

---
links: [[405 DSS TOC - Evolving the Protocol|DSS TOC - Evolving the Protocol]] - [[themes/000 Index|Index]]