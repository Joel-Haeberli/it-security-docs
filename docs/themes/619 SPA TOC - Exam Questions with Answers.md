tags: #web #network #security-tool #security-protocol   

# SPA TOC - Exam Questions with Answers

links: [[600 SPA MOC|SPA MOC]] - [[themes/000 Index|Index]]

---
## Part 1

### Topic 1: Information Security

1. What is meant with Information Security?
2. What are the goals of Information Security?
3. What are older terms for Information Security?
4. Whats an information asset?
5. Who is responsible to protect information assets?
6. What is an ISMS?
7. Do you now Information Security Standards? Which?
8. What are Risks?
9. What are Security Controls?
10. Do you know some important Security Controls? Explain them.
11. What's the job of a Security Professional?
12. Which Security Controls should be implemented immediate if no other controls are in function (e.g., according to the NSA)?
13. What do the acronyms CIA and AAA in connection with Information Security mean?
14. Are you able to explain the meaning of the abbreviated words?
15. What is an "information security incident"?
16. What is the difference between an "information security event" and an "information security incident"?
17. What are the goals of "security incident management"?

### ✅ Topic 2: Hacking Basics

1. Recently, there were more and more cyber security attacks against critical infrastructures. What is a critical infrastructure? Provide some examples. What are the targets of such attacks?
     - Power grid
	* Airport
	* Harbour
	* Railway
	* Hospital
	* Core router
	* DNS root NS
	* Cloud Provider
	* Attacks against those often target industrial control systems (ICS) such as supervisory control and data acquisition (SCADA) systems.
2. From where do external attackers (outside attackers, remote attackers) attack networks and computers?
     - Can attack from the internet, wireless network or via a physical break-in
3. Do you know some intrusion techniques? Can you explain these techniques in detail?
     - Physical intrusion
     - Through Software bugs
     - Through configuration bugs
     - Through design flaws
     - Through weak passwords
4. List known vulnerabilities of systems. Can you explain these vulnerabilities in more details.
     - Buffer Overflow
     - Unpatched Software
     - Insecure APIs
     - Misconfiguration
     - Weak Authentication
5. What authentication methods do you know?
     - Password-based
     - Two-Factor
     - Biometric
     - Token-based
     - Certificate-based
     - Challenge and Response-based (FIDO)
6. List and explain the five stages / phases of an intrusion into a system.
	1. **reconnaissance** (appearing as a normal user, hard to detect)
	2. **scanning** (ICMP scan, Port scan, identify OS and software)
	3. **running exploits** (exploit a vulnerability that was found, you cross the line here)
	4. **establish a foothold** (hide evidence, rootkit installation, replace services, hack other systems from here)
	5. **playing for profit**
7. Do you know "shortcuts" to the five stages / phases of an intrusion?
     -  Use automated tools for scanning and break in
	* Create fake websites to harvest credentials
	* Infect vulnerable websites with malware
	* Scam mails and messages for social engineering
	* Or directly by phone, as a fake support agent

### Topic 3: Layered Security

1. Do you know layer specific vulnerabilities (vulnerabilities, which occur on one of the seven layers of the ISO / OSI network reference model)?
2. Can you explain countermeasures?
3. Which vulnerability is the most critical?

### ✅ Topic 4: Host and Network Security

1. **What are well known computer-based security mechanisms (Host-based security mechanisms)?**
	- os hardening/updating, host firewall, host IDS/IPS, virus scanner, endpoint security, SIEM
2. **What are well-known network-based security mechanisms?**
	- network firewalls (subnets, segments, zones) against external attackers
	- access control against internal attackers (network IDS/IPS, network access control)
	- SIEM
3. **What are capabilities of network firewalls?**
	- connect two or more network segments
	- control, log, modify (mangle), filter packages
4. **What are limitations of network firewalls?**
	- cannot protect against internal attackers
	- malware which came in through applications
	- secured/tunneling connections (IPsec, SSH, TLS)
5. **Which other terms are used for network layer firewalls?**
	- packet filters
6. **Explain briefly the operation of network layer firewalls.**
	- checking of header entries (L2, L3, L4), has to reassembling fragmented packages to analyse all headers
7. **Which protocol header fields are usually evaluated by a packet filter?**
	- L2 (MAC): source/destination, ethertype (`0x0800` IPv4, `0x0806` ARP, `0x086DD` IPv6, `0x8100` VLAN), tag protocol identifier (VLAN 802.1Q) 
	- L3 (IP): source/destination, protocol/next header (`1` ICMP, `6` TCP, `17` UDP)
	- L4 (ICMP): control messages (`0/0` Echo Reply, `3/X` Destination unreachable, `8/0` Echo Request, `11/X` Time Exceeded)
	- L4 (TCP): source/destination port, sequence number, connection establishment (`SYN`, `SYN-ACK`, `ACK`, `FIN`, `RST`, ...)
	- L4 (UDP): source port/destination
