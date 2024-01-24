tags: #web-security #broken-access-control

# Tampering with HTTP parameters

links: [[502 WS TOC - Broken Access Control|WS TOC - Broken Access Control]] - [[themes/000 Index|Index]]

---

## Why HTTP

HTTP is probably the most used application layer protocol used in internet traffic. It loads pages and serves API's with specific data used to enrich web pages with dynamic content. Therefore the protocol is also exposed to vulnerabilities like broken access control. HTTP comes with a set of parameters which can be tampered in order to force a server to act in an unexpected way.

Since HTTP is an open protocol, it is not necessary to use a browser or webpage to tamper requests. One can also create requests manually and use programs to execute requests (e.g. curl).

## HTTP GET

When using HTTP GET to attack a website, we can tamper the request by directly changing the request parameters in the url. The url is never encrypted and GET requests do not have a request body as defined by the protocol. If a request is not verified by the receiver or transmitted through HTTP*S*, one could also tamper requests as MITM. The widespread adoption of HTTP*S* mitigates such a MITM attack.

## HTTP POST

Parameters of POST requests are held in the body and are therefore encrypted. Only the client creating the request can tamper the parameters in the body.

## HTTP Headers

Other HTTP headers which can be tampered in order to leverage broken access control are:

- Cookies
- Languages
- User-Agent
- and so on

An detailed insight to the capabilities of HTTP see [Mozilla on HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)

---
links: [[502 WS TOC - Broken Access Control|WS TOC - Broken Access Control]] - [[themes/000 Index|Index]]