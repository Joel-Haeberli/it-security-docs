tags: #linux #

# 606 SPA TOC - Linux Firewall

links: [[606 SPA TOC - Linux Firewall]] - [[600 SPA MOC|SPA MOC]] - [[themes/000 Index|Index]]

---

## About

To understand the linux firewall and [[netfilter]], [[iptables]], [[nftables]] or [[bpfilter]] it's a good idea to understand the basic building blocks of them. Therefore this page explains the terms `Tables`, `Chains` and `Rules` which shall help to understand how the linux firewall builds up on these constructs.
## Tables

WHICH FUNCTIONALITY of the network stack is requested by in- or outgoing packet?

A Table contains a list of Chains which concerns one specific functionality of the networking stack. This means that if you process a package in favor of an application you want to enforce all Rules of all Chains of the Filter Table. But if you do NAT, you want to call the NAT Table which contains Chains containing Rules important to enforce during NAT.

Following default Tables exist:

- Filter: Table used for packets being forwarded on the system
- NAT: Table used during NAT
- Mangle: Table used to modify IP packets
- Raw: 
## Chains

WHEN is a rule to be processed?

Chains define at which time (hook of the [[netfilter]] framework) the chain (set of rules) is applied to a packet.

## Rules

WHAT is checked for in a package?

The rule describes, what is to be done with the packet. This can either result in accepting, dropping or changing the packet in some way. A rule defines a target. The target is the decision or what should happen with the packet according to the rule.

[Baeldung on iptables and how packets traverse the chains](https://www.baeldung.com/linux/iptables-chains-tables-traversal)
[Good video explaining basic usage of iptables](https://www.youtube.com/watch?v=6Ra17Qpj68c)

For a deeper introduction to [[netfilter]] and [[iptables]], refer to the respective [[606 SPA TOC - Linux Firewall|Linux Firewall topic]].

---
links: [[600 SPA MOC|SPA MOC]] - [[themes/000 Index|Index]]