tags: #osi

# Attacks summary

links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]

---

### Layer 1: Physical Layer

1. **Tap Attack**: Unauthorized physical access to network cables or ports to intercept data, exploiting unsecured physical network infrastructure.
2. **RF Jamming**: Deliberately sending radio frequency signals to disrupt wireless network communications, exploiting the nature of shared wireless medium.
3. **Physical Destruction**: Damaging or destroying physical components of a network (e.g., routers, switches, cabling), exploiting the physical vulnerability of network hardware.

### Layer 2: Data Link Layer

1. **ARP Spoofing**: Attacker sends fake ARP (Address Resolution Protocol) messages to link their MAC address with the IP address of another host, exploiting the lack of authentication in ARP protocols.
2. **MAC Flooding**: Overwhelming the switch's MAC table by flooding the network with frames with unique MAC addresses, exploiting limited size of MAC address tables in switches.
3. **VLAN Hopping**: Exploiting switch misconfigurations to send traffic from one VLAN to another unauthorized VLAN.

### Layer 3: Network Layer

1. **IP Spoofing**: Creating IP packets with a forged source IP address to conceal the sender's identity or impersonate another computing system, exploiting the lack of authentication in the IP protocol.
2. **Routing Attack**: Compromising network routers to disrupt or reroute network traffic, exploiting vulnerabilities in routing protocols.
3. **Ping of Death**: Sending malformed or oversized packets to crash, freeze, or reboot the target machine, exploiting the handling of fragmented packets.

### Layer 4: Transport Layer

1. **SYN Flood**: Overloading a server by initiating a large number of TCP connections but not completing the handshake, exploiting the TCP three-way handshake.
2. **Session Hijacking**: Taking over a web user's session by stealing or predicting a valid session token, exploiting the stateful nature of TCP connections.
3. **UDP Flood**: Flooding the target with UDP packets, leading to denial of service, exploiting the stateless nature of UDP.

### Layer 5: Session Layer

1. **Man-in-the-Middle Attack**: Intercepting communication between two parties and possibly altering the communication, exploiting non-encrypted session establishment.
2. **Session Fixation**: An attacker fixes a user's session ID before the user logs in, then hijacks the user's authenticated session, exploiting the vulnerable session management.
3. **Cross-Site Request Forgery (CSRF)**: Tricking a victim's browser into sending unauthorized commands to a website, exploiting the website's trust in the user's browser.

### Layer 6: Presentation Layer

1. **SSL Stripping**: Downgrading a secure HTTPS connection to an unsecured HTTP connection, exploiting the client's ability to handle multiple types of connections.
2. **Compression Ratio Info-leak Made Easy (CRIME)**: Exploiting the compression mechanism of SSL to extract secure data, particularly cookies.
3. **Character Encoding Attacks**: Manipulating character encoding to bypass input validation checks, exploiting weaknesses in data representation and encoding.

### Layer 7: Application Layer

1. **SQL Injection**: Inserting or "injecting" a SQL query via input data from the client to the application, exploiting poor input validation.
2. **Cross-Site Scripting (XSS)**: Injecting malicious scripts into web pages viewed by other users, exploiting the trust a user has for a particular site.
3. **DNS Hijacking**: Redirecting queries to a fraudulent domain name server, leading users to malicious websites, exploiting vulnerabilities in DNS services.

---
links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]