tags: #header-fields

# Important Header Fields

links: [[Firewalls]] - [[themes/000 Index|Index]]

---

## MAC header

![[Ethernet_frame.png]]

**EtherType**
- two octet (16bits)
- `0x0800`: IPv4
- `0x0806`: ARP
- `0x8100`: VLAN-tagged frame
- `0x86DD`: IPv6

**VLAN tagging (802.1Q)**
- insertion 802.1Q Header of the four octets (32bits) into the Ethernet frame
- **tag protocol identifier (TPID)** of `0x8100`

![[Ethernet_802.1Q_Insert.png]]
## IP header

**Fragment offset**
- specifies the offset of a particular fragment relative to the beginning of the original unfragmented IP datagram. The first fragment is always 0.

**IP Protocol numbers**
- found in field *Protocol* of the IPv4 header
- found in field *Next Header* of the IPv6 header

- `1`: ICMP
- `6`: TCP
- `17`: UDP

## ICMP Header

**Control messages**
- `0/0`: Echo Reply
- `3`: Destination unreachable
	- Code `0`: network unreachable
	- Code `1`: host unreachable
- `8/0`: Echo Request
- `9/0`: Router Advertisement (IPv6)
- `10/0`: Router Solicitation (IPv6)
- `11`: Time Exceeded
	- Code `0`: TTL expired in transit
	- Code `1`: Fragment reassembly time exceeded

## TCP Header

- **important header fields**: source port, destination port, sequence number, Acknowledgment number, options

**Connection establishment**
- `SYN`: active open is performed by the client sending a SYN to the server
- `SYN-ACK`: server replies with a SYN-ACK
- `ACK`: the client sends an ACK back to the server

**Connection termination**
- `FIN`: endpoint which wishes to stop (initiator)
- `ACK` & `FIN`: receiver of FIN package
- `ACK`: initiator

## UDP Header

- **important header fields**: source port & destination port

---
links: [[Firewalls]] - [[themes/000 Index|Index]]