tags: #wifi #wep

# WEP

links: [[617 SPA TOC - Wireless Security|SPA TOC - Wireless Security]] - [[themes/000 Index|Index]]

---

## Overview

- **Wired Equivalent Privacy (WEP)** uses the stream cipher **RC4** for confidentiality and the **CRC-32** checksum for integrity
- Standard 64-bit WEP uses a 40-bit key with an IV of 24bit. The extended 128-WEP uses a 104-bit key
- **All users use the same key**

![[wep-overview.png]]

## Authentication

- **Shared Key Authentication** (discouraged!):
	1. The client sends authentication request to the access point
	2. The access point replies with a challenge (pseudo-random number/nonce)
	3. The client encrypts the nonce using the WEP key and send it back
	4. The access point encrypts the same nonce and compares it to the response
- **Open System Authentication** (relies on the fact that packets are encrypted with the correct WEP key)
	1. The client sends an authentication request to the access point
	2. The access point sends back a message that the station is authenticated

## FMS attack

- Fluhrer, Mantin and Shamir (FMS) attack is an attack to the RC4 stream cipher, was improved in 2004 by the KoreK Attack
- It allows an attacker to **recover the key in an RC4 encrypted stream from a large number of messages**.
- basis lies in the **weak 24bit IVs** used with RC4
- the number of required packet is about 400'000

## PTW attack

- Pyshkin, Tews and Weinmann (PTW) attack
- presented the first correlation that holds for all packets $\rightarrow$ using all packets allows for fewer packets to decrypt key

---
links: [[617 SPA TOC - Wireless Security|SPA TOC - Wireless Security]] - [[themes/000 Index|Index]]