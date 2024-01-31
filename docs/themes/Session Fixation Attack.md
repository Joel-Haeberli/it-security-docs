tags: #web-security #broken-authentication

# Session Fixation Attack

links: [[503 WS TOC - Broken Authentication|WS TOC - Broken Authentication]] - [[themes/000 Index|Index]]

---

## Idea

The attacker is able to **create a session and keeping the session alive**. If a web page then handles session identifiers via URL, the attacker can for example use his session to for example let the victim execute a action in person of the session which was injected by the attacker.

## How the attack works

Attacker first sets up and keeps alive a session. He then poisons a URL which takes the session in the URL and uses this URL for e.g. phishing and sending it to victims who use the web page. If the victim opens the web page, it will be authenticated using the session given by the attacker.

Don't use session identifiers in URL. Reset the session on each login.

---
links: [[503 WS TOC - Broken Authentication|WS TOC - Broken Authentication]] - [[themes/000 Index|Index]]