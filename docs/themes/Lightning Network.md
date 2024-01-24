tags: #cryptocurrency #scaling

# Lightning Network

links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]

---
## The lightning network

To understand the lightning network it is a good idea to understand the [[Payment Channels#Lightning Payment Channels (Bidirectional)|Lightning Payment Channel]].

The lightning network leverages the bidirectional payment channel introduced by the [[Payment Channels#Lightning Payment Channels (Bidirectional)|Lightning Payment Channel]]. Now a network can be formed of such channels.

### Multi-Hop Payments

Through the linking of multiple lightning channels together, Multi-Hop payments are possible. This allows to route payments trustless through multiple lightning channels.

### In-Flight Outputs

Coins that are in-flight are part of the channel state (commitment transaction). In-Flight coins are coins which are not handled between the two parties participating in the channel but are on the route and therefore pass the channel.

### Timeout

Since nodes on the route from sender to final recipient on the network might go offline, the sender must be capable to take back his money in this case.

### Revokability

All payments to a party are stealable by the counter party on the channel with the revocation secret.

### Hash Timelock Contracts (HTLC)

The Hash Timelock Contract (HTLC) is the output script of in-flight transactions. Translated to a human condition it means: "If you give me a secret within a certain time, you can take the money". The Timeout is called HTLC timeout.

### Lightning Fees

Node operating the lightning service will of course charge for forwarding payments and take a fee. The consists of a fixed base fee and a percentage fee based on the amount forwarded.

---
links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]