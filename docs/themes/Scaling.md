tags: #cryptocurrency #scaling

# Scaling

links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]

---

**Challenge**

The more participants take part in the network, the more transactions and therefore more validation operations must be executed. Therefore, the network must be capable of *scaling*.
The question therefore arises how the validation effort of the network changes by an increasing number of participants.

The behaviour of this depends on the throughput of the Bitcoin protocol. The throughput is defined by following properties:

- Block Size Limit (1MB in Bitcoin)
- Median transaction size (300B)

 This leads to around 9 transactions per second (tps). The actual throughput is around 3 to 4 tps. 

Compared to Visa which reaches around 47000 tps this is a funny number. **Bitcoin is too slow**.

On-Chain transactions are expensive, because every participant needs to validate and store it (and the block reward runs out). Therefore for small payments we need off-chain payments, because on-chain payments are too expensive.

[[Transaction Replacement]] tries to mitigate these problems.
 
---
links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]