tags: #auth 

# Basic Authentication

links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]

---

## Basic Authentication

- It's a simple authentication scheme built into the HTTP protocol to transfer username and password with each HTTP request
- Transmits the string 'username:password' in cleartext (Base 64 encoded) $\rightarrow$ needs to use TLS
- Rarely used anymore, mostly replaced by form-based authentication
- Most APIs that use Basic Auth provide server generated tokens / passwords which replace the base64 encoded 'username:pw'
	- higher entropy
	- possible to create separate access token for separate applications
	- revokable
	- scope-able

### How it works

1. Server sends status 401 Unauthorized with a challenge: `WWW-Authenticate: Basic realm="Wallys World"`
2. The client concats username and pw: "username:pw"
3. Base64 encode the string
4. Put the resulting base64 in the authorization header: `Authorization:Basic am9objpwYXNzd29yZA==`

---
links: [[612 SPA TOC - Identification Authentication|SPA TOC - Identification Authentication]] - [[themes/000 Index|Index]]