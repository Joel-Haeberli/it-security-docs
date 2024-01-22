tags: #netfilter #iptables

# Connection Tracking Subsystem

links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]

---

## Overview

- the **Connection tracking subsystem** of [[netfilter]]/[[iptables]] enables the **tracking of state information of connections** in a kernel table (connection tracking table)
- this allows the build of [[Firewalls#Stateful Packet Filter|stateful packet filtering firewalls]]
- on older systems the table was overlaid to `/proc/net/nf_conntrack`, on more recent systems there is an API which can be used to query/modify the table
- the utility IP tables state `ipstate` can be used to query and display the table

## Adding entries

- the entries in the table are added by **packets running through the `PREROUTING` chain and the `OUTPUT` chain respectively**
- this happens before the iptables rules get activated
- source and destination NAT are mapped in the table too

## Example entries of /proc/net/nf_conntrack

![[connection-tracking-subsystem-example-1.png]]

![[connection-tracking-subsystem-example-2.png]]

![[connection-tracking-subsystem-example-3.png]]

## State examination

The state of connections can be examined using iptables match extensions `conntrack`:

- `NEW`: the packet has started a new connection
- `ESTABLISHED`: the packet is associated with an established connection, both directions
- `RELATED`: new connection created as a result of an associated connection (e.g. FTP data connection)
- `INVALID`: the packet is associated with no known connection
- `SNAT`: virtual state, matching if the original source address differs from the reply destination
- `DNAT`: virtual state, matching if the original destination differs from the reply source
- ...

---
links: [[606 SPA TOC - Linux Firewall|SPA TOC - Linux Firewall]] - [[themes/000 Index|Index]]