8. **What is a stateful inspection firewall?**
	- Recording state information of connections and modify filter rules dynamically to accept expected answer packets
9. **What is meant by "deep inspection"?**
	- do stateful packet inspection (SPI) by analyzing and modifying the application layer content $\rightarrow$ no only inspecting basic header fields, inspecting actual data payload. important for identifying malware or application-layer attacks
10. **What are the features of a "Next Generation Firewall"?**
	- can apply configuration modifications without interruptions
	- has an integrated IPS
	- provide application intelligence
	- can consider external sources in rules (e.g. allow-/blocklists of IP addresses)
11. **Explain the term "Unified Threat Management UTM"**
	- Can perform multiple security functions within one single appliance:
		- firewall
		- IDS/IPS
		- antivirus
		- anti-spam
		- content-filtering
		- VPN
12. **What's the intention of threat protection firewalls? How do they work?**
	- Enhancement of Next Generation Firewall
	- Can detect malicious content/code (executing content in sandbox environment, behavioral analysis)
	- Protection against APTs
13. **What's an advanced persistent threat (APT)?**
	- An Advanced Persistent Threat (APT) is a highly sophisticated and targeted cyberattack in which malicious actors gain unauthorized access to a network or system and remain undetected for an extended period. APTs are characterized by their persistence, often involving well-funded and organized attackers, making them difficult to detect and mitigate.
14. **What is an application layer firewall? How does it work?**
	- Unpack an analyze the content of the application layer protocol
	- act as a relay station or proxy between sender and recipient
	- allow authentication and authorization on user level
	- referred to as application layer gateway, proxy server, application firewall
15. **How do proxy servers work, what are non-/transparent proxy servers?**
	- MITM for protocol specific traffic (HTTP, DNS, ...)
	- *Non-Transparent proxy servers*: sender must send the packets directly to the proxy server, configuration inside the application/host system
	-  Transparent proxy servers: transparent for client, no configuration needed
16. **What are "Web Application Firewalls" for?**
	- special case of an application layer firewall
	- protect web applications against attacks over HTTP/S (Injection, tampering, cookie poisoning, buffer overflow attack, unauthorized access)
17. **Which basic firewall architectures do you know?**
	- Screened Host: Access from Internet only to services on one host. Host has access to intranet (be aware!)
	- Screened Subnet: Firewall $\leftrightarrow$ Host $\leftrightarrow$ Firewall $\leftarrow$ Internet access (additional firewall before Intranet)
	- Dual Homed Host: "All in one firewall" instead of two firewalls
	- Tri- & Multi Homed Host: multiple network zones with one firewall (DMZ)
18. **What are scurity zones?**
	 - **Security Zones** are segments within a network infrastructure that have distinct levels of security controls. They separate and manage access between different parts of the network based on security requirements. Common examples include public-facing areas (like DMZs), internal networks, sensitive data zones, and isolated environments for critical systems.
19. **You enable the access to an internal web server through your home router / firewall via port forwarding. Which firewall architecture corresponds to this setup? What dangers does it offer?**
     - **Setup**: Enabling access to an internal web server through a home router or firewall via port forwarding.
     - **Architecture**: This setup typically corresponds to a Packet-Filtering Firewall architecture.
     - **Dangers**:
	    - Exposes the internal server to the Internet, potentially to malicious traffic.
	    - If the server has vulnerabilities, it can be exploited.
	    - Increases the risk of attacks like port scanning, brute force, or exploiting server-specific vulnerabilities.
20. **What are advantages/disadvantages of a IDS/IPS?**
    - **Advantages**:
	    - Detect and potentially prevent a wide range of attacks.
	    - Provide visibility into network traffic patterns.
	    - IDS can alert on suspicious activities without affecting network performance.
	- **Disadvantages**:
	    - False positives/negatives can occur, leading to unnecessary alerts or missed threats.
	    - IPS can inadvertently block legitimate traffic.
	    - Require regular updates and management to stay effective against new threats.
21. **Explain the term "endpoint security"**
    - Refers to securing endpoints or entry points of end-user devices like desktops, laptops, and mobile devices from being exploited by malicious actors. It involves technologies, processes, and strategies to protect devices connected to the corporate network.
22. **What's the function of an SIEM?**
    - Provide real-time analysis of security alerts generated by applications and network hardware. They aggregate and analyze log data, providing centralized reporting and alerting on security incidents, thereby aiding in incident detection and response.
23. **Explain the "Zero Trust" approach to improve network security**
    - Security concept centered on the belief that organizations should not automatically trust anything inside or outside its perimeters. Instead, they must verify anything and everything trying to connect to its systems before granting access. It involves continuous authentication, least-privilege access, micro-segmentation of networks, and prevents unauthorized access to data and services.

### Topic 5: Linux firewall (netfilter / iptables / nftables)

