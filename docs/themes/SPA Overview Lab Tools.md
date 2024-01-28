tags: #lab

# Overview Lab Tools

links: [[609 SPA TOC - Lab|SPA TOC - Lab]] - [[themes/000 Index|Index]]

---

## Lab 1

**Syslog**

- Standard for message logging, allows forward event notifications across networks
- Default port: UDP 514
- *Priority*: PRI = Facility x 8 + Severity
- There are tools available for sending from Windows Clients
- *Configuration for remote write*
	- Configuration of server to listen correctly, create firewall rules
	- Configuration of client to send to correct IP (UDP or TCP), create firewall rules, create rules (e.g. if logs from sshd, save to `/var/log/sshd.log`)

**Logrotate**

- system utility that manages the automatic rotation and compression of log files
- *Use*: create config files under `/etc/logrotate.d/`

**Logwatch**

- Logwatch is a customizable log analysis system. It parses through your system's logs for a given period of time and creates a report analyzing areas that you specify, in as much detail as you require.
- *Use*: `logwatch --service syslog-manual --detail High`

**LogAnalyzer**

- This is a web interface to syslog and other network event data. It provides easy browsing, analysis, and reporting of log data, which is often critical for system auditing and troubleshooting.
- *Use*: download loganalyzer copy to apache directory, run script, add user, restart apache, browse logs on webinterface

**Remote systemd-journald**

- *Configuration for remote write*: 
	- install package `systemd-journal-remote` on client and server
	- create necessary firewall rules on hosts
	- create certificates on client and server (e.g. with certbot)
	- *server*: configure journal-remote system daemon to use correct certificates
	- *client*: create user for daemon with rights to the certificates, configure journal-remote system daemon with 

**tcpdump**

- Command-line packet analyzer
- *lab exercice*: install `vsftp`, do ftp login, capture password with tcpdump
- *Use with capture filter*: `tcpdump -i eth0 -w dhcp.pcap port 67 or port 68`

**nmap**

- Nmap is a free network security scanner. Allows network-wide ping sweep, port, OS detection scans
- *Use*:
	- `nmap -sn 192.168.1.0/24`: ping scan of network (disable port scan)
	- `nmap -O -v`: OS detection
	- `nmap -sS --open`: TCP SYN scan
	- `nmap -sT --open`: TCP connect scan
	- `nmap -sU --open --top-ports=100`: UDP scan
	- `nmap -6 -sn`: ipv6 scan

**OpenVAS**

- OpenVAS (Open Vulnerability Assessment System) is a framework of several services and tools offering a comprehensive and powerful vulnerability scanning and vulnerability management solution.
- Pendant to Nessus but open-source
- Part of the Greenbone Security manager (GSM)
- *Use*:
	- enable systemd service `gsad`, `gvmd`, `ospd-openvas` (necessary daemons for web interface, scanner, etc.) 
	- `greenbone-feed-sync`: synchronize the vulnerability data feeds provided by Greenbone
	- `gvm-start`: start webserver, connect with browser to given localhost port
	- `runuser -u _gvm -- gvmd --get-get-scanners`:  ?

## Lab 2

**SNMP**

- find open SNMP ports: `nmap -sU --script snmp-brute 192.168.1.0/24 --script-args snmp-brute.communitiesdb=public`
- snmpwalk: `snmpwalk -v2c -c public 192.168.1.20`
- With snmpwalk, different attributes of the device can be find out (e.g. which routing protocols a router has configured, what MAC/IP pairs the device has cached, ...)

**Arpspoof**

- Arpspoof is a tool for network auditing and testing. It performs ARP spoofing, which involves sending fake ARP messages to an Ethernet network, generally for the purpose of associating the attacker's MAC address with the IP address of another host (such as the default gateway).
- ip forwarding must be active `echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward`
- `sudo arpspoof -i eth0 -t 192.168.1.21 -r 192.168.1.40`:
	- target host is `192.168.1.21`
	- `-r` stands for "poisen both hosts (host and target)"
	- `192.168.1.40` is the ip to spoof
	- *summary*: the attackers host send ARP replies to the host at `192.168.1.21`, making it believe that the attacker's machine is the device with IP `192.168.1.40`. The attack is bidirectional, redirecting traffic form both targets to the attacker's machine

**Arpwatch**

- Arpwatch is a network monitoring tool that tracks changes in Ethernet MAC addresses on a network and maintains a database of known MAC to IP address mappings. It is useful for detecting ARP spoofing or unauthorized network changes.
- can send emails based on events of an interface

**softflowd**

- Softflowd is a flow-based network traffic analyzer and exporter. It tracks network traffic and exports flow data in formats compatible with tools like SiLK and flow-tools, often used for network traffic accounting and monitoring.
- *Use*: configure softflowd-config to send packages to a specific ip: `options='-v 9 -n 192.168.1.220:2055'`

