tags: #cryptocurrency #protocol

# Upgrades

links: [[405 DSS TOC - Evolving the Protocol|DSS TOC - Evolving the Protocol]] - [[themes/000 Index|Index]]

---

This section explains three significant upgrades to the Bitcoin protocol.

## Pay-To-Script-Hash (P2SH, 2012)

**Problem**:

Assume you want an amount of coins only spendable if some complex conditions are met. These conditions are specified by the sender of the transaction as part of the [[Scripts#Lock|Lock Script]]. Under normal circumstances this complexity shall be hidden from the sender. So it should be the responsibility of the recipient to specify the details of the [[Scripts#Lock|Lock Script]].

**Solution**:

The recipient hands the sender the hash of the lock script. The sender writes that hash into the output. When the recipient wants to spend the output he adds the actual [[Scripts#Lock|Lock Script]] (the *redeem script*) to his [[Scripts#Unlock|Unlock Script]]. The node software then ensures that the hash of the *redeem script* matches the hash in the output and the [[Scripts#Unlock|Unlock Script]] automatically unlocks the *redeem script*

![redeem-script](redeem_script.png)
The first validation is spent, when the sender sends the coin to the recipient and the second validation is done, if the recipient wants to eventually spend the coin.

## Segregated Witness (SegWit, 2017)

Tbd.

## Taproot (2021)

Tbd.

---
links: [[405 DSS TOC - Evolving the Protocol|DSS TOC - Evolving the Protocol]] - [[themes/000 Index|Index]]