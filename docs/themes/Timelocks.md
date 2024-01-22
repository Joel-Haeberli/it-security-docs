tags: #cryptocurrency #scaling

# Timelocks

links: [[406 DSS TOC - Scaling]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]

---

# Locktime details

Remember: lock times of [[Transaction Replacement]]

The locktime field of a transaction is interpreted differently depending on the value. This means that a locktime value is seen as...

- block number, if $locktime < 500$ million
- unix timestamp, if $locktime \geq 500$

In most transactions, the locktime is zero, which means the transactions can be confirmed immediately. A consensus rule says that if all inputs have a sequence number of MAXINT ($2^{32}$), the locktime is ignored.

Problems arise using locktimes because both parties know, that a transaction cannot be performed before the set locktime. The receiver can not even be sure that the transaction will be confirmed, because it is possible that the sender double spends coins. This basic scheme is trash. We need to timelock outputs of already confirmed transactions:
### OP_CHECKLOCKTIMEVERIFY (CLTV)

This operation allows timelocking per output. This means each output can have its own time wise restrictions regarding the time of spending. It restricts spending the output in the way preventing it to be spent in a transaction with lower or equal locktime. Like this, once the transaction is confirmed, the sender can not double spend.

The operations works as follows (simplified):

1. Take locktime $t_1$ from the stack
2. Take locktime $t_2$ of the spending transaction
3. Fail to spend if $t_1 > t_2$
### Relative Lock Time

The Sequence Number of [[Transaction Replacement]] was repurposed allowing Relative Lock Times. This means that a transaction with sequence number value of $n$ can only be confirmed $n$ blocks after the referenced output was confirmed. Since the sequence number has 32 bits and the value of the relative lock time only uses 16bits, the first bits of the two first bytes (MSB) have special pruposes. The first bit of the first byte (MSB) is the Activation Flag. It allows disabling the relative lock time. The first bit of the second byte, represents the type flag. It defines wether the value means $n$ blocks or $n \times 512$ seconds.

![sequence-number-repurpose](sequence_number_abuse.png)
### OP_CHECKSEQUENCEVERIFY (CSV)

This operation was introduced in 2016 and allows relative time locking per output. It restricts outputs to only be spent in an input with a higher relative lock time (sequence number value).

## Fee Sniping

Fees are intended to incentivize the competition of the last block. The combination of the highest paying transaction from the last block and the current block have more fees than the transactions in the current block (mine this combination is called *fee sniping*). Since there are still rewards incentivizing the participation in the network, at the moment this is not a problem but will become one if the reward run out (coin limit is reached). To defend against fee sniping, transactions are timelocked to the next block.

[Bitcoin Stackexchange about Fee Sniping](https://bitcoin.stackexchange.com/questions/120922/what-is-fee-sniping)
## Timelocks use Median-Time-Past

To prevent participants from lying, timelocks are based on the Median-Time-Past (described in [[From IncentiveCoin to Bitcoin#DifficultyAdjustmentCoin|DifficultyAdjustmentCoin]]). This time is backed by the network and so manipulating it is as hard as an 51% attack which are hard since the [[From BankCoin to IncentiveCoin#IncentiveCoin|IncentiveCoin]].

---
links: [[406 DSS TOC - Scaling]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]