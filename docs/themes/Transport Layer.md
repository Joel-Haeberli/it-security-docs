tags: #osi

# Transport Layer

links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]

---

## Transport Layer

- Works in units of segments or messages
- Guarantees error free end-to-end connection / communication
- Provides a segmentation and reassembly of data streams
- Related topics: Client / Server principle, (segmentation) TCP, send receive buffer, TCP state machine, three-way handshake, UDP

### Vulnerabilities

- Different implementations of transport protocols allow fingerprinting
	- Different OS implement TCP/IP, UDP slightly different
	- Nmap can send various TCP/UDP packets and analyse the response to infer the OS
- Overloading of transport-layer mechanisms such as port numbers to effectively filter and qualify traffic
	- *GPT: If a server is running too many services a	- Sending ICMP Echo request packet that is larger than the maximum IP packet size accessible through different ports, it can become difficult to manage and secure all these ports. For instance, if a server is running HTTP on port 80, HTTPS on port 443, FTP on port 21, and several other services on other ports, it may not have the capacity to filter and monitor all the traffic effectively. An attacker might exploit a less secure service to gain unauthorized access to the server.*
- Transmission mechanisms can be subject to spoofing and attacks based on crafted packets and the educated guessing of flow and transmission values, allowing the disruption or seizure of control of communications
	- Example: SYN flooding
	- Goal: DoS, making system unresponsive to legitimate traffic because it's handing all the SYN requests
	- Forged packets / segments can be used to terminate or hijack connections

### Attacks

- SYN flooding
	- Caused by flaw in how most hosts implement the TCP three-way handshake
	- Host B receives SYN request from A
	- Host B adds partially opened connection in a "listen queue" (stored for 75 seconds)
	- "listen queue" is normally very limited
	- Host A sends lots of SYN requests but never replies to SYN&ACK from Host B
	- When "listen queue" on Host B is full, it won't accept any connections from other Hosts -> DoS
- Land Attack
	- Attacker sends forged TCP SYN packets with the same source and destination IP address and TCP port numbers
	- Victim system might crash or reboot
	- Can be mitigated with packet filtering
- UDP flood attack
	- Simply sending lots of forged UDP packets to victim
	- Victim will generate ICMP "destination unreachable" -> DoS
- Port scan attack
	- Sending a message to each port
	- Evaluate responses to see what services are available

### Controls

- Strict firewall rules limiting access to specific transmission protocols and subprotocol information such as TCP / UDP port number or ICMP type
	- For example only allowing Ports 80 and 443 on web server to mitigate against port scanning
- Stateful inspection at firewall layer, preventing out-of-state packets, "illegal" flags, and other phony packet profiles from entering the perimeter
	- Block TCP packets that initiate a connection without a SYN flag
	- Block TCP packets with unexpected flag combinations (SYN-ACK packet that comes before the SYN request)
- Stronger transmission and session layer identification mechanisms to prevent the attack and takeover of communications
	- Use mutual TLS where both the client and server authenticate each other before a connection is established

---
links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]