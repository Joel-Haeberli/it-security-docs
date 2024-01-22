tags: #network-security 

# Network Access Control

links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]

---

## Network Access

**Requirements**

- knowing who is using the network
- limiting the access to networks to **authorized users**
- limiting access to **clean systems**

### MAC based Port Security

- **limiting access on switch ports to specified MAC addresses only**
- manual or automatic through "learning"
- **Disadvantages**: not flexible in networks with roaming/ mobile devices, MAC addresses can be spoofed

### IEEE 802.1X

- **Port-Based Network Access Control**
- restricts the use of networks/ports to **authenticated and authorized devices**
- specifies a common architecture and protocols that support mutual authentication between the clients of ports (**supplicant**) and the switch (**authenticator**) using a backend (**authentication server**, e.g. a RADIUS server) & secures the communication between them
- based on **extensible authentication protocol (EAP)** and works with any IEEE802 network technology (ethernet, wireless)

## Network Access Control (NAC)

- control access to a network with policies
- including **pre-admission endpoint security policy checks**
- and **post-admission controls**: where users and devices can go on a network

**Goals**

- **identity and access management:** identify user, his node, ip address, switch-port, network segment, MAC address
- **policy enforcement**: grant or deny access to a network segment
- **mitigation of zero-day attacks**: deny access for unmaintained, contaminated and malicious nodes

**Concepts**

- **client verification**: before (pre-admission) or after (post-admission) granting access
- **agent or argent less**: verification of the client with or without installed client
- **remediation**: using quarantine networks/vlans

---
links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]