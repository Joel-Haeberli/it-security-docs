tags: #osi

# Physical Layer

links: [[604 SPA TOC - Layered Security]] - [[600 SPA MOC|Security Protocols and Applications MOC]] - [[000 Index|Index]]

---

## Physical Layer

The physical layer sends and receives bits between adjacent stations on the link and handles the following specifications:

- physical
	- connectors
	- type of medium
		- wired (gerichtet, copper cable, fibreglass)
		- wireless (ungerichtet, radio waves)
- electrical
	- voltage
	- current level
- procedural
	- signal encoding
	- modulation
	- bit rate control
	- frame delimiting
	- error detection
	- frame ordering
	- collision detection

### Vulnerabilities

- loss of power
- loss of environmental control -> air conditioning failure
- physical theft of hw or data
- physical damage or destruction of hw or data
- unauthorized changes to the functional environment -> employee installing unapproved modem
- disconnection of physical data links
- undetectable interception of data -> scanning electromagnetic radiation, [Van-Eck-Phreaking](https://de.wikipedia.org/wiki/Van-Eck-Phreaking)
- key logging
![[physical-layer-vulnerability.png]]

### Controls

- geographical separated datacenters and redundant connections
- use of link and data storage cryptography -> TLS for transit, AES for data at rest
- uninterruptible power supplies (UPS) and emergency generators
- monitored (thermal) environment, use of cooling systems
- electromagnetic shielding
- locked and monitored perimeters and enclosures using:
	- electronic lock mechanisms for logging & detailed authorization
	- PIN & password secured locks
	- biometric authentication systems
	- video & audio surveillance

---
links: [[600 SPA MOC|Security Protocols and Applications MOC]] - [[000 Index|Index]]