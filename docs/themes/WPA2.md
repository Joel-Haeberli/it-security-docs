tags: #wifi #wpa

# WPA2

links: [[617 SPA TOC - Wireless Security|SPA TOC - Wireless Security]] - [[themes/000 Index|Index]]

---

## Overview

- WPA2 is the most common authentication method used on wireless networks today
- it includes mandatory support for **CCMP** (**Counter Mode CBC-MAC Protocol**) $\rightarrow$ see [[Authenticated Encryption#CCM (Counter with CBC-MAC)|CCM]]
- there are tow flavors:
	- **WPA Personal**: Pre Shared Key (PSK) for authentication
	- **WPA Enterprise**: Extensible Authentication Protocol (EAP) via [[Network Access Control#IEEE 802.1X|IEEE 802.1X]] (requires a RADIUS server for authentication)

## 4-Way Handshake

1. The AP sending a random number (ANonce) to the client
2. The client responding with its random number (SNonce)
3. The AP calculating the PTK (Pairwise Transient Key) from these numbers and sending an encrypted message to the client
4. The client decrypting this message with the PTK, confirming successful authentication

![[wpa2-handshake.png]]

## Pairwise Master Key (PMK) from PSK

- the PTK (Pairwise Transient Key) depends on the PMK (Pairwise Master Key) which is 256 Bit value derived from the PSK (WPA passphrase) via [[Password Based Key Derivation Function (PBKDF)#PBKDF1 & PBKDF2|PBKDF2]]

![[pmk.png]]

## Pairwise Transit Key (PTK) Calculation

- the PTK is used to encrypt data between client and AP
- it has 64 bits and will change every 65535 packets
- it is derived from a [[CPA-Security#Pseudorandom Functions and Permutations|PRF]]

![[ptk.png]]

**The PTK splits as follows:**

![[ptk-components.png]]

- Key Confirmation Key (**KCK**): used to compute MIC for integrity
- Key Encryption Key (**KEK**): used to encrypt additional data from the AP during handshake
- Temporal Key (**TK**): used to encrypt/decrypt messages after the handshake
- MIC Authenticator Tx Key (**MIC Tx**): used to compute MIC on packets transmitted by AP
- MIC Authenticator Rx Key (**MIC Rx**): used to compute MIC on packets transmitted by the client

## Message Integrity Check (MIC)

- the MIC is used to prevent tampering with or forgery of data packets, ensuring the integrity and authenticity of the transmitted data

![[mic.png]]

## WPA/WPA2-PSK Cracking

- Available information from the handshake:
	- SSID
	- ANonce and SNonce (transmitted in clear-text)
	- MAC addresses (Client and AP)
	- Message's MIC computed with a valid PTK (used to verify passphrase guess)
- Cracking process:
	1. Guess passphrase (PSK)
	2. Compute PMK for this passphrase using `PMK = PBKDF2(HMAC-SHA1,PSK,SSID,4096,256)`
	3. Derive PTK from the assumed PMK using `PTK = PRF(PMK,STRING|ANONCE|SNONCE|MAC(AA)|MAC(STA))`
	4. Use generated KCK to compute a MIC for packet 2, 3 or 4 of the captured handshake
	5. If computed MIC = MIC of the captured packet $\rightarrow$ passphrase found!
	6. Otherwise, go back to step 1

## Wi-Fi Attacks

- **ARP Spoofing**: also known as ARP poisoning, can be used to perform MITM attacks
- **Rouge DHCP**: allows attackers to set their device as the default router
- **ICMP Redirects**: MITM attack, instruct the victim device to route all traffic through the attacker
- **DNS Spoofing**: one of the easiest way to redirect victims to the system of their choice
- **Fake Webauth**: most users are used seeing a webauth page when connecting to a Wi-Fi
- **SSL MITM**: every SSL Reverse Proxy is actually an SSL MITM
- **SSL Stripping**: instead of presenting a fake certificate, redirect to an HTTP page and rely on the user not noticing
- **KARMA attack**: vulnerable client devices broadcast a "preferred network list" (PNL), which contains the SSIDs of APs to which they are willing to reconnect without user intervention. The KARMA attack consists of an access point receiving this list and then assigning itself an SSID from the PNL, thus becoming the evil twin of an AP already trusted by the client.

## Securing Wireless Networks

- **Network Segmentation**: Least privileges and segmentation through firewalls, routers, ...
- **Encryption**: use WPA2 with CCMP, add additional layers such as IPsec, ...
- **Authentication**: choose between Pre-Shared Key (PSK), Protected Extensible Authentication Protocol (PEAP) or the Extensible Authentication Protocol-TLS (EAP-TLS) with user certificates. The latter is considered the most secure variant.
- **Faraday Cage**: limit physical propagation of signals
- **MAC Filtering**: Questionable
- **SSID Cloaking**: not broadcasting the SSID $\rightarrow$ SSID cloaking can obscure a network from the general public but is detectable by more sophisticated users and not more secure against attacks
- **IDS or IPS**: see [[IDS & IPS]]
- **Honeypot**: simulate a vulnerable target

---
links: [[617 SPA TOC - Wireless Security|SPA TOC - Wireless Security]] - [[themes/000 Index|Index]]