tags: #cryptocurrency #scaling

# Transaction Replacement

links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]

---

## Original Transaction Replacement

In order to allow off-chain transactions, Nakamoto implemented a scheme for replacing transactions in the mempool. It allows counterparties to pay each other off-chain at high speed and low cost. Therefore transactions are marked as replaceable and a lock time and sequence number is added for each input. This feature allowed denail of service (DoS) attacks and was therefore deactivated by Nakamoto in 2010.

### Locktime

The locktime defines a time which helps to check the consensus rule, that a transaction can not be included in a block before its locktime.

### Sequence Number

The sequence number helps to check for the mempool policy rule, which says that a transaction in the mempool is only replaced with an incoming transaction if the incomings transactions sequence number is higher than the sequence number of the to be replaced transaction.

Since Transaction Replacements introduce weaknesses into the system, other alternatives for off-chain transactions were introduced: [[Payment Channels]]

## Replacement-By-Fee

To fight the DoS problem in Transaction Replacement originally implemented, the Replacement-By-Fee method was introduced in BIP-125. This update requires replaceable transactions to explicitly opt-in the replaceability of the transaction itself. It also requires that the fee of the replacing transaction is strictly higher than the to be replaced transaction. Like this DoS attacks are mitigated because they are too expensive.

The Replacement-By-Fee transaction replacement makes Bitcoin an *incentive compatible* protocol. This means that no participant can improve their economic situation by deviating from the protocol.

---
links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]