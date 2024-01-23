tags: #netfilter #nftables

# nftables utility

links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]

---

##  Tables

- see available [[nftables#Tables|kind of families]]

```bash
nft list tables              # list all tables
nft list tables arp|ip|...   # list tables per family
nft list table ip myfilter   # list the content of a specific table

nft add table ip myfilter    # adding an IPv4 table named "myfilter"

nft delete table ip myfilter # delete tyle, table must be empty!

nft flush table ip myfilter  # flush the rules, clear all rules
```

## Chains

Possible chain types: `filter`, `route`, `nat`

### Base chain

- [[nftables#Base chain|base chain]]
- [[netfilter#Netfilter Hooks|Netfilter hooks]]

```bash
# add new base chain "myinput" to existing IPv4 table "myfilter"
# "myinput" is hooked to the netfilter "input hook"
nft add chain ip myfilter myinput { type filter hook input priority 0 ; }

# add new base chain with a default accept policy
nft add chain ip foo myoutput { type filter hook output priority 0 ; \
	policy accept; }
```

**Hook priority value**

![[nftables-priorities.png]]

### Regular or non-base chain

- [[nftables#Regular or non-base chain|regular or non-base chain]]

```bash
# add regular chain "myinput" to existing IPv4 table "myfilter"
nft add chain ip myfilter myinput

# delete an empty chain
nft delete chain ip myfilter myinput

# flush a chain (clear all rules)
nft flush chain myfilter myinput
```

## IPv4-filter example

- the `ipv4-filter` and `ipv4-nat` of the nftables distribution provides an iptables-like filtering/nat structure

![[nftables-ipv4-filter-example.png]]

![[nftables-ipv4-nat-example.png]]

## Rules

To add new rules, the table and the chain must be specified

```bash
# list rules and chains of a table
nft list table myfilter
nft -n list ... # no hostname resolution
nft -nn list ... # no hostname and service name resolution

# add new rules to the table "myfilter" and the chain "myoutput"
nft add rule myfilter myoutput ip daddr 8.8.8.8 counter
nft add rule myfilter myoutput tcp dport ssh counter
```

### Rule management

- to add, insert and remove rules at a given position the rule handle is required:
	- `add`: after the referenced rule
	- `insert`: at the place of the referenced rule
	- `delete`: the referenced rule
- use `flush` to empty a chain or a table

```bash
# print out the rule handles
nft -a list ...

# examples
nft add rule myfilter myoutput position 8 ip daddr 127.0.0.8 drop
nft insert rule myfilter myoutput position 9 ip daddr 127.0.0.1 drop
nft delete rule myfilter myoutput handle 5

# insert a rule at the first position of a chain
nft insert rule myfilter myoutput ip daddr 192.168.1.1 counter

# flush all rules of a chain
nft flush chain myfilter myoutput

# flush all rules of all chains of a table
nft flush table myfilter
```

### Expressions

- x

### Ruleset

- see [[IP sets]]

```bash

```

### Save and restore rules

- to (atomically) replace a rule set a `flush table myfilter` line must be added at the beginning of the file `myfilter-table`

```bash
# save rules to file
nft list table myfilter > myfilter-table

# atomically update rule set from a file
nft -f myfilter-table
```

---
links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]