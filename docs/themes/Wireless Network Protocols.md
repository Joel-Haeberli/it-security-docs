tags: #wifi

# Wireless Network Protocols

links: [[617 SPA TOC - Wireless Security|SPA TOC - Wireless Security]] - [[themes/000 Index|Index]]

---

## Overview

- Wi-Fi stands for a family of wireless network protocols based on the **IEEE 802.11** family
- Each of these standards define **unique channels**. The channels available may be different by country!
- IEEE802.11 works on **OSI Layer 1** (Physical Layer)

## Usage

- **Ad Hoc** Peer-to-Peer (P2P)
	- Wireless Display
		- Miracast (Wi-Fi Alliance)
		- Apple Airplay
		- Google Cast
	- Apple AirDrop
	- HP Printers Wi-Fi Direct
- **Infrastructure**
	- Access Point
	- Wireless Router
	- ...

## 802.11a/b/g/n

![[802-11.png]]

## Access Point Characteristics

- **Access Point**: : Liaison between wireless and wired/celluar communication
- **SSID (Service Set Identifier)**: human readable name for wireless network, also called *network name*
- **BSSID (Basic Service Set Identifier)**: Unique identifier for a specific access point, same format as a MAC address (commonly set to the MAC address)
- **ESSID (Extended Service Set Identifier)**: group of BSSIDs that share the same Layer 2 network and the same SSID
- **Beacons**: Broadcasts that advertise the wireless settings (SSID, encryption method, ...) for a specific BSSID
- **Associating**: an access point and a client have agreed on parameters for communication

## Sniffing Communication

Firstly, you need a good antenna. Second, there are two basic ways to sniff:

- **Promiscuous Mode**: captures all packets on a connected network, regardless of the intended destination MAC address. You will see only packet if you are connected to a station and only packets inside the same network.
- **Monitor Mode**: captures all wireless traffic within its range, including packets not addressed to it, allowing analysis of all Wi-Fi communications in the vicinity (including beacons and data form any wireless networks in the area).

---
links: [[617 SPA TOC - Wireless Security|SPA TOC - Wireless Security]] - [[themes/000 Index|Index]]