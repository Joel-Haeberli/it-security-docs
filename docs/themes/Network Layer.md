tags: #osi

# Network Layer

links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]

---

## Network Layer

- Sending and receiving packets
- Addressing and routing of packets between hosts
- Fragmenting and reassembling packets
- Relevant topics: IP, ICMP

### Vulnerabilities

- Route spoofing / DoS
	- Propagation of false network topology using [RIP](https://en.wikipedia.org/wiki/Routing_Information_Protocol)
	- Goal: Route data through attacker controlled router
	- Goal: Create loop
	- Goal: Impersonate specific host
- IP address spoofing
	- False source addressing on malicious packets
	- Goal: Attacker can send malicious packets that appear to come from within the network
	- Requirement: Attacker knows currently used IP addresses in the network
- Identity & resource ID vulnerability
	- reliance on addresses to identify resources and peers can be brittle and vulnerable
	- Example: Access to router based on IP address. Attacker can spoof IP address and get access to router
- Misuse (spoofing/starvation/DoS) of automatic device configuration mechanisms (DHCPv4, [IPv6 SLAAC](https://datatracker.ietf.org/doc/html/rfc4862), DHCPv6)
	- Attacker sets up rogue DHCP server to issue IP configuration
		- Set attacker as router -> Man-in-the-middle attack
		- Set wrong IP as router -> Network DoS
	- Attacker creates virtual interfaces to generate large number of IPv6 address configuration requests
		- Overload roxuter or DHCPv6 server capacity to track devices
		- Legitimate devices can't obtain IP anymore -> starvation, DoS

### Attacks

- [[#Vulnerabilities|IP address spoofing]]
- [[#Vulnerabilities|Routing attack]]
- IPv6 neighbour discover attack / spoofing
	- Similar to ARP-spoofing
- [[ICMP]] Attack
	- ICMP is used to send one-way informational messages to hosts (no authentication)
	- Sending forged ICMP "Time exceeded" or "Destination unreachable" to a host
		- Goal: Break communication between two hosts -> DoS
	- Sending ICMP "Redirect" 
		- Goal: Attacked host sends certain packets through attackers host
	- PING Flood (ICMP Flood)
		- Goal: Crash or slow down attacked host
- [Ping of death attack](https://en.wikipedia.org/wiki/Ping_of_death)
	- Sending ICMP Echo request packet that is larger than the maximum IP packet size
	- Attacked host can't reassemble the packet
	- Goal: Cause crash or reboot
- Teardrop attack
	- Using Teardrop to send IP fragments that can't be reassembled properly by manipulating the offset value of the packet
	- Goal: Cause reboot or crash
- DHCP starvation
	- Broadcast DHCP requests with spoofed MAC addresses to exhaust available address space
	- Set up rogue DHCP server and respond to new DHCP requests from hosts
	- Goal: Change network settings in hosts
- IPv6 fake router advertisements
	- Similar to rogue DHCP server
- Packet sniffing

---
links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]