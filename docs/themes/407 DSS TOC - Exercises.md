tags: #cryptocurrency #exercise 

# Exercises - Distributed Systems Security

links: [[400 DSS MOC|DSS MOC]] - [[themes/000 Index|Index]]

---

## Exercise 1 - Think about Bitcoin Clients

### What could happen to your bitcoins if you downloaded a trojan horse masquerading as the bitcoin client instead of the real bitcoin client? 

If you mistakenly download a Trojan horse masquerading as the Bitcoin client, several adverse outcomes could occur. The Trojan could act as a keylogger to capture your cryptographic keys, allowing unauthorized access to your Bitcoin wallet. It could also directly steal Bitcoin from your wallet if it gains access to your wallet's private keys. Additionally, it might install other malicious software that could compromise your computer's security in various ways.

### How do you know that you downloaded the real bitcoin client? 

- Download from the official website: Always download the client from the official Bitcoin website or a trusted source.
- Verify signatures: The official Bitcoin client releases are usually signed by the developers. You can verify these signatures using tools like GnuPG.
- Check the checksum: A checksum is provided for the official client. Compare the checksum of the file you downloaded with the official one to ensure integrity.
- Research: Read up on the latest releases from trusted community sources and forums.
- Use trusted networks: Avoid downloading the client when connected to unsecured or public Wi-Fi networks.
### What would you do if you had 10n+1 dollars in bitcoin? What would you do to ensure that you are using the real bitcoin client?

- Diversify: It's prudent to diversify investments to mitigate risk. Consider spreading the investment across different asset classes.
- Secure Storage: Use hardware wallets for the bulk of your holdings. These are offline and provide a high level of security.
- Continuous Verification: Regularly ensure that you are using the real Bitcoin client by following the verification steps mentioned earlier.
- Professional Advice: Consult with cybersecurity and financial experts to ensure both the security of your Bitcoin and the optimization of your investment strategy.
- Monitor Transactions: Regularly monitor your Bitcoin transactions and wallet for any unusual activity.



## Exercise 2 - Hashing

[[ex2-solution.pdf]]

![[ex2-solution.pdf]]



## Exercise 3 - Proof of Work

[[ex3-solution.pdf]]

![[ex3-solution.pdf]]




## Exercise 4 - Merkle Trees

[[ex4-solution.pdf]]

![[ex4-solution.pdf]]


## Exercise 5 - Merkle Trees Part 2

[[ex5-solution.pdf]]

![[ex5-solution.pdf]]


## Exercise 6 - Bitcoin Whitepaper (Summary)

1. **Introduction**: The paper begins by discussing the limitations of traditional electronic payment systems that rely on trusted third parties, like banks, to process transactions. These systems are prone to fraud and limit the minimum transaction size due to high transaction costs.
2. **Transactions**: Bitcoin transactions are described as a chain of digital signatures. Each owner transfers the coin to the next owner by digitally signing a hash of the previous transaction and the public key of the next owner.
3. **Timestamp Server**: To prevent double-spending, a timestamp server is used to hash a block of items (transactions) and publish the hash. Each timestamp includes the previous timestamp in its hash, forming a chain that reinforces the previous ones.
4. **Proof-of-Work**: The paper introduces a proof-of-work system to implement a distributed timestamp server on a peer-to-peer basis. This involves solving a computationally challenging problem that is easy to verify. The proof-of-work is essential for creating trust in the network and establishing a consensus on the transaction history.
5. **Network**: The steps of operating the Bitcoin network include broadcasting transactions to all nodes, which then work on finding a proof-of-work for their blocks. Accepted blocks are used as the previous hash in the next block, creating a chain.
6. **Incentive**: Bitcoin introduces incentives for nodes to support the network, such as the generation of new coins for the creator of each new block, and transaction fees.
7. **Reclaiming Disk Space**: To reduce the demand for storage space, transactions are hashed in a Merkle Tree, allowing for older transactions to be pruned without compromising the block's hash.
8. **Simplified Payment Verification**: The paper presents a method for users to verify payments without running a full network node, by relying on the longest proof-of-work chain.
9. **Combining and Splitting Value**: Transactions can contain multiple inputs and outputs, allowing for the combination and splitting of value.
10. **Privacy**: The system maintains privacy by keeping public keys anonymous, though some transaction linkages are inevitable.
11. **Calculations**: The paper discusses the probability of an attacker catching up to the honest chain, concluding that this becomes exponentially more difficult as more blocks are added.
12. **Conclusion**: Bitcoin is presented as a solution for electronic transactions without relying on trust, robust in its simplicity and secured by proof-of-work and peer consensus.

## Exercise 7 - Double spending

### You are a bitcoin user and you are running the bitcoin client. Your internet provider completely controls your network. Which of the following attacks can they carry out against you successfully, and why/why not?

1. **Steal Your Coins**:
    - **Feasibility**: Unlikely, unless additional security breaches occur.
    - **Explanation**: Your private keys, which are necessary to access and transfer your Bitcoin, are stored locally on your device, not on the network. So, even a fully compromised network cannot directly steal your coins unless your device is also compromised or your private keys are exposed through other means.
2. **Create Money**:
    - **Feasibility**: Impossible.
    - **Explanation**: The creation of new bitcoins is governed by the Bitcoin protocol and occurs through mining, which involves solving complex cryptographic puzzles. An internet provider doesn't have the ability to alter the Bitcoin protocol or generate valid blocks faster than the rest of the network.
3. **Censor Your Transactions**:
    - **Feasibility**: Possible.
    - **Explanation**: If your internet provider is your only connection to the Bitcoin network, they could potentially block or delay your transactions from reaching other nodes. However, this censorship can often be circumvented by using different network paths, like VPNs or Tor.
4. **Double-Spend Attack You**:
    - **Feasibility**: Highly unlikely, but theoretically possible under certain conditions.
    - **Explanation**: A double-spend attack involves successfully spending the same bitcoins more than once. This is extremely difficult to achieve under normal network conditions due to the consensus mechanism of the Bitcoin network. Your internet provider alone wouldn't have enough hash power to outpace the rest of the network. However, in a hypothetical scenario where they also control a majority of the network's hash rate (51% attack), they could potentially achieve this.
5. **Hide Confirmed Transactions from You**:
    - **Feasibility**: Possible, but you can notice.
    - **Explanation**: The provider could theoretically hide transactions or blocks from you, but this would be noticeable. The Bitcoin client can detect inconsistencies in the blockchain it receives, such as missing blocks or transactions that don't add up. You might not see the latest transactions, but you would likely notice the discrepancy, especially if you're expecting certain transactions or regularly monitoring your balance and the blockchain.

[[ex7-solution.pdf]]

![[ex7-solution.pdf]]



## Exercise 8 - InputOutputCoin

[[ex8-solution.pdf]]

![[ex8-solution.pdf]]


## Exercise 9 - Script

[[ex9-solution.pdf]]

![[ex9-solution.pdf]]



## Exercise 10 - Bitcoin Script

[[ex10-solution.pdf]]

![[ex10-solution.pdf]]

---
links: [[400 DSS MOC|DSS MOC]] - [[themes/000 Index|Index]]