tags: #cryptocurrency #bitcoin #timestamp #timestamping

# Timestamping

links: [[402 DSS TOC - Preliminaries]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]

---

## Concept & Usage

The idea of timestamping is to guarantee that specific data existed at certain time. (*Put data into an envelope and mail to yourself*)

Timestamps are used to prove that certain software or other work existed at a given time.  They can help in case of recovery. They also ensure that signatures are valid even after a key was revoked.
## Trusted Timestamping

Trusted Timestamping is one way of creating timestamps leveraging a trusted third party, *whom we **trust*** to add the correct timestamp. The TTP will add a signature using its private key which can be verified by others using the TTP public key. The signature will sign the to be stamped data and the timestamp. This links the data to a timestamp.

Problem: requires **Trust**, once the secret key of the TTP is compromised, all its timestamps are useless.
## Linked Timestamping

The TSS issues a series of timestamps. These timestamps include not only the timestamp itself but also the hash of the timestamp issued before the current timestamp. This links timestamps together and gives us trust agility. This means that I can verify a timestamp based on a timestamp signed by someone I trust.

![Linked Timestamping](linked_timestamping.png)

Let's say I want to verify the timestamp of a document, Alice tells to have turned in on time. I don't know her so I don't trust her. Sadly the key of the Timestamp Server was compromised after Time $t_2$. I trust Bob who has a message of the Timestamp Server signed by it before $t_2$. I can verify the signature of Bob and find out (due to the linking of the timestamps) that the Alice's timestamp was issued before Bob's timestamp. This gives me the answer I wanted.

---
links: [[402 DSS TOC - Preliminaries]] - [[400 DSS MOC]] - [[themes/000 Index|Index]]