1. Explain the structure of "netfilter (-hooks)"
2. Which are the predefined rule chains of "netfilter" / "iptables"?
3. Can you draw a schema of the rule chains in the filter table? Where do they have an effect?
4. What is the "nat" table of "netfilter" / "iptables" for?
5. Which predefined rule chains belong to the "nat" table?
6. What is the structure of a rule in an "iptables" chain?
7. What happens, if a rule matches/does not match a packet?
8. Which predefined targets are known with "iptables" and what do they do?
9. Do you know some "match/target extensions" and their work?
10. What ist the purpose of the match extension "state"/"conntrack" of iptables?
11. What states of connections can be checked by iptables using the match extension "conntrack"?
12. How can packets be marked for further processing?
13. Which kind of processing can be done?
14. Explain presented iptables/nftables rules or rule chains.
15. Why is "nftables" more flexible then "iptables"?
16. What are the main differences between "nftables" and "iptables"?
17. What happens with my "iptables"-rules if "nftables" is deployed?
18. Explain what the presented "nftables" firewall does (e.g., lab sample solutions).

### Topic 6: DNSSEC and DNS privacy

1. Why is DNSSEC used? What problem does it solve?
2. What is the purpose and function of a validating resolver?
3. What are the new DNSSEC Resource Records? What are they for?
4. What is the purpose of the RRSIG/DNSKEY/NSEC/DS RR? Explain how they work.
5. What is a Resource Record Set (RRSet) and where is it used?
6. What problem is caused by the NSEC RR? How can it be solved?
7. What is the purpose of the Zone Signing Key ZSK?
8. What is the purpose of the Key Signing Key KSK?
9. How are DNS entries validated on a validating resolver?
10. How does the Chain of Trust for DNSSEC work?
11. What response does a client receive if the resolver used cannot validate a response?
12. What is the purpose of the AD or the CD flag in the DNS protocol header?
13. Explain use cases for DNSSEC such as SSHFP or DANE?
14. Do you know methods to improve the confidentiality and privacy of DNS communication?
15. Explain mechanisms/protocols that ensure the confidentiality of DNS transactions.
16. How can DoT be implemented on a DNS resolver (which does not support it natively)? 

### Topic 7: DNS RPZ

1. What is a Response Policy Zone (RPZ) and how does it work?
2. What do you use RPZs for?
3. How do you get valuable RPZ information?
4. What responses can a resolving name server respond to a client out of a RPZ?
5. How can you block/redirect access to "badhost.baddom.com" using RPZ?

### Topic 8: Tools

1. Why is a centralized logging important? How can it be done?
2. What is a syslog facility and a syslog severity?
3. Which tools can you use to capture traffic?
4. How do vulnerability scanners work? Can they find every vulnerable system?
5. What is nmap for? What is a stealth scan?
6. What is "netflow" or "IPFIX"? How does it work and why is it an important mean to rise host and network security?
7. Explain an ARP MITM attack. What are countermeasures?
8. What is the purpose of "arpwatch"?
9. Why and when is SNMP dangerous?
10. How do you capture packets of a DNS request / response on Interface "eth0" using "tcpdump"?

### ✅ Topic 9: Lab Exercises

1. **How can a centralized syslog be implemented?**
	  - A centralized syslog can be implemented using a syslog server that collects logs from multiple devices. Syslog clients on these devices are configured to send their log data to this central server. This centralization aids in efficient log management, monitoring, and analysis.
1. **Explain how you tested arp spoofing, did it work?**
     - ARP spoofing was tested by creating false ARP messages and observing the redirection of network traffic. By associating the attacker's MAC address with the IP address of another host (like a gateway), all traffic meant for that IP was redirected to the attacker, confirming the success of the ARP spoofing.
3. **What does a specific "iptables" or "nftables" firewall rule do (see also the provided sample solutions)?**
     - Each rule in "iptables" or "nftables" specifies conditions for packet matching and decides what action to take when a packet matches these conditions. For example, a rule can be set to drop packets from a specific IP address, effectively blocking access.
4. **How do you redirect traffic to a filtering proxy using "iptables" or "nftables"?**
     - In "iptables" or "nftables", you can redirect traffic to a proxy server by setting up NAT (Network Address Translation) rules that reroute incoming or outgoing traffic to the proxy's IP address and port. This is commonly used for web filtering or caching.
5. **Which criteria did you use for your filtering proxy?**
     - For Squid, criteria can include URL patterns, IP addresses, or protocols. For example, you might configure Squid to block all access to certain websites or to only allow browsing during specific hours.
6. **Which means do you know to explore networks?**
     - Network exploration can be done using tools like Nmap for port scanning, Wireshark for packet analysis, traceroute for path tracking, and network mapping tools that visualize network topology.
7. **Which vulnerability scanner was used in the lab excercises?**
     - In the lab, Greenbone OpenVAS was used. It's a comprehensive vulnerability scanning tool that helps in identifying vulnerabilities in network services and software.
