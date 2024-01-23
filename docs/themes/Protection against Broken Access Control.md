tags: #web-security #broken-access-control

# Protection against Broken Access Control

links: [[502 WS TOC - Broken Access Control]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---

## Authorization

First authorize each request to each single page. For this a user must be logged in and have the correct privileges to access the requested page. Additionally, for each object referenced, it must be checked that the user has the correct privileges to access the resource. Only because a user is signed in successfully, it doesn't mean that the user should have access to all resources that may be requested by the user somehow.

## Avoiding Direct Object Referencing

If using identifiers on API don't match them directly to objects inside the system. This means that it should not be possible to gain access to data directly through an exposed parameter. So don't use database primary keys or filenames directly as parameters. Instead us a mapping or hashing functionality. Also remember to check authorization on each request to an object. This should check if the user has the correct privileges to read the respective object.

## Disallow Malicious File Execution

In order to prevent the application from running files on behalf of the attacker, the application shall not use user-supplied input for 

- Accessing server base resources
- Images
- XML or XSLT
- Scripts

Additionally the application should not have firewall rules preventing outbound requests. **Validate your input**. This means for filenames to have a certain format or to be placed in a certain location. Prevent path traversal by checking that the file does lie within a defined boundary. Implement some sandbox functionality to run the application, which forces it to stay within the boundaries of the sandbox.

## Conclusion

(directly copied from slides)

- OWASP Top 10 - A1:2021
	- Broken Access Control
	- most important web security risk in 2021
- Dangerous
	- Easy to exploit
	- Flow is quite common
	- Business impact is proportional to the functions that can be discovered.
- Web Parameters are easily spoofed
	- GET can be manipulated in the URL string
	- POST needs more sophisticated tool but is very easy too
- Giving access to internal resource
	- Allows modification, and illegal access
	- But gives also useful information about your site (even if access is prohibited)
- Should include authorization check in every page and resource
	- Protects against privilege escalation (horizontal and vertical).
- Hard to protect the access to internal resources
	- Even harder in Client Side applications (JSON / AJAX).

---
links: [[502 WS TOC - Broken Access Control]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]