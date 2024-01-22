tags: #ip-sets

# IP sets

links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]

---

## Overview

IP sets provides a framework inside the Linux kernel to store sets of:

- IP addresses
- networks
- TCP/UDP port numbers
- MAC addresses
- interface names
- combination of these

**Use cases**

- Can be administered using the `ipset` utility
- store multiple IP addresses/ports/etc. and match against the collection by iptables in one swoop
- dynamically update iptables rules
- express complex rulesets with one single iptables rule

---
links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]