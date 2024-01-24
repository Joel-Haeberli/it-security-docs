tags: #osi

# Application Layer

links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]

---

## Application Layer

- Provides protocols for end-user applications
- Provides standardized services to applications

### Vulnerabilities

- Open design issues allow free use of application resources by unintended parties
	- Example: API endpoint that allows retrieving user information without authentication / authorization
	- Anyone who knows the API URL can access personal data of all users
- Backdoors and application design flaws bypass standard security controls
	- Example: Platform has hidden URL that was used during development to test payment systems and allows orders to be marked as paid without any transaction
- Inadequate security controls force "all-or-nothing" approach, resulting in either excessive or insufficient access
	- Example: Platform with regular users and admin users
	- No granular permissions to limit access based on necessity or role
- Overly complex application security controls tend to be bypassed or poorly understood and implemented
	- Example: Complicated role-based access control system that is poorly documented
	- Users are given higher privileges than necessary just to ensure they can access the tools they need for their job
- Program logic flaws may be accidentally or purposely used to crash programs or cause undesired behaviour
	- Example: Chat application only handles message payloads smaller than a certain size
	- If a user sends a larger message it might cause a buffer overflow that crashes the server -> DoS

### Attacks

- Malicious spam emails containing malware
- Malware
	- Viruses
		- Software that piggybacks on other programs or files
		- Virus runs when program runs or file is opened
		- Can reproduce itself by attaching to other programs or files
	- Worms
		- Software that uses computer networks and security holes to replicate itself onto other clients
	- Trojan horses
		- Program which claims to do one thing but instead does damage such as erase HD
		- Trojan horses don't replicate
	- Ransomware
		- Encrypt client data and demand ransom for decryption keys

### Controls

- Application-level access
	- Define and enforce access to application resources
	- Controls must be detailed, flexible and straightforward to prevent complexity
- Standards, testing, and review of application code and functionality
	- Define a baseline (set of metrics) or standards / best practices
	- Regularly compare the current implementation of the application to this baseline
- Intrusion detection systems (IDS)
	- Monitor network or system activities for malicious activities or policy violations
- Traffic regulation by application
	- Define firewall rules to regulate traffic by application / port

---
links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]