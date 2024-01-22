tags: #netfilter

# Netfilter

links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]

---

## Overview

- netfilter and [[iptables]] are components of a **packet filtering framework** inside the **Linux Kernel** since version 2.4
- [[nftables]] is a newer alternative to [[iptables]] integrated into the Linux Kernel since version 3.13

## Packet filtering framework

- allows to:
	- build **packet filter firewalls**
	- do any kind of **NAT and NAPT**
	- do **further packet manipulation**
- components:
	- netfilter
	- Xtables: **iptables** (IPv4), **ip6tables** (IPv6), **arptables** (ARP), **ebtables** (Ethernet bridge filtering)
	- [[Connection Tracking Subsystem]]
	- **NAT/NAPT** subsystem
	- [[nftables]]

![[netfilter-components.png]]

## Netfilter

Provides a **set of hooks** inside the Linux kernel that allows kernel modules to register callback functions with the network stack

### Netfilter Hooks

![[netfilter-hooks.png]]

### Main features netfilter/iptables

- **stateless packet filtering**
- **stateful packet filtering**
- all kind of **network address and port translation (NAT/NAPT)**
- multiple layers of APIs for **3rd party extensions**

### Use cases netfilter/iptables

- **build internet firewal**l
- use **NAT and masquerading**
- use NAT to implement **transparent proxies**
- aid the tc (traffic control) and iproute2 systems to **build sophisticated QoS** and **policy routers**
- do further **packet manipulation**

---
links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]