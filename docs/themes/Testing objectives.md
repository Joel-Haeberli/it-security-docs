tags: #web-security

# Testing objectives

links: [[507 WS TOC - Testing|WS TOC - Testing]] - [[themes/000 Index|Index]]

---

### Introduction

This topic is about testing a website for attack points and potential vulnerabilities. The intended situation is that the tester is employed by a company to make a security analysis of their website.

### Methodology (Randomly ordered)

- Get overview of the system
- List all the entry points
- Make a check list of controls
- Report
	- Describe the scope of testing
	- Write the list of tests done and their result
	- For each of the problems, state its "risk"
- Gather intelligence on the site
	- Who, which technology, server, language, lib
- Make a map of the site
	- Have a complete list of all features and entry points of an application
- Find entry points
	- Where can user enter input?
	- Can the application be manipulated?
	- Spoofing(???)
- Systematically check input validation / output encoding
	- $\rightarrow$ [[505 WS TOC - Cross Site Scripting (XSS)|Cross Site Scripting (XSS)]]
- Attack authentication / authorization mechanism
- Test business logic

### Testing techniques

- Manual inspections and reviews
	- human-driven reviews
	- This approach is time consuming but powerful / effective
- Threat modelling
	- Decomposing the application
	- Defining and classifying the assets
	- Exploring potential vulnerabilities / threats
- Code review
	- Check code for completeness, effectiveness and accuracy
	- Requires highly skilled devs
	- Issues can be missed in compiled libraries
- Penetration testing
	- *“If you fail a penetration test you know you have a very bad problem indeed. If you pass a penetration test you do not know that you don’t have a very bad problem”*

---
links: [[507 WS TOC - Testing|WS TOC - Testing]] - [[themes/000 Index|Index]]