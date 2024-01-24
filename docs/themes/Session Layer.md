tags: #osi

# Session Layer

links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]

---

## Session Layer

- Establishes and terminates communication sessions between host processes
- Provides synchronization and translation between name and address databases
	- Synchronization: Keeping client and server in sync
	- Translation: URL to IP (DNS)
- Relevant topics: TLS, TCP

### Vulnerabilities

- Weak authentication mechanisms
- Passing of session credentials such as user ID and password in the clear, allowing intercept and unauthorized use
- Session identification may be subject to spoofing and hijacking
	- If session IDs are predictable, an attacker might be able to guess another users session ID and hijack the session
- Leakage of information based on failed authentication attempts
	- Login form returns "Username is correct but the password is incorrect"
- Unlimited failed sessions allow brute-force attacks on access credentials
	- Can be mitigated with lockouts after a given amount of failed tries or CAPTCHAs

### Attacks

- TCP session hijacking
	- Possible if the attacker can predict the sequence number
	- Server will accept the packet if the sequence number matches
	- Requirement: IP Spoofing to get the same IP as victim
- (TLS / SSL) Man-in-the-middle
	- Attacker intercepts unencrypted connections, reads the data and then sends it to the intended recipient without them knowing
	- With TLS the attacker also needs a forged certificate to intercept and decrypt the communication
- Session ID / Cookie attack
	- Attacker steals or predicts the session identifier to impersonate a user
- Downgrade attack
	- Attacker forces the use of an older less secure version of the protocol
- SSH brute-force attack
	- Attacker repeatedly attempts to log in to an SSH server with different username / password combinations
- TCP connection hijacking / MITM
	- Host A and host B go through the TCP handshake to establish a connection
	- Attacker can exploit a "desynchronized state" in TCP communication where the sequence numbers between Host A and B do not match up
	- Attacker can trigger this state by sending packets to one or both Hosts
	- Once the sequence numbers are out of sync, host A and B are ignoring each others packets
	- Attacker can then inject forged packets with the correct sequence numbers
	- Requirement: IP Spoofing to get the same IP as victim

### Controls

- Encrypted password exchange and storage
	- Using HTTPS and hashing / salting passwords
	- Mitigates eavesdropping attacks
- Accounts have specific expirations for credentials and authorization
	- Mitigates against unauthorized access from stolen credentials
	- Reduces window of opportunity
- Protect session identification information via random/cryptographic means
	- Use secure RNG to generate session IDs
	- Mitigates against session hijacking
	- Attackers can't guess / predict session IDs
- Limit failed session attempts via timing mechanism, not lockout
	- Mitigates against brute force attacks
- Use correct certificates on servers and clients
	- Mitigates against MITM attacks

---
links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]