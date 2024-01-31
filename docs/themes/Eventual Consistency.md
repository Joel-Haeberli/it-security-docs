tags: #cryptocurrency #decentralization

# Eventual Consistency

links: [[403 DSS TOC - Decentralization|DSS TOC - Decentralization]] - [[themes/000 Index|Index]]

---

## Consistency vs. Eventual Consistency

Consistency is a key indicator in data storage. An inconsistent data storage is useless because we can not trust that data we are reading is the data we must rely on for our purpose. Therefore consistency is an inevitable property of a system which stores data in some way for later usage. In a peer-to-peer network like Bitcoin we have the problem, that we cannot guarantee consistency because maybe our version of the ledger is out of date at the time we are reading and writing to it. Suppose we have acquired a lock on a row that is being updated by an incoming transaction that we have not yet processed. We will then work with data which is not up-to-date. But the [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]] introduces *eventual consistency* which guarantees that the system will be in a consistent state not immediately but after some time. The [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]] focuses on availability and partition tolerance, addressing the lack of consistency by guaranteeing that it will eventually become consistent. (see [[Anonymity - Trilemmas#CAP Theorem|CAP Theorem]]).

Read also: [How bitcoin Loses to the CAP Theorem](https://paulkernfeld.com/2016/01/15/bitcoin-cap-theorem.html)

## How is Eventual Consistency achieved in Bitcoin?

The [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]] is the first coin which is capable of establishing an eventual consistent state within the distributed peer network. But how is this achieved?

The problem of inconsistency occurs when two nodes find a solution to the puzzle (formulated in [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]]) at the same time. First this will lead to two **forks** of the chain. One part of the network will go on calculating the next block base on the first fork an the other part on the second fork. This process goes on until only one solution is found for the current solution which results in an absolute longest chain. This chain is then taken by all nodes as base for further computation (this comes from how the [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]] handles broadcasts of the leader, by using the leaders block as single source of truth).

So it is a question of probability how fast a chain will become consistent after entering an inconsistent state. This probability relies on two properties:

1. **Block Propagation Time**
	1. This is the time needed for one block to be known by the entire network from the start of its existence.
	2. This depends on block size and internet infrastructure.
	3. There are estimates, that after around 5 seconds since the generation of a block, *half* of the network knows the block.
2. **Inter-Block Time**
	1. This is the average time between two consecutive blocks found by the network (how fast two consecutive puzzles are resolved by the network of nodes).
	2. This is determined by the puzzle difficulty
	3. The Inter-Block time is chosen that it is unlikely two nodes find the solution of the puzzle at the same time (thus preventing a lot of forks). This is around 10 minutes.

An indicator of how sure you can be that a certain transaction is permanently written to the blockchain (and therefore consistent) can be the number of [[Transaction Confirmation|Transaction Confirmations]].

---
links: [[403 DSS TOC - Decentralization|DSS TOC - Decentralization]] - [[themes/000 Index|Index]]