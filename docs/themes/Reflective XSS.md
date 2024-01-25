tags: #web-security #xss

# Reflective XSS

links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[themes/000 Index|Index]]

---

- The website reflects user supplied data directly back to the user
- Example
	- User enters text in a search bar
	- The server returns dynamic feedback: "You searched: ..."
	- The browser renders the text
	- If it contains a script, the script is executed

``` javascript
"You searched: "<script>alert("Hello World")</script>"
```

### Exploit

- Add the script as parameter in the URL and make the victim click the link (Phishing)
- Link looks correct and the certificate is also correct

Unencoded URL example

```
http://vulnerable-website.com/search?query=<script>alert('XSS')</script>
```

---
links: [[505 WS TOC - Cross Site Scripting (XSS)|WS TOC - Cross Site Scripting (XSS)]] - [[themes/000 Index|Index]]
