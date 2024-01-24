tags: #osi

# Data Link Layer

links: [[604 SPA TOC - Layered Security]] - [[600 SPA MOC|Security Protocols and Applications MOC]] - [[000 Index|Index]]

---

## Data Link Layer

- Sends and receives frames between adjacent stations on the link
- Frames and addresses data
	- Encapsulates data packets into frames
	- Adds MAC address in frame header
- Provide error-free node-to-node connections and flow control
	- Error detection protocol: [Cyclic Redundancy Check (CRC)](https://en.wikipedia.org/wiki/Cyclic_redundancy_check)
	- Flow control based on [IEEE 802.3x standard (pause frames)](https://en.wikipedia.org/wiki/Ethernet_flow_control)
	- VLANs using Q-Tag in header
	- Flow control is often delegated to higher layers -> TCP
	- [Spanning Tree Protocol](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol) to avoid loops
- Mapping between network layer and data link layer
	- [Address Resolution Protocol (ARP)](https://en.wikipedia.org/wiki/Address_Resolution_Protocol)
- Network component: Switch
- Relevant topics: Ethernet, Switches (vs. Hubs), Spanning Tree, VLAN, ARP

### Vulnerabilities

- MAC address spoofing
	- NIC configured to use AMC address of another device
- VLAN circumvention
	- Configure NIC to tag traffic with a different VLAN ID to access different VLAN
- Spanning tree errors
	- Misconfiguration causing switch to be elected as root bridge leading to suboptimal traffic flow or loops
- Free connection or weak authentication and encryption to access links
	- Open wifi network allowing anyone to connect without password
- Wrong behaviour of network devices in overload situations
	- Switch dropping packets or providing inconsistent connectivity when at capacity

### Attacks

- Content-Addressable Memory (CAM) table overflow
	- CAM table contains MAC <-> Port Mapping and VLAN parameters
	- Attacker floods the switch with invalid-source MAC addresses
	- When the CAM table is full the switch starts behaving like a hub -> incoming packets are sent to all parts
- VLAN hopping
	- Attacker in VLAN 1 sending packets to VLAN 2
	- Tagging packets with different VLAN ID or behave like a switch and negotiate trunking
- Spanning-Tree Protocol manipulation
	- Spam network with topology change bridge protocol data units to force spanning-tree recalculation
	- Goal: Attacker becomes root bridge
- MAC address spoofing
	- Attacker sends packet with MAC address of attacked host to make switch overwrite CAM table
	- Attacker will receive data destined for attacked host until the attacked host sends a packet to the switch to rewrite CAM table again
- ARP attack
	- Attacker sends unsolicited ARP reply packets to attacked device
	- Attacked device updates ARP table which results in data being sent to the wrong device -> attacker
- [Private VLAN](https://kb.netgear.com/de/21618/Was-sind-private-VLANs-und-wie-funktionieren-sie-mit-meinem-Managed-Switch?language=de)
	- Promiscuous port: can communicate with all interfaces in VLAN
	- Community port: can communicate with all interface in community VLAN
	- Proxy can be used to circumvent restrictions

### Controls

- Disable / Shutdown unused switch ports
	- Prevent attacker from connecting to network
- Implement MAC address filtering
	- Restrict access to network to devices with approved MAC addresses
	- Counters CAM table overflow attack
- Do not use VLAN assignments to enforce secure design
	- to achieve secure isolation the networks should be physically isolated with policy engines (firewalls) in between
	- Mitigates VLAN hopping attack
- Use security enhanced network devices
	- IEEE 802.1X-2010 with port-based network access control
	- IEEE 802.11i-2004 WiFi protected access with WPA2
	- WPA3 with AES-GCM
- Use device built-in security features (encryption, authentication, MAC filtering)
- Use ARP / broadcast monitoring software
	- Identify unknown devices
	- Identify spoofed MAC addresses
- Use IPv6 [secure neighbor discovery (SEND)](https://en.wikipedia.org/wiki/Secure_Neighbor_Discovery)

---
links: [[600 SPA MOC|Security Protocols and Applications MOC]] - [[000 Index|Index]]