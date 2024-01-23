tags: #web-security #broken-access-control

# Introduction and Principles of Broken Access Control

links: [[502 WS TOC - Broken Access Control]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---
## Introduction 

Access control is intended to force users to act inside intended permissions. If an access control measure fails and an attacker can gain unauthorized access, it can come to...

- Unauthorized disclosure of information
- Modification or destruction of data
- Performing an action on a system which the user shall not be legitimated to
- Accessing pages and information without authorization
- Accessing data directly, but through a transaction ([[Introduction and Principles of Broken Access Control#Insecure Direct Object Reference|Direct Object Reference]])
- Accessing files outside defined boundaries (Path Traversal)

Broken Access Control can lead to two kinds of privilege escalation:

- Vertical Escalation (escalate to privileges of higher power):
	- Anonymous users access private functionality
	- Regular users access administrators functionality
- Horizontal Escalation (privileges of other users are gained):
	- A user can access data of other users

Broken Access Control is the **top vulnerability** according to the [OWASP Top 10 (2021)](https://owasp.org/www-project-top-ten/)
### Insecure Direct Object Reference

Insecure Direct Object Reference appears when an exposed API directly links to artefacts which shall be protected by access control. So if an attacker can bypass the access control, he is capable of *directly referencing* the (un)protected artefact. This is also important when using identifiers as parameters. One should on each request check if the user has the right to read the object referenced by the given identifier. Otherwise horizontal escalation might be possible, if the user is able to change the identifier in the request.

In the following request for example, each time the `id` must be matched by some authorization service and lookup if the logged in user is allowed to access the object referenced by `id`: `https://mydocs/private?id=123`
## Principles of the vulnerability

In general the Broken Access Control vulnerability is caused...

- by developers...
	- not testing a users request for its legitimacy to access the requested resource
	- exposing insecure direct object references such as files, directories, database records or keys through an API
- by attackers...
	- using a lack in access control check by manipulating request parameters
- by applications...
	- exposing an internal object reference to users (for example if an application is allowed to access files only within the applications process working directory, this must be checked when a user can choose a file-path for whatever reason the user needs the file for).

## Threat Agents

Participants who could leverage broken access control are: 

- Anyone with network access
	- by sending requests to your application
- Anonymous users may access restricted parts of the application
	- Vertical Escalation
- A regular user of the system uses privileged functions
	- Vertical Escalation
- A regular user can access data of other regular users
	- Horizontal Escalation


---
links: [[502 WS TOC - Broken Access Control]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]