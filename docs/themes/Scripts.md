tags: #cryptocurrency #bitcoin #bitcoin-scripts #scripts
# Scripts

links: [[404 DSS TOC - Bitcoin]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]

---

As described in [[From IncentiveCoin to Bitcoin#ScriptCoin|ScriptCoin]] ...
## Bitcoin Script
Bitcoin script is the assembly language leveraged by bitcoin to validate transactions (see [[From IncentiveCoin to Bitcoin#ScriptCoin|ScriptCoin]]). It is stacked based and comes with a distinguished set of operations which it is capable of solving. A Bitcoin script executes and if at the end of the execution, the stack is either empty or the top element is true, the script was successful. Otherwise the script failed and the Input-Output pair of the transaction must be refused. A Bitcoin Script is composed of two distinct scripts called the Unlock- and the Lock-Script. First the work of the unlock script is done, then the work of the lock script. If the final result is a valid solution (empty stack or true as top element), the transaction goes through.
## Unlock
The unlock script is the script that runs during the transaction validation to validate the input.
## Lock
The lock script runs during the transaction validation to validate the output.
## Pay-To-Pubkey
A *Pay-To-Pubkey* script consists of an unlock and a lock script which do the following (Pay amount of coins to public key matching the public key of the recipient):

Unlock-Script:

1. Push signature of the to be verified input to the stack

Lock-Script:

1. Push public key of recipient to the stack
2. Verify signature on the stack with the pushed public key

![pay-to-pubkey](pay_to_pubkey.png)

## Pay-To-Pubkey-Hash
A *Pay-To-Pubkey-Hash* script consists of an unlock and a lock script which do the following (Pay amount of coins to hash matching the hash of the public key of the recipient):

Unlock-Script:

1. Push signature of the to be verified input to the stack
2. Push public key, that can verify the signature, to the stack

Lock-Script:

1. Duplicate public key
2. Hash duplicated public key
3. Push hash of public key contained in the output
4. Compare hashed duplicated public key with public key hash of output
5. Verify signature on the stack

![pay-to-pubkey-hash](pay_to_pubkey_hash.png)
![pay-to-pubkey-hash-stack](pay_to_pubkey_hash_stack.png)
## Multisignature
A *Multisignature* script consists of an unlock and a lock script which do the following (Pay only if $x$ in $n$ parties sign to spend the output):

Unlock-Script:

1. Push 0 to the stack (due to a bug in OP_CHECKMULTISIG)
2. Push all available signatures

Lock-Script:

1. Push number of *required* signature $x$
2. Push all public keys contained in output
3. Push number of pushed public keys $n$, $n >= x$
4. Check all signatures and count that at least $x$ valid signatures were present (all done by OP_CHECKMULTISIG)

![multisig](multisig.png)
![multisig-stack](multisig_stack.png)
## OP_RETURN
OP_RETURN is an operation code (opcode), which will throw an error whenever it is reached. An output that is locked with a script that contains OP_RETURN is unspendable due to this. A script can contain up to 80 bytes after the OP_RETURN instruction.

---
links: [[404 DSS TOC - Bitcoin]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]