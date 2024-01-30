tags: #cryptocurrency #scaling

# Payment Channels

links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]

---

## Payment Channels

As described in [[Transaction Replacement]] Nakamoto's introduced mechanism is insecure. That's why other methods have been introduced to allow untrustworthy off-chain payments: payment channels. They rely on [[Conditionals]] and [[Timelocks]]. 

Two of such payment channels are [[Timelocks#OP_CHECKLOCKTIMEVERIFY (CLTV)|CLTV]]-style payment channels and Lightning channels

### [[Timelocks#OP_CHECKLOCKTIMEVERIFY (CLTV)|CLTV]] Payment Channels (Unidirectional)

Since Alice expects to pay Bob multiple times, she wants to put everything in one transaction which helps her to safe fees. She ***prepares*** a transaction (2-of-2 multisig transaction, like this Bob is sure that she cannot spam him) which she does **not broadcast** but instead sends the draft to Bob. Alice repeats this procedure every time she wants to pay Bob again (this creates a *commitment transaction* which is already signed by Alice). According to the consensus rules in [[Timelocks#OP_CHECKLOCKTIMEVERIFY (CLTV)|CLTV]] this will update Bob's transaction inside mempool if the transaction meets the requirements. Bob can, if Alice will not pay anymore coins, broadcast the highest paying transaction. This transaction closes the payment channel and pay the highest specified amount of coins to Bob.

**Operations**

1. *Open the Channel*: Alice broadcasts a special transaction that locks coins using 2-of-2 multisig
2. *Make a payment*: Alice sends unconfirmed transactions to Bob which spend from those locked coins to Bob
3. *Close the Channel*:
	1. *Normal Closure*: Bob signs and broadcasts the highest value transaction he received from Alice
	2. *Expiry*: If Bob stops to cooperate, after the expiry time passes, Alice broadcasts a transaction taking her money back

**Properties**

- the channel does not depend on miners $\rightarrow$ bob can be sure that the output of the opening transaction is spendable if he acts within the expire date
- Alice can not cheat Bob by broadcasting an old transaction, she does not have Bob's signature
- these channels have limited lifetime and are one-way

### Lightning Payment Channels (Bidirectional)

The main problem we have is that currently we are not able to invalidate an old commitment transaction (they are also called *channel state*). The Lightning Channel is capable of invalidating commitment transactions, by introducing some cryptographic secrets to the communication:

1. Alice chooses a secret $R_{A1}$, Bob chooses a secret $R_{B1}$
2. They exchange the hash of their respective secret with an opening transaction
3. They exchange the commitment transaction and confirm the opening transaction

To make further payments in the channel both can choose a new secret and repeat steps 2 and 3 above. The opening transaction specifies the maximal spendable amount. If this amount is exceeded, a new channel must be opened by starting the process from the beginning.

A channel can besides a cooperative closure also be closed by either *expiry* or an *old state being published*. 

- In case of expiry, Alice can broadcasts her latest commitment transaction and a transaction spending from this the latest commitment transaction to herself (after the specified delay, this transaction will be confirmed).
- In case an old state is published it depends:
	- If the party who is about to lose money does *not detect*, that the transaction is an old, the party *loses money*.
	- If the party who would lose money *detects* the old state, it can *punish* the other party by claiming all money in the channel. 

#### How does the lightning channel work?

##### 1. Alice and Bob file an opening transaction 

To open a lightning channel, both sign the opening transaction specifying the amount of coins inside the channel. 
![lightning_channel_opening_transaction](lightning_channel_opening_transaction.png)
Here Alice and Bob put 1 coin inside the opening transaction and agreeing that the amount spendable inside this channel will be 2 coins.
##### 2. Alice and Bob create secret

Alice and Bob both choose a their respective secret $R_{A1}$ and $R_{B1}$ which they keep to them. They exchange the **hash** of their secrets.
##### 3. They exchange a commitment transaction

As Alice or Bob want to pay their counter party, they create a commitment transaction which contains the new balances and the respective signatures.

![lightning_channel_commitment_transaction](lightning_channel_commitment_transaction.png)

We see that Alice commitment transaction contains Bob's balance signed by himself. The balance of Alice is signed by her and a timelock of one day OR Bob and Alice's secret.
On the other hand we have the same situation, that Bob has the balance of Alice signed by her and his balance signed by him and a timelock of one day OR Alice's signature and Bob's secret.

##### 4. They repeat step 2 and 3

As long as the balance is high enough and they want to pay each other, they repeat step two and three. This means for each commitment transaction new secrets are generated. Important is that after creating the new commitment transaction with new secrets, they share the old secret with each other [preventing the other party broadcasting older transaction which favours them more](https://bitcoinmagazine.com/technical/understanding-the-lightning-network-part-building-a-bidirectional-payment-channel-1464710791).

The lightning payment channel can be leveraged to create a [[Lightning Network]].

---
links: [[406 DSS TOC - Scaling|DSS TOC - Scaling]] - [[themes/000 Index|Index]]