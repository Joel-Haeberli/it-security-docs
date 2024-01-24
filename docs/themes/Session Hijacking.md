tags: #web-security #broken-authentication

# Session Hijacking

links: [[503 WS TOC - Broken Authentication|WS TOC - Broken Authentication]] - [[themes/000 Index|Index]]

---

## Idea

An attacker can somehow **guess or deduce the session ID** and use it to execute actions with the victims privileges.

## How the attack works

Since HTTP is session-less and identity and access rights might be bound to a session, the session ID is the key to link browser and server together. When an attacker can guess the session ID somehow, he can just send the ID and the server will not recognize that it is not the victim but the attacker sending the request. The problem lies in guessing or deducing the session ID. This might be easier depending on the mechanism used to create session ID (incremental approach for example make it way easier to deduce session ID's). 

To make session hijacking harder, use real random session ID and expire session within a reasonable time.

---
links: [[503 WS TOC - Broken Authentication|WS TOC - Broken Authentication]] - [[themes/000 Index|Index]]