**nfcapd/nfdump**

- Nfcapd is part of the NFDUMP toolset and is responsible for collecting network flows (like NetFlow data). Nfdump is used to process and analyze the collected flow data, supporting various NetFlow versions.
- *Use*:
	- listen on port `2055` (add firewall rules)
	- Process Multiple Capture Files: `nfdump -r file1.nfcap -r file2.nfcap`
	- Filter Flows: `nfdump -r file.nfcap -A src-ip,10.0.0.1`
	- Top N Packets: `nfdump -r file.nfcap -o "fmt:%sS packets:%pkt" -s pkt`

## Lab 3

**nftables**

- create stateless and stateful rules
- **Exercise Scanners**:
	- create a ruleset in table: `set SCANNERS { type ..., size ..., flags ... }`
	- create new stateful rules which jumps to a user defined chain: `ct state invalid,new tcp dport { 21, 23, 25, 80, 443, 587, 993, 995 } jump PSCAN`
	- chain `PSCAN`: create rule with `limit rate over 60/minute add @SCANNERS { ip saddr } counter log prefix`
	- create rules in `INPUT` chain:  `ip saddr @SCANNERS counter drop`
	- **summary**: The nftable rules create a dynamic set named `SCANNERS` to identify and block IP addresses exhibiting port scanning behavior on specific TCP and UDP ports. Traffic from these IPs is dropped, and excessive connection attempts to unused ports trigger logging and addition of the source IP to the `SCANNERS` set for further mitigation.
- **Exercise NAT**:
	- add new ip address: `ip address add 192.168.70.1/24 dev ens224`
	- enable ip forwarding: `vim /etc/sysctl.conf (Set net.ipv4.ip_forward=1)`
	- create table: `nft add table ip nat`
	- create chain: `nft add chain ip nat POSTROUTING { type nat hook postrouting priority 100 \; }`
	- create rule: `nft add rule ip nat POSTROUTING oifname "ens224" ip saddr 192.168.70.0/24 masquerade`
	- **summary**: When packets are sent from the `192.168.70.0/24` network via the `ens224` interface, the `masquerade` action is applied. This implements Source Network Address Translation (SNAT), effectively masking the original IP addresses of the devices in the `192.168.70.0/24` network. Instead, these packets appear to originate from the router's IP address, `192.168.70.1`.
- **Exercise Squid**
	- create rules in mangle table/ PREROUTING chain
		- `tcp sport 80 socket transparent 1 socket wildcard 0 meta mark set 1 counter accept`: mark and accept response packet
		- `ip saddr 192.168.1.0/24 tcp dport 80 tproxy ip to :3129 meta mark set 1 counter`: redirect matching packets to local Squid port
	- create rules in filter table/ INPUT chain
		- `ip saddr 192.168.1.0/24 tcp dport { 80, 3128, 3129 } ct state new counter accept`: allow incoming access to Squid proxy
	- create rule in filter table/ OUTPUT chain
		- default policy accept
- **Exercise Firewall forward**
	- create rules in filter table/ FORWARD chain
		- `ip saddr 192.168.1.0/24 ct state new accept`: allow NEW outgoing connections from our net
		- `ip daddr 192.168.1.14 udp sport 1024-65535 udp dport 53 ct state new accept`: allow incoming DNS queries over udp to our nameserver
		- `ip daddr 192.168.1.15 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new counter accept`: allow incoming http connections to our webserver
	- create rule in filter table/ OUTPUT chain
		- default policy accept
	- *Summary*: The host will forward traffic based on the routing table (e.g. the DNS/Web traffic). It must be configured as "default gateway" by the clients. It cannot be a non-transparent proxy since the destination IP must be on the host for that (and we would not be in the FORWARD chain!).

**snort**

- Snort is an open-source network intrusion detection system (NIDS) and intrusion prevention system (IPS). It performs real-time traffic analysis and packet logging on IP networks for the detection of network threats and anomalies.
- *Use*: configure `snort.conf`, set up network variables etc, download and manage snort rules, run snort in test mode to ensure it's correctly configured

**suricata**

- Suricata is a high-performance Network IDS, IPS, and Network Security Monitoring engine. It is open-source and capable of real-time intrusion detection, inline intrusion prevention, network security monitoring, and offline pcap
- *Use*: configure `suricata.yaml`, set up network variables etc. download and manage suricata rulsets, run suricata to verify setup

**squid**

- Squid is a caching and forwarding HTTP web proxy. It has a variety of uses, from speeding up a web server by caching repeated requests, to caching web, DNS, and other network lookups for a group of people sharing network resources.

---
links: [[609 SPA TOC - Lab|SPA TOC - Lab]] - [[themes/000 Index|Index]]