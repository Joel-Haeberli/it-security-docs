tags: #secure-mail

# Email Authentication

links: [[613 SPA TOC - Secure Email|SPA TOC - Secure Email]] - [[themes/000 Index|Index]]

---

## Overview

- Authentication and Verification is mostly hidden for the end-users
- can be found in the *Mail Header*

## SPF

- **Sender Policy Framework** specify **which servers are allowed to send Emails** for the domain
- the IP addresses of authorized hosts are published in DNS records
- indirect mailflows (forwarders, mailing lists) cause SPF to either fail or lookup against a rewritten `MailFrom`
- Mail receivers declined to filter mail based solely on SPF

### Matchers

- `ALL`: matches always, used mainly for negation `-all` at the end of the policy
- `A`: check against hostname
- `IP4`: check against IPv4 address range (CIDR block is common)
- `IP6`: check against IPv6 address range
- `MX`: check against DNS MX record
- `PTR`: deprecated
- `EXISTS`: if the given domain resolves to any address, match (rarely used)
- `INCLUDE`: references the policy of another domain

### Qualifiers

- `+`: Pass (implicit always set `a:mail.example.com`)
- `-`: Fail
- `~`: Softfail
- `?`: Neutral
- Most records include: `+all`, `-all`, `~all` or `?all`

### Examples

```bash
dig TXT bfh.ch
```

![[spf-bfh.png]]

```bash
dig TXT _spf.bfh.ch
```

![[spf-bfh-2.png]]

### Limitations

- SPF typically fails after the first relay or "hop" (forwarding, mailing lists, etc.)
- Mailing lists and other indirect flows can rewrite the RFC5321.MailFrom to generate an SPF pass $\rightarrow$ spammers do this too
- Many receivers do not act on SPF's policy assertions (due to misconfiguration historically & present, what to do with a "softfail"?, ...)

![[spf-limits-1.png]]

![[spf-limits-2.png]]

## DKIM

- **Domain Keys Identified Message** uses a **digital signature** based on public key cryptography
- The sending organization uses its private company key to **sign outbound messages at the gateway** to the internet
- Receiver can **retrieve the corresponding public key via DNS** to verify the signature
- The signing domain does not have to have any relationship to the domains in the `From` (Mail Header) or `Mail From` (SMTP Envelope)

### Limitations

- **more complicated** to deploy than SPF
- does not verify if the signed parts of the message are altered (which unfortunately happens often):
	- mailing lists modifying Subject header
	- Corporate gateways adding a disclaimer/footer
	- Filtering services exchanging links/ removing images or MIME parts
- Crypto concerns need to be tracked and addressed (key length, hashing algorithms)

### Anatomy of a DKIM Signature

![[dkim-anatomy.png]]

### Getting the Signing Key

```bash
# dig TXT selector._domainkey.SDID
dig TXT selector1-bernerfachhochschule-onmicrosoft-com._domainkey.bernerfachhochschule.onmicrosoft.com
```

![[dkim-bfh.png]]

![[dkim-process.png]]

## ARC

- **Authenticated Received Chain** was published in 2019 as "Experimental"
- ARC defines three new mail headers
	- **ARC-Authentication-Results (AAR)**: combination of an instance number (`i`) and the results of the SPF, DKIM and DMARC validation
	- **ARC-Seal (AS)**: combination of an instance number (`i`), a DKIM-like signature of the previous ARC-Seal headers, and the validity of the prior ARC entries
	- **ARC-Message-Signature (AMS)**: combination of an instance number (`i`) and a DKIM-like signature of the entire message except for the ARC-Seal headers
- **to sign a modification**, an intermediate server performs the following steps:
	- Copies the "Authentication-Results" field into a new AAR field (starting with `i=1`) and prepends it to the message
	- Calculates the AMS for the message (with the AAR) and prepends it to the message
	- Calculates the AS for the previous ARC-Seal headers and prepends it to the message
- **to validate** an ARC, the recipient performs the following steps
	- Validates the chain of ARC-Seal headers (no missing entries, all ARC-Seal messages state that the prior ARC entries are valid, etc.)
	- Validates the newest ARC-Message-Signature (based on the instance number)

### ARC Anatomy

![[arc-anatomy.png]]

### Why another protocol?

- no consistency in DKIM and SPF deployment
- Receivers could not rely on pass/fail results
- No way to tell if things improve or worsen (no visibility)

- ARC was created to **address challenges posed by the SPF and DKIM in certain email forwarding scenarios**
- ARC wont replace SPF, DKIM and DMARC, ARC complements them and is designed to work alongside these standards.

## DMARC

- **Domain-based Message Authentication, Reporting and Conformance**
- developed 


---
links: [[613 SPA TOC - Secure Email|SPA TOC - Secure Email]] - [[themes/000 Index|Index]]