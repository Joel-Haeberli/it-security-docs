tags: #cryptocurrency #decentralization #double-spending-attack

# Double Spending Attack

links: [[403 DSS TOC - Decentralization|DSS TOC - Decentralization]] - [[themes/000 Index|Index]]

---

## Double Spending Attack

The Double Spending Attack is the act of writing the same transaction with different recipients, so that the same coin is spent twice $\rightarrow$ therefore double spending. 

The Problem is approximately solved by the [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]] under following **assumptions**:

1. Network will always find consensus eventually (see [[Eventual Consistency]])
2. The Recipients of a payment wait long enough before delivering their assets (waiting in this context means that a transaction has enough confirmations, so that it can be seen as final [[Transaction Confirmation]])
3. Nobody controls close to half of the network (which is hard according to [[From BankCoin to IncentiveCoin#IncentiveCoin|IncentiveCoin]])

## Probability of a Successful Double Spending Attack

- original calculation by Nakamoto and improved by Rosenfeld
- the probability that an attacker reverses a transaction depends on:
	- the attacker's hash rate as a percentage of the entire network
	- the number of confirmations of the transaction
- the probability decreases exponentially with the number of confirmations
- we assume an *(economically) rational* attacker: such an attacker will only perform attacks that are profitable $\rightarrow$ weighs the gain of a successful attack with their respective probabilities

**Maximal Safe Transaction Value**

- In [[From BankCoin to IncentiveCoin#IncentiveCoin|Incentive Coin]], we now know the gains and losses and can compute a *maximal safe transaction value* (analysis of Rosenfeld with some assumptions like block reward value)
- in this table, we can see how much transactions we have to wait for a specific transaction value (e.g. 1'000 BTCs), if we assume an adversary model of a specific percentage of computational power of the network (e.g. the attacker owns 20% of the computational power)
- *Example*: we have a transaction of 800 BTCs and the attacker has 30% of computational power. The *Maximal Safe Transaction Value* table told us to wait in minimum 8 transactions (after this amount of transactions, a double spending attack would not be valuable for an rational attacker)

---
links: [[403 DSS TOC - Decentralization|DSS TOC - Decentralization]] - [[themes/000 Index|Index]]