tags: #social #hacking 

# Intrusion Techniques

links: [[603 SPA TOC - Hacking Basics|SPA TOC - Hacking Basics]] - [[themes/000 Index|Index]]

---

## Physical Intrusion 

This is the worst attack from a victims point of view, as the attacker has access to the hardware itself.

## Remote Intrusion

Happens over the network. Starting with `nmap` or other tools. Using software bugs, configuration bugs, design flaws, weak passwords or [[Social Engineering]].

### Software Bugs (CWE)

See also: [[500 WS MOC|Web Security]]

1. Out-of-bounds Write
2. Improper Neutralisation of Input during Web Page Generation ([[Cross Site Scripting|Cross-site Scripting]])
3. Improper Neutralisation of Special Elements used in an SQL Command ([[SQL-Injection|SQL Injection]])
4. Use After Free
5. Improper Neutralisation of Special Elements used in an OS Command (OS Command Injection)
6. Improper Input Validation
7. Out-of-bounds Read
8. Path Traversal
9. [[Cross Site Request Forgery (CSRF)]]
10. Unrestricted Upload of File with Dangerous Type
11. Missing Authorisation
12. NULL Pointer Dereference
13. Improper Authentication
14. Integer Overflow or Wraparound
15. Deserialisation of Untrusted Data
16. Command Injection
17. Improper Restriction of Operations within the Bounds of a Memory Buffer
18. Use of Hard-coded Credentials
19. Server-Side Request Forgery (SSRF)
20. Missing Authentication for Critical Function
21. Race Condition
22. Improper Privilege Management
23. Improper Control of Generation of Code (Code Injection)
24. Incorrect Authorisation
25. Incorrect Default Permissions

### Configuration Bugs

* Leaving bad default configurations in place
* Running unnecessary services (bigger attack surface)
* Trust relationships between systems $\rightarrow$ Weakest link

### Design flaws

* Protocol flaws
* Poor system administrator practices (let's try first without security and then forgot to change it)

## Weak passwords

Passwords are still the most widely used method in 2024.
If they are weak they be cracked through guessing, dictionary attacks, brute fore attacks and rainbow tables. Or acquire them by sniffing, replay, observation, social engineering or key logging.

## Intrusion Scenarios

1. **reconnaissance** (appearing as a normal user, hard to detect)
2. **scanning** (ICMP scan, Port scan, identify OS and software)
3. **running exploits** (exploit a vulnerability that was found, you cross the line here)
4. **establish a foothold** (hide evidence, rootkit installation, replace services, hack other systems from here)
5. **playing for profit**

## Shortcut Intrusion Scenarios

* Use automated tools for scanning and break in
* Create fake websites to harvest credentials
* Infect vulnerable websites with malware
* Scam mails and messages for social engineering
* Or directly by phone, as a fake support agent

---
links: [[603 SPA TOC - Hacking Basics|SPA TOC - Hacking Basics]] - [[themes/000 Index|Index]]