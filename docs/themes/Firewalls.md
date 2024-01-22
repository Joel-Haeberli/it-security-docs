tags: #firewall #host-security #network-security

# Firewalls

links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]

---

## Security Classification

- Technical security $\rightarrow$ System security $\rightarrow$ host & network security

A better **information system security** can be achieved with:
- **host-based** security mechanisms (system in a network)
- **network-based** security mechanisms (subnets, network zones)

## Host-based Security Mechanisms

- **operating system**: updates, patches
- **host hardening**
- **host or personal firewall**: securing incoming and outgoing network access
- **host intrusion detection an prevention/protection systems**: HIDS/HIPS
- **recent virus and content scanner**
- **endpoint security/endpoint protection**
- **secure applications**: designed and programmed to minimize security risk
- **centralized Security Information and Event Management (SIEM)**: send audit, system and other logs to aSIEM

## Network-based Security Mechanisms

- **network firewalls**: protection of networks (subnets, segments, zones) against **external attackers**
- **access control through active network devices**: protection of networks against **internal attackers**
	- network intrusion detection and prevention systems (NIDS/NIPS)
	- port based authentication, network access control (NAC)
- use of centralized SIEM: also send firewall logs, access logs, IDS, flow data, ...

## Host or Personal Firewalls

- monitors incoming and outgoing connections
- prevents host from port scans
- **limitations**:
	- consumes resources, can be target of an attack
	- if host is compromised, the firewall is also affected

## Network Firewalls

- connects two or more network segments
- capability to control, log and deny packets (filter) and modify packets (mangle)
- **limitations**
	- cannot protect against **internal attackers**
	- malware which came in through allowed applications
	- secured or tunneling connections running through the firewall (IPSEC, SSH, TLS)

## Network layer firewall

- act on the network layer
- also named **packet filters** (drop unwanted packages)
- checking of the **Header entries**
	- traversed interfaces and direction: `eth0 inbound`
	- [[Important Header Fields#MAC header|L2 MAC Header]]: 
		- source/destination address: `00:D0:20:34:4F:55`
		- ethertype: `0x800, 0x806, ...`
		- tag protocol identifier: `0x8100` followed by priority code point & VLAN ID
	- [[Important Header Fields#IP header|L3 IP Header]]:
		- source/destination address: `192.168.1.10, 2001:620:500::1`
		- protocol/ next header: `1, 6, 17`
	- [[Important Header Fields#ICMP Header|L4 ICMP/TCP/UDP Header]]:
		- source/destination port: `22, 20, ...`
		- TCP control bits: `SYN, ACK, FIN, ...`
		- ICMP message types & code: `0, 3/0, 8, 11/1, ...`
- packet fragmentation/reassembling
	- fragments of IP-packets must be reassembled before a reason check of the layer 4 headers can be done
	- reassembling usesadditional resources which is a target for **DoS attacks**

### Stateless Packet Filter

- not recording state information of connections and only filter according to **predefined filter rules**
- less secure but more efficient then stateful packet filters
- **disadvantages**: outdated, difficult configuration, packets cannot be modified

*Example for SSH Filter Rules*
![[stateless-rules.png]]
*Example for SSH Filter Rules (Evaluating ACK-Flag)*
![[stateless-rules2.png]]
### Stateful Packet Filter


**Types of packet filter firewalls**
- stateless packet filter (outdated)
- **stateful packet filter**
- **stateful inspection firewall**
- **next generation firewall**
- **Threat protection firewall**


- **network layer** firewall
- **application layer** firewall
- **DNS** firewall
- **Hybrid** firewalls (combination of above firewalls)

---
links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]