tags: #web-security #broken-authentication

# Brute Force (Broken Authentication)

links: [[503 WS TOC - Broken Authentication]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---

## Idea

Just **brute force a login**. This can be done online if the site does not protect against it (max numbers of login attempts or similar mechanism). Brute force attacks get easier, because web pages do allow weak passwords.

## How the attack works

Often the attacker takes a list of often used passwords and a database dump of password hashes. Then he automatically tries all the passwords by hashing them with the correct password hashing method. If a match is found we have a password. Now if we can also link the password to the user (which should be possible if the database dump holds the linked user).

---
links: [[503 WS TOC - Broken Authentication]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]