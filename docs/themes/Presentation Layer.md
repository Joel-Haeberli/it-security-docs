tags: #osi

# Presentation Layer

links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]

---

## Presentation Layer

- Translates data format of sender to the data format of the receiver
- Provides code conversion, data compression and encryption services (according to ISO / OSI)

### Vulnerabilities

- poor handling of unexpected input can lead to application crashes or surrender of control to execute arbitrary instructions
	- Example: SQL injection
- unintentional or ill-advised use of externally supplied input in control contexts may allow remote manipulation or information leakage
	- Example: Attacker providing /etc/passwd in the URL
- cryptographic flaws may be exploited to circumvent privacy protections
	- Example: Passwords hashed with MD5

### Attacks

- Unicode vulnerabilities
	- Normally web servers only serve files from certain directories
	- Older versions of IIS web server interpreted directory traversal sequences like "../" as illegal
	- This rule didn't not trigger when the "/" was provided as unicode encoded version "%c0%af"
	- This allowed attackers to traverse directories
	- [Apache UTF-8 directory traversal](- https://www.cvedetails.com/cve-details.php?cve_id=CVE-2008-2938)
	- [Windows Vista filename spoofing](0. https://heise.de/-178566)
	- [Other unicode vulnerabilities](- https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=Unicode)
- [DNS IDN spoofing](https://heise.de/-132814)
	- Using special characters in domain names
	- http://www.pаypal.com/ -> http://www.xn--pypal-4ve.com
- [.zip TLD](https://www.digitec.ch/de/page/neue-zip-domain-wird-bereits-von-cyberkriminellen-missbraucht-27828)

### Controls

- Careful specification and checking of received input incoming into applications or library functions
	- Example: Using regex to validate if an email address is actually an email address
	- Mitigation against injection attacks
- Separation of user input and program control functions
	- Input should be sanitized, and sanity checked before being passed into functions that use the input to control operation
	- Use prepared statements and parameterized queries
	- Treat user inputs as data, not as part of a SQL command itself
	- Mitigates against injection attacks
- Careful and continuous review of cryptography solutions to ensure current security versus known and emerging threats
	- Updating TLS to the latest version

---
links: [[604 SPA TOC - Layered Security|SPA TOC - Layered Security]] - [[000 Index|Index]]