tags: #web-security #crypto-failures

# Introduction to Crypto Failures

links: [[504 WS TOC - Crypto Failures]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---

## About Crypto Failures

Cryptographic failures are listed as the second vulnerability within the [OWASP Top 10 (2021)](https://owasp.org/Top10/). It describes the vulnerability, where sensitive data can be accessed due to lack of encryption or broken cryptographic implementations. These vulnerabilities can occur in local storage, in a database or when transiting data through a network.

In most of the cases, attackers do not break a cryptographic standard but instead steal a key, break something which they can use to decrypt the data or place them selves as MITM.

The difficulty for exploits depends on the exact vulnerability. Not encrypting sensitive data is one of the most common exploits in this category (but is it already an exploit if you can read some human readable alphabet?). If data is encrypted, weak key generation processes, poor key management or the usage of weak algorithms are the problems.

Once a vulnerability exists, its exploitation can cause severe damage because sensitive data like health data, credentials, personal secrets or financial concerns can be uncovered.

## History and examples

[**Wikileaks**](https://wikileaks.org/) showed that NSA was spying on google mail and tons of emails were readable by then. Therefore the NSA listened on communication between the datacenters. Google, after Wikileaks published it, strengthtened their systems by using TLS (HTTPS) for all their clients of gmail. Data was encrypted in transit and when stored on disk.

**Heartbleed** was a security flaw within the OpenSSL library discovered in 2014 which made it possible for attackers to read out memory of machines which might include private keys and other sensitive data:

- [OWASP on Heartbleed](https://owasp.org/www-community/vulnerabilities/Heartbleed_Bug)
- [Bruce Schneier on Heartbleed](https://www.schneier.com/blog/archives/2014/04/heartbleed.html)
- [EFF on Heartbleed](https://www.eff.org/deeplinks/2014/04/wild-heart-were-intelligence-agencies-using-heartbleed-november-2013)

To prevent such attacks and other, you must [[Defining your Assets|define you assets]] in order to know needs to be done to secure them.

---
links: [[504 WS TOC - Crypto Failures]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]