tags: #SPA #VPN 
 
# VPN Overview

links: [[616 SPA TOC - VPN|SPA TOC - VPN]] - [[themes/000 Index|Index]]

---

A Virtual Private Network (VPN) is a technology that establishes a secure, encrypted connection over a public network. It allows users to securely access a private network and share data remotely through public networks.

![[VPN-tunnel-overview.png]]

## Communication Layer (ISO/OSI)

 ![[vpn-communication-layers.png]]

## Quantum Key Distribution

Not that important but it was mentioned in the slides so:

- Unconditionally secure private key encryption can be done with a one time pad (OTP). Weakness of this is, that the key has to be securely transmitted between the communication partners
- Quantum cryptography solves this problem by enabling a unconditionally secure transmission of random bytes. Most famus example is the BB84 protocol developed in 1984.

## Bridging

Used to create a virtual network between VMs on the same physical host:

![[vpn-bridging.png]]

---
links: [[616 SPA TOC - VPN|SPA TOC - VPN]] - [[themes/000 Index|Index]]