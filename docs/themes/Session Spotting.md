tags: #web-security #broken-authentication

# Session Spotting

links: [[503 WS TOC - Broken Authentication|WS TOC - Broken Authentication]] - [[themes/000 Index|Index]]

---

## Idea

When the attacker can **observe the login** of a user and the user receives a session-ID of the server during the process, the attacker steals this session-ID and can now use the session-ID to authenticate against the web application.

## How the attack works

The attacker somehow manages to eavesdrop the traffic of the client to the server. He specifically looks for requests to the login functionality. If a login occurs, he looks for the respective response. This response may contain a session-ID as cookie. Now the attacker can use this cookie to gain access to the API. He will therefore impersonate the user which he stole the session-ID from.

To prevent the attack only secure cookies shall be used.

---
links: [[503 WS TOC - Broken Authentication|WS TOC - Broken Authentication]] - [[themes/000 Index|Index]]