8. **What data of your router can you analyze using "nfsen"?**
     - "nfsen" allows you to analyze network flow data from your router. It can display traffic patterns, bandwidth usage, and type of traffic (e.g., HTTP, FTP) over time, aiding in network monitoring and troubleshooting.
9. **What ist "softflowd" and how can it be used to export flow data?**
    - "softflowd" is a flow-based network traffic analyzer. It can be used to export flow data from network interfaces, tracking various aspects of traffic like source/destination IP, ports, and protocols.
10. **Explain how "softflowd" and "nfcap/nfsen" interact.**
	  - "softflowd" captures flow data from network traffic and exports it in a format compatible with "nfcapd", a collector component of "nfsen". "nfsen" then uses this data for analysis, visualization, and reporting.
11. **Which security distibutions where used in the lab? Explain their main focus.**
	  - Kali Linux was used, which is a distribution designed for digital forensics and penetration testing. It comes with numerous tools for network analysis, vulnerability scanning, and security auditing. Its main focus is to provide a comprehensive suite for cybersecurity professionals to test network defenses and security measures.
## Part 2

### ✅  TLS

1. **Name 5 protocols based on TLS.**
	- HTTPS, FTPS, SMTPS, LDAPS, DTLS
   
2. **What is meant with «Opportunistic TLS»? What is meant with «implicit TLS»? What kind of risks / attacks do you know?**
	- Opportunistic TLS: Refers to a system that uses TLS encryption if available but can fall back to an unencrypted connection if TLS isn’t supported by the other party. It's often used in email transmission. The risk is that it can be subject to downgrade attacks, where an attacker forces the connection to revert to an unencrypted state.
	- Implicit TLS: In this mode, TLS is a mandatory part of the connection from the start (as opposed to being negotiated with STARTTLS). The connection starts with the TLS handshake, and no unencrypted communication is permitted. It is considered more secure than opportunistic TLS as it doesn’t allow falling back to an unencrypted connection.

3. **What does «HTTP Strict Transport Security» (HSTS) stands for? How is it supposed to work? Describe the OSI layer in general and where the TLS communication takes place.**
	- HSTS is a web security policy mechanism that helps to protect websites against protocol downgrade attacks and cookie hijacking. It allows web servers to declare that web browsers (or other complying user agents) should only interact with it using secure HTTPS connections, and never via the insecure HTTP protocol.
	- In the OSI model, HSTS operates at the application layer (Layer 7), where it instructs the browser on how to handle connections to the server. The TLS communication itself occurs at the session layer (Layer 5) and the presentation layer (Layer 6), where it provides privacy and data integrity between two communicating applications.
   
4. **TLS is composed of the handshake protocol and the record protocol. Describe what happens on each layer?**
	- Handshake Protocol: This part of TLS is responsible for the initial negotiation between client and server. It establishes which cryptographic algorithms will be used, authenticates the server (and optionally the client), and sets up a secure encryption key.
	- Record Protocol: Once the handshake is complete, the Record Protocol is used to secure the actual data being transmitted. It uses the encryption key established during the handshake to encrypt the data and ensures that it is transmitted securely and intact.

5. **What information do we find in a «Client Hello» message?**
	- Protocol Version: The highest TLS version supported by the client.
	- Random: A client-generated random string used for key generation.
	- Session ID: An identifier to resume previous sessions for faster handshakes.
	- Cipher Suites: A list of cryptographic algorithms supported by the client.
	- Compression Methods: Information about the compression methods available.
	- Extensions: Optional additional features like server name indication (SNI) or maximum segment size.

6. **What information contains the CipherSuite such as TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (128-bit AES encryption with SHA-256 message authentication and ephemeral ECDH key exchange signed with an RSA certificate)?**
	- TLS: Indicates the protocol is TLS.
	- ECDHE (Elliptic Curve Diffie-Hellman Ephemeral): Specifies the key exchange mechanism using ephemeral keys with Elliptic Curve cryptography for secure key agreement.
	- RSA: Indicates the use of RSA for digital signatures and certificate verification.
	- AES_128_CBC: Specifies the encryption algorithm (AES) with a 128-bit key size, using Cipher Block Chaining (CBC) mode.
	- SHA256: Indicates the use of the SHA-256 algorithm for message authentication and integrity verification.
	  
7. **How does a TLS mutual authentication works? Which additional handshake messages are exchanged?**
	- In TLS mutual authentication, both client and server authenticate each other. This is usually done in environments where security requirements are higher.
	- Additional Handshake Messages: In addition to the standard TLS handshake messages, both the client and server present certificates. After the server sends its certificate, the server requests the client's certificate (CertificateRequest), and the client responds with its certificate (Certificate). The client then sends a CertificateVerify message to prove ownership of the private key associated with the certificate.
   
