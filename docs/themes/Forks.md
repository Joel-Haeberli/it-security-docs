tags: #cryptocurrency #protocol

# Forks

links: [[405 DSS TOC - Evolving the Protocol]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]

---

## Forking

A fork happens, when state becomes inconsistent. In Blockchain are thus a possible state (even if they are resolved automatically after some time due to [[Eventual Consistency]]). Forks are more than one state existing at an instant of time. In Bitcoin two types of forks are common: Network and Software Forks.

## Network Fork

A Network fork happens if the puzzle is solved at the same time by more than one participant and thus different chains are considered as valid. Under normal circumstances network forks are resolved and brought together and quickly resolved automatically due to the [[Eventual Consistency]] property of the [[From BankCoin to IncentiveCoin#BlockchainCoin|BlockchainCoin]]. Such a network fork is also called *chain split*.
## Software Fork

A software fork happens every time a new release of a software package is released. Each release has its own version and properties. Each of them represent a fork of the respective software. For example nodes running different client versions represent a software fork.

A software fork can be a cause for a network fork. Such a fork is called a *hard fork* if the network fork is permanent (it essentially splits the network into the part running successors of the previous version and the part running successors of the *hard forked* version). If the network will eventually become consistent, the fork is called a *soft fork*.
### Soft Forks

A soft fork is an update  of the consensus rules that all blocks according to the new rules are also valid according to the old rules. Soft forks are the generally accepted way to make protocol updates to Bitcoin, because it will not cause permanent network forks if the majority of the hash power switches to the new rules. A soft fork might include:

- Decrease block size limit
- Decrease block reward

Example: If I decrease the block size limit from 4 bytes to 2 bytes, a newly created block of 2 bytes is also valid under the old rule of max. 4 bytes per block (backward compatibility).
### Hard Forks
 
A hard fork is an update of the consensus rules such that new blocks are valid under the new rules but perhaps not anymore under the old rules. Hard forks are considered too risky for protocol updates, because they cause permanent network forks. Hard forks might include:

- Increase block size limit
- Increase block reward
- Changing the format of a block

Example: An old block was allowed a maximal reward of 0.5 Bitcoin. The new rule states, that a maximal reward of 1 Bitcoin can be given to the solver of the puzzle. This means that a block with more than 0.5 Bitcoin rewards is not valid under old rules but valid under the new rules.

---
links: [[405 DSS TOC - Evolving the Protocol]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]