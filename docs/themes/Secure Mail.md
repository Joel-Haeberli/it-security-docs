tags: #secure-mail

# Secure Mail

links: [[613 SPA TOC - Secure Email|SPA TOC - Secure Email]] - [[themes/000 Index|Index]]

---

## Message Routing

- mails are sent via **Simple Mail Transfer Protocol (SMTP)**
- the **mail exchanger record (MX record)** specifies the mail server responsible for a domain name
- the sending MTA queries DNS for the MX records of the recipient's domain name. The **lowest-numbered records are the most preferred**
- **MTA**: Mail Transfer Agent, SMTP server which forwards a mail
- **MUA**: Mail User Agent, pick up mails via POP3 or IMAP
- **MSA**: Mail Submission Agent
- **MDA**: Mail Delivery Agent

## SMTP over TLS

1. MUA submits email to MSA over port 587 (implicit TLS)
2. MSA forwards the email to the boundary MTA
3. MTA transmits the email to the boundary MTA of destination domain via implicit TLS
4. Receiving MTA forwards the email normally over multiple hops to the MDA. An MDA saves messages in the relevant mailbox format.
5. Only authenticated MUA can access the emails over implicit TLS (IMAP port 993, POP3 port 995)

![[smtp-over-tls.png]]

---
links: [[613 SPA TOC - Secure Email|SPA TOC - Secure Email]] - [[themes/000 Index|Index]]