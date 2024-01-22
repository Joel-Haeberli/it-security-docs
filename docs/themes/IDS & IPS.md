tags: #ids #ips

# IDS & IPS

links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]

---

## Overview

- Intrustion detection & prevention systems (IDS/IPS)
- can **detect attacks or attempts to attack** against hosts and networks
- can **work together with firewalls and network devices** to prevent or stop attacks

## Host based IDS/IPS (HIDS)

- work close together with OS
- can detect attacks against the host
- can have a **negative impact on system performance and stability**
- sometimes not able to detect network based attacks (e.g. DoS attacks)

## Network based IDS/IPS (NIDS/NIPS)

- analyze all network traffic, intelligent **protocol analyzer**
- **detect attacks, start counter-measures**
- need access to all packets of a network segement (often realized with **mirror ports** on switches)
- can **detect anomalies** and react preventive by interaction with network firewall
- not always detect attacks (e.g. if the attack is distributed on multiple packets and fragments, low profile attacks)
- can be disabled by DoS attacks, which they should detect

## Hybrid IDS/IPS

- combination of both host and network-based IDS/IPS
- allows a **better recognition of anomalies and attacks**
- consists of:
	- a **central management system**
	- **host based sensors**
	- **network based sensors**

---

links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]