8. . **How does a TLS resume session looks like. What are the prerequisites? What is a anonymous TLS session such as TLS_ECDH_anon?**
	 - TLS session resumption is a mechanism to speed up repeated TLS connections between the same client and server. Prerequisites: A previously established TLS session with agreed-upon session keys and a session ID or session ticket. In a resumed session, the client and server use the session ID or session ticket from a previous session to skip the full handshake and quickly re-establish encryption keys. Anonymous TLS Session (e.g., TLS_ECDH_anon): These are TLS sessions that do not authenticate one or both parties. They use ECDH for key exchange without RSA or other certificate-based methods. These sessions are vulnerable to man-in-the-middle attacks as they lack authentication.
   
9. **What does the term Forward Secrecy stands for. What has to be done to get perfect forward secrecy (PFS)?**
	- Forward Secrecy (FS), or Perfect Forward Secrecy (PFS), refers to a property of secure communication protocols where session keys cannot be compromised even if the private key of the server is compromised in the future.
	- Achieving PFS: This is typically done by using ephemeral key exchange mechanisms (like Diffie-Hellman or ECDHE) where a new key pair is generated for each session and not based on a static server key.

10. **What do you have to do respectively think off to implement a TLS reverse proxy for a company?**
    - Certificate Management for the proxy, protocol and cipher configurations for TLS, secure communication between the proxy and internal servers, logging and monitoring and compliance and policy enforcement.
    
11. **What is a bit flipping attack? Which ciphers are vulnerable?**
    - A bit flipping attack is a form of cryptographic attack where the attacker changes bits in the encrypted message in a predictable way to manipulate the decrypted plaintext. This type of attack is typically used against cipher modes like CBC (Cipher Block Chaining) where alterations in one block can predictably affect the decryption of subsequent blocks.
    - Ciphers Vulnerable: Cipher modes that do not authenticate message integrity, such as CBC, are particularly vulnerable to this attack. This vulnerability led to the development of authenticated encryption modes like GCM (Galois/Counter Mode) that combine encryption and message authentication.
    
12. **What information do you need to inspect and decipher all TLS packets e.g. with wireshark (TLS private key corresponding to the server certificate, pre-master key, master key)?**
    - If using traditional RSA key exchange, having the server's private key allows you to decrypt the session. For sessions using Diffie-Hellman key exchange, you need the pre-master key or master key, as these sessions cannot be decrypted using just the server's private key.
    
13. **What information is exchanged with Diffie-Hellman key exchange in a TLS session? Describe which information is used for a JA3 fingerprint?**
    - This exchange involves each party sending a public value (computed from their private value and a common base) and then combining their private value with the received public value to compute a shared secret. JA3 Fingerprint: It's a method to fingerprint SSL/TLS clients based on specific details of their TLS handshake process. This includes the TLS version, accepted cipher suites, list of extensions, elliptic curves, and elliptic curve point formats.
    
14. **How is the master secret derived for the pre-master secret?**
    - In a TLS handshake, the master secret is derived from the pre-master secret through a secure hashing process. This involves using a pseudo-random function (PRF) that combines the pre-master secret with nonces (random numbers) from both client and server, plus a string literal. The result is a master secret that is then used to generate encryption keys, MAC (Message Authentication Code) keys, and initialization vectors.
    
15. **Describe how a HMAC function works.**
    - HMAC is a type of message authentication code (MAC) that uses a cryptographic hash function (like SHA-256) combined with a secret key. It works by applying the hash function in two steps: The key is combined with the message and hashed. The hash output is then combined with the key again and re-hashed. This process provides both data integrity and authentication of the message. HMAC ensures that the message has not been altered and that it was sent by a holder of the secret key.
    
16. **What is meant with «Authenticated Encryption» (AE)?**  
    - Authenticated Encryption refers to encryption methods that ensure both confidentiality and integrity of the data.
    
17. **What is the difference between AE and AEAD (Authenticated Encryption Associated Data)?** 
    - While Authenticated Encryption (AE) ensures data confidentiality and integrity, Authenticated Encryption with Associated Data (AEAD) goes a step further by also protecting additional associated data's integrity (but not its confidentiality). This associated data is typically header or other metadata.
    
18. **Describe a «Padding Oracle Attack».**
    - This is an attack method on cryptographic systems where the attacker makes use of a 'padding oracle' - a side channel giving them hints about whether a given decryption attempt was correct based on the padding's validity. The attacker can iteratively guess and decrypt data, exploiting the way some encryption algorithms handle padding.
    
