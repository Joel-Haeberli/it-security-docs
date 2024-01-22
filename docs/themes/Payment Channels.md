tags: #cryptocurrency #scaling

# Payment Channels

links: [[406 DSS TOC - Scaling]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]

---

## Payment Channels

As described in [[Transaction Replacement]] Nakamoto's introduced mechanism is insecure. That's why other methods have been introduced to allow trustless off-chain payments: payment channels. They rely on [[Conditionals]] and [[Timelocks]]. 

Two of such payment channels are [[Timelocks#OP_CHECKLOCKTIMEVERIFY (CLTV)|CLTV]]-style payment channels and Lightning channels

### [[Timelocks#OP_CHECKLOCKTIMEVERIFY (CLTV)|CLTV]] Payment Channels (Unidirectional)

Since Alice expects to pay Bob multiple times, she wants to put everything in one transaction which helps her to safe fees. She ***prepares*** a transaction (2-of-2 multisig transaction, like this Bob is sure that she cannot spam him) which she does **not broadcast** but instead sends the draft to Bob. Alice repeats this procedure everytime she wants to pay Bob again (this creates a *commitment transaction* which is already signed by Alice). According to the consensus rules in [[Timelocks#OP_CHECKLOCKTIMEVERIFY (CLTV)|CLTV]] this will updates Bob's transaction inside Mempool if the transaction meet the requirements. Bob can if Alice will not pay anymore coins, broadcast the highest paying transaction.
### Lightning Payment Channels (Bidirectional)

The main problem we have is that currently we are not able to invalidate an old commitment transaction (they are also called *channel state*). The Lightning Channel is capable of invalidating commitment transactions, by introducing some cryptographic secrets to the communication:

1. Alice chooses a secret $R_{A1}$, Bob chooses a secret $R_{A2}$
2. They exchange the hash of their respective secret with an opening transaction
3. They exchange the commitment transaction and confirm the opening transaction

To make further payments in the channel both can choose a new secret and repeat steps 2 and 3 above.

#### The lightning network


---
links: [[406 DSS TOC - Scaling]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]