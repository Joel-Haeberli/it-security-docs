tags: #netfilter #iptables

# iptables utility

links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]

---

## Overview

- the utility `iptables` is used to **set up, view, delete and modify chains and their rules**
- more information: `iptables -h` or `man 8 iptables`
- version of iptables: `iptables -V`

## Tables

- use `-t` to specify a table
- if no table is specified, the **filter** table is chosen automatically

```bash
iptables -t filter # specifies filter table
iptables -t nat    # specifies nat table
```

## Listing of chains and rules

- use `-L` to list all rules of a selected chain
- use `-v` (verbose) to list interface name, packets, byte counters, ...
- use `-n` (numeric) to display IP addresses and port numbers in numeric format $\rightarrow$ by default, it tries to resolve addresses and port numbers and display them as host/network/service names, this can be time consuming
- use `--line-numbers` to print line/rule numbers

```bash
iptables -t filter -L # rules of the filter table
iptables -t nat -L -v # verbose rules of the mangle table
iptables -t mangle -n # rules of the mangle table in numeric format
```


## Set default policy

- use `-P` to set up a default policy of a built-in chain $\rightarrow$ be aware, not all tables have all chains (see [[iptables table architecture]])

```bash
iptables -t nat -P OUTPUT ACCEPT # set default policy of OUTPUT chain in nat table
```

## User-defined chains

- use `-N` to create a user-defined chain
- use `-X` to delete a user-defined chain
- use `-E` to rename a user-defined chain

```bash
iptables -t nat -N mynat        # create new chain "mynat" in nat table
iptables -X junk                # delete user-defined chain "junk" from filter table
iptables -t mangle -E test work # rename chain "test" to "work" in mangle table
```

## Rules

Rules of a chain can be modified using following options:

- `-A`, `--append chain <rule-specification>`
- `-D`, `--delete chain <rule-specification>`
- `-D`, `--delete chain rulenum`
- `-I`, `--insert chain [rulenum] <rule-specification>`
- `-R`, `--replace chain rulenum <rule-specification>`

- `rulenum` can be found out using `--line-numbers`
- `<rule-specification>` contains the packet matching rule and can be very complex

## Rule specification

The following options can be used to define packet matching filter rules:

- `-p`, `--protocol [!] protocol`
- `-s`, `--source [!] address[/mask]`
- 

## Flush chains, reset counters

- use `-F`(Flush) to flush a chain
- use `-Z` (Zero) to set all counters of a chain to zero

```bash
iptables -t nat -F PREROUTING # flash PREROUTING chain of nat table
iptables -t mangle -Z INPUT   # reset counters of INPUT chain of mangle table
```

---
links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]