19. **Describe a «Padding Oracle On DOwngradeD Legacy Encryption» (POODLE) attack.** 
    - Padding Oracle On Downgraded Legacy Encryption (POODLE) is a security vulnerability that exploits the fall-back to SSL 3.0 in TLS. When a secure connection attempt fails, a server might fall back to older protocols like SSL 3.0. POODLE can force this downgrade and then use padding oracle attacks (exploiting SSL 3.0's vulnerabilities) to decrypt sensitive data like cookies.
    
20. **Describe the changes between TLS 1.2 and TLS 1.3 in respect of: Key exchange, Cipher suites, Round trip time, Authenticated Encryption , Authentication / Signature**
    - Key Exchange: TLS 1.3 removes RSA key exchange for forward secrecy, focusing on Diffie-Hellman and ECDH (Elliptic Curve Diffie-Hellman) instead.
	- Cipher Suites: TLS 1.3 streamlines cipher suite negotiation, supporting only AEAD cipher suites. It removes many older cipher suites and hashing algorithms, increasing overall security.
	- Round Trip Time: TLS 1.3 reduces the number of round trips (handshake messages exchanged between client and server) needed to establish a secure connection, making the handshake process faster.
	- Authenticated Encryption: TLS 1.3 mandates the use of AEAD ciphers for encrypting and authenticating all data, ensuring better security and efficiency.
	- Authentication/Signature: TLS 1.3 improves the way certificates are authenticated and signed, requiring digital signatures even when a previous session is resumed. This enhances the overall security of the authentication process.

### Certificates and PKI

1. What is defined in PKCS#1, PKCS#7, PKCS#10, PKCS#11, PKCS#12?
2. What is the life cycle of a X509 certificate?
3. What protocols do you know to check the status of a certificate (CRL-DP, OSCP)? Describe them.
4. What is a Extended Validation SSL (EV SSL) certificate?
5. What problems are addressed with the «Certificate Transparency» (CT) standard?
6. How does CT works? Where is it implemented? Who is enforcing checks?
7. Which components and processes are required for a PKI?
8. How to you generate a «Certificate Signing Request» (PKCS#10)? What attributes are checked by the RA?
9. What are «Advanced Digital Signature» (AdES) and «Qualified Electronic Signatures» (QES). Who can issue such certificates in Switzerland?

### Identification Authentication Authorization

1. What is Identification, Authentication and Authorization?
2. What factors are distinguished for authentication? What is required for 2FA / MFA?
3. What is meant in the PSD2 regulation with «strong authentication with linking»?
4. What hat to be met to get a high «Level of Assurance» (LoA)?
5. What can go wrong with shared secrets? How should you store credentials used for password based authentication?
6. Describe «online» and «offline» attacks against passwords.  
7. How do you calculate the Entropy of a password?  
8. How is the password transferred with «HTTP Basic Authentication»?  
9. How does the OATH standard HOTP (HMAC-based One Time Password) works?  
10. How does the OATH standard TOTP (Time-based One Time Password) works?  
11. What is a Challenge-Response-Protocol and why do we need it?  
12. FIDO2 consists of the standards WebAuthn and CTAP. Describe the function of the two standards.
13. What is meant with attestation?
14. What information / LoA do we get with a FIDO2 registration with a YubiKey? 
15. What does the Relying Party (RP) need for verifying the attestation?
16. What communication protocols are supported by CTAP? What options are displayed when resisting on a FIDO2 page with an Android device?
17. What is needed to access resources over OAuth from a «Resource Server»?
18. What is a «bearer token»?
19. Describe the trust relations between the 4 parties: resource holder, client, authentication server and resource server.
20. What kind of CSRF attack would be possible if the client would not check the session state? 
21. How can a resource holder revoke his consent?
22. Outline how you can use «OpenID Connect» as authentication layer. What is the benefit. How are the trust relations?
23. Outline how you can leverage OAuth as Identity Provider interface. 
24. On what security mechanism is OAuth relying on?

### ✅  Secure Email

1. **How does the email routing works?**
	- Mails are sent via SMTP, the MX record specifies the mail server responsible for a domain name. By sending a mail, the MTA queries DNS for the MX record for the recipient's domain name (lowest-numbered records are the most preferred).
	- MUA $\rightarrow$ MSA $\rightarrow$ Sender's MTA $\rightarrow$ Receiving MTA $\rightarrow$ (multiple hops) $\rightarrow$ MDA $\leftarrow$ only authenticated MUAs can access emails via POP3 or IMAP.
2. **RFC 8314 introduces Transport Layer Security (TLS) for Email Submission and Access. What security concerns are addressed?**
	- Confidentiality and integrity of email content during transit (no E2E encryption!), protects user credentials from eavesdropping when clients authenticate to email servers, mitigates MITM attacks by authentication email servers to client
3. **Explain what information the «Email envelop» contains (RFC 5321) and what information «Internet Message Format» (RFC 5322) contains?**
	- SMTP envelope: Sender and recipient information used for routing and delivery (MAIL FROM, RCPT TO)
	- Internet Message Format:
		- Mail Header (From, To, Subject, Date, DKIM, ...)
		- Mail Body
4. **What information can be found in the «mail header» which fields are mandatory?**
	- Required: origination date field (Date) and the originator from (From)
	- Common: To, Subject, Message-ID, CC, BCC, Received (trace fields), ...
5. **SMTP originally (RFC821) only allowed 7-bit encoding. What encodings do you know to circumvent this limitation?**
	- MIME supports Base64 and Quoted-Printable encoding
6. **How can you sent signed and encrypted emails (PKCS#7)?**
	- Use MIME type `application/pkcs7-mime` and sign or encrypt mail with certificates (pk infrastructure)
7. **What is the difference between a «Detached Signatures» (application/pkcs7-signature) and a regular PKCS#7 signature (application/pkcs7-mime)?**
	- *Detached Signature*: The signature is stored separately from the original data. This allows recipients to verify the signature without altering the original message format $\rightarrow$ if a mailing list modify email parts, the signature isn't valid anymore.
	- *Regular PKCS#7 Signature: The signature and the original data are bundled together in a single file. This is more convenient for ensuring both the data and its integrity are preserved together, but it alters the original message format.
8. **Describe how a PKCS#7 message is encrypted for a group of recipients. How is the PKCS#7 encrypted data (pkcs7-envelopedData) structured?**
	- The message is encrypted once using a symmetric key.
	- Each recipient's public key encrypts the symmetric key.
	- The PKCS#7 structure contains the encrypted message, a per-recipient encrypted symmetric key, and encryption algorithm details.
9. **How can you authenticate the origin of an email message (SPF, DKIM, DMARC)?**
	- SPF: erifies the sender's IP address against the domain's published SPF record in DNS.
	- DKIM: Uses a digital signature, linked to the sender's domain, that is verified against a public key in the domain's DNS records.
	- DMARC: Leverages SPF and DKIM authentication results, specifying how receivers should handle failed emails and providing reports on email sources and failures.
10. **What problems tries the Sender Policy Framework (SPF) to address? On what address (RFC5321.MailFrom) is the policy based on?**
	- SPF addresses Email Spoofing (unauthorized senders) and Spam/Phishing (verify sender authenticity). SPF policy is only based on the RFC5321.MailFrom (SMTP envelope) and thus can be bypassed by Spammers.
11. **Describe a typical SPF entry (e.g. from bfh.ch). Where do we find the entry and what information does it contain?**  
	 - The SPF record can be found in DNS as TXT record (`dig bfh.ch TXT`), for an example see [[Email Authentication#Examples|here]]
12. **Describe problem cases respectively scenarios where SPF will fail.**
	- *Email Forwarding*: if an email is forwarded by an intermediate server, the sender's IP may no longer match the SPF record (e.g. Mailing list)
	- RFC5321.MailFrom (SMTP envelope) can be overwritten by a Mailing list or Spamer to generate an SPF pass
	- Many receivers do not act on SPF's policy assertion (misconfiguration, unclear implementation like "softfail")
13. **Which problem addresses the Domain Keys Identified Messages (DKIM) standard?**
	- DKIM addresses the problem of email tampering and sender identity verification. It ensures that an email's content and sender can be authenticated and have not been altered or forged during transit.
14. **How is DKIM designed. What do you need for implementing DKIM?**
	- *Digital Signatures*: the email gateway sign all outgoing emails with a private key
	- *Public Key in DNS*: the public key is published as an DNS TXT record
15. **Describe a typical DKIM entry found in the mail header. What information does it contain?**
	- Version (v=1), Algorithm (rsa-sha256), Domain (d=example.com), Selector (s=selector1, specific public key), Signature Data (b=signature), Signed Headers (h=from:to:date)
16. **Where do we find the DKIM key? What types / formats of keys are used?**
	- The key is in the sender's domain DNS record. RSA is mostly used ed25519 is supported too.
17. **Describe the relationships of DKIM key location (domain), RFC5322.From, RFC5321.MailFrom to DKIM.**
	- The signing domain does not have to have any relationship to the domains in the RFC5322.From (Mail Header) or RFC5321.Mail From (SMTP Envelope)
18. **Which steps are involved verifying a DKIM signature? What can go wrong?**
	- more complicated to deploy than SPF
	- does not verify if the signed parts of the message are altered (which happens often, e.g. mailing lists, corporate gateways adding a header, etc.)
	- crypto concerns need to be tracked (key length, hashing algorithms)
19. **Describe the functions of ARC-Authentication-Results (AAR), ARC-Message-Signature (AMS) and ARC-Seal (AS)? Who is adding these mail headers?**
	- ARC headers are added by intermediate email servers to solve altering headers and provide valid signatures
	- *AAR*: checks for SPF, DKIM, DMARC
	- *AMS*: added by the server that performs the ARC signing, signature of entire message except for the ARC-Seal headers
	- *AS*: signature of the previous ARC-Seal headers, validity of the prior ARC entries
20. **What problems is DMARC addressing?**
	- DMARC addresses email spoofing, fraud, and unauthorized domain use by allowing domain owners to specify authorized email sources and policies for handling failed emails. It provides visibility through reporting on email authentication.
21. **Describe a typical DMARC entry (e.g. from ubs.com). Where do we find the entry and what information does it contain?**
	- DMARC entries are published in DNS TXT records
	- Version, Policy (p=reject/quarantine/none), Alignment (adkim=strict/relaxed), Reporting (rua=mailto:dmarc@example.com)
22. **On what address is DMARC based on (RFC5322.From)?**
	- DMARC operates on RFC5322.From address (Mail Header)
23. **What is the alignment to the DKIM and SPF record?**
	- Alignment in DMARC can be strict or relaxed, and it checks whether the domains in DKIM signatures or SPF records match the RFC5322.From domain. Strict alignment requires an exact match, while relaxed alignment allows for subdomain matches.
24. **Where is DMARC policies verification enforced? How can you check the effect of your DMARC policies?**
	- DMARC policies are enforced by email receivers (servers) that validate incoming emails against the policies set by the sending domain. To check the effect of your DMARC policies, send test emails to services like Gmail and configure your DMARC record to receive reports.
25. **What are the options if the DMARC verification fails?**
	- None (monitor), Quarantine (move mails in quarantine or spam folders), Reject (reject email)

### Kerberos

1. How does Kerberos works? Why does Kerberos need shared secrets? What are these shared secrets?
2. The Key Distribution Center (KDC) is composed of the Authentication Server (AS) and the Ticket Granting Server (TGT). What is the function of AS and TGT?
3. What is a Server Principal Name (SPN)? How is the name composed / structured?
4. Explain the content and the function of Kerberos Tickets? What is a Ticket Granting Ticket (TGT) and what is a service ticket (ST)? Explain the differences.
5. Explain the differences between «secret keys» and «session keys».
6. How does the Kerberos Pre-authentication works?
7. What is needed to decrypt all messages / tickets in Wireshark?
8. What type of attacks are referred as «Golden Ticket» «Silver Ticket» attack? What can you do with a «Golden Ticket» or «Silver Ticket»?
9. What has to be done if an attacker gained a «Golden Ticket»? 
10. Describe Kerberos delegation. What does it mean. Where is it used?
11. What is the difference between «unconstrained», «constrained» and «resource-based constrained» Delegation.
12. Can the user prevent delegation?  
13. Can you restrict delegation. Where does it makes sense to restrict delegation?  
14. What are the security risks? Describe how «unconstrained» delegation could be misused.  
15. How can you trick users to connect to your service configured for delegation? 
16. How could a printer on a DC could be attacked?  
17. What mitigation measurements do you know to secure Kerberos? 
18. How does an attack against «constrained» delegation looks like?  
19. What is meant with «protocol transition»? How does it work?  
20. What can you do with the permission «Trusted to Auth for Delegation» S4U2Self & S4U2Proxy?

### PKCS\#11

1. Describe a typical PKCS\#11 stack for accessing a security token.  
2. Where are APDU (Application Protocol Data Unit) commands used?  
3. Which protocol is common between SIM card, smart cards, credit cards, YubiKey etc.?
4. What is the intention of the PKCS\#11 API?  
5. How can you extract keys from a smart card or HSM?  
6. What does attestation stands for?  
7. What does the acronym U2F (Universal Second Factor) stands for? What is it based on?

### Wi-Fi
1. Under which conditions can you read all Wi-Fi network traffic?
2. Explain the difference between a network card in «promiscuous mode» and «monitor mode».
3. Describe the WEP (Wired Equivalent Privacy) encryption. What are the weak points?
4. What kind of authentication does WEP support (Shared Key Authentication, Open System Authentication)?
5. What is needed to crack a WEP key?
6. Describe a WPA2 authentication with PSK (pre-shared key)?
7. What is the purpose of PBKDF2 (Password-Based Key Derivation Function 2)?
8. Assume you want to analyze an WPA2 communication with Wireshark. What is needed to decrypt the packets of the CAP file (packet capture file)?
9. What Wi-Fi attacks do you know? Describe how they work. 
10. What is «SSID Cloaking»? Does it protect a Wi-Fi access point?

### VPN

1. At which OSI layer can VPN solutions be established? Provide examples.
2. What advantages and disadvantages, or challenges, are associated with a low-level implementation?
3. Explain the authentication process involved in IKEv2 (Internet Key Exchange Protocol Version 2).
4. What is the purpose of the Authentication Header (AH) and the Encapsulating Security Payload (ESP)? Elucidate the distinctions between these two components.
5. Explain the two IPsec modes: «tunnel mode» and «transport mode».
6. What MTU (Maximum Transmission Unit) considerations should be taken into account when implementing IPsec?
7. Which credentials are required to initiate a WireGuard VPN connection?
8. What is the fundamental concept behind the key exchange in «Noise Protocol Framework»? What is the RTT of the handshake?
9. Describe VPN network topologies.  
10. What minimum configurations are needed to set up a point-to-point VPN with WireGuard.

---
links: [[600 SPA MOC|SPA MOC]] - [[themes/000 Index|Index]]