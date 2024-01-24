tags: #auth 

# Basic Authentication

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## Basic Authentication

- A way for a web browser to send username and password to a server
- Transmits passwords in cleartext, needs TLS
- Rarely used anymore, mostly replaced by form-based authentication
- APIs often provide server generated tokens which replace the base64 encoded "username:pw"
	- higher entropy
	- possible to create separate access token for separate applications
	- revokable
	- scope-able

1. Server sends status 401 Unauthorized with a challenge: `WWW-Authenticate: Basic realm="Wallys World"`
2. The client concats username and pw: "username:pw"
3. Base64 encode the string
4. Put the resulting base64 in the authorization header: `Authorization:Basic am9objpwYXNzd29yZA==`

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]