tags: #lab

# Lab 3 - Firewalls, Proxies, IDS

links: [[609 SPA TOC - Lab|SPA TOC - Lab]] - [[themes/000 Index|Index]]

---

"Solutions" from the dear professor :) Added it to have everything. Should be enough to get the concept.

## Exercise host based packet filter (stateless)

```
flush ruleset ip
table ip filter {
	chain INPUT {
		type filter hook input priority filter; policy drop;
		iifname "lo" ip saddr 127.0.0.0/8 ip daddr 127.0.0.0/8 counter packets 106 bytes 7109 accept
		udp sport 67 udp dport 68 counter packets 0 bytes 0 accept
		icmp type echo-reply counter packets 0 bytes 0 accept
		tcp sport 1024-65535 tcp dport 22 counter packets 0 bytes 0 accept
		udp sport 53 udp dport 1024-65535 counter packets 10 bytes 1056 accept
		tcp sport 53 tcp dport 1024-65535 tcp flags != syn / fin,syn,rst,ack counter packets 0 bytes 0 accept
		tcp sport { 22, 25, 80, 110, 143, 443, 587, 993, 995 } tcp dport 1024-65535 tcp flags != syn / fin,syn,rst,ack counter packets 85 bytes 32628 accept
		tcp sport 21 tcp dport 1024-65535 tcp flags != syn / fin,syn,rst,ack counter packets 0 bytes 0 accept
		tcp sport 20 tcp dport 1024-65535 counter packets 0 bytes 0 accept
		tcp dport 1024-65535 tcp flags != syn / fin,syn,rst,ack counter packets 0 bytes 0 accept
	}

	chain FORWARD {
		type filter hook forward priority filter; policy drop;
	}

	chain OUTPUT {
		type filter hook output priority filter; policy drop;
		oifname "lo" ip saddr 127.0.0.0/8 ip daddr 127.0.0.0/8 counter packets 106 bytes 7109 accept
		udp sport 68 udp dport 67 counter packets 0 bytes 0 accept
		icmp type echo-request counter packets 0 bytes 0 accept
		tcp sport 22 tcp dport 1024-65535 tcp flags != syn / fin,syn,rst,ack counter packets 0 bytes 0 accept
		udp sport 1024-65535 udp dport 53 counter packets 10 bytes 694 accept
		tcp dport 53 tcp sport 1024-65535 counter packets 0 bytes 0 accept
		tcp dport { 22, 25, 80, 110, 143, 443, 587, 993, 995 } tcp sport 1024-65535 counter packets 80 bytes 10870 accept
		tcp dport 21 tcp sport 1024-65535 counter packets 0 bytes 0 accept
		tcp dport 20 tcp sport 1024-65535 tcp flags != syn / fin,syn,rst,ack counter packets 0 bytes 0 accept
		tcp sport 1024-65535 counter packets 0 bytes 0 accept
	}
}%
```

## Exercise host based packet filter (stateful)

```
flush ruleset inet
table inet filter {
	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" ip saddr 127.0.0.0/8 ip daddr 127.0.0.0/8 accept comment "accept new local traffic"
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmp type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert } ip6 hoplimit 255 accept comment "allow icmp6 message for NDP with hop limit 255"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmpv6 type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "accept incomming RELATED and ESTABLISHED connections"
		ct state invalid drop comment "drop invalid packets silently"
		ct state new tcp sport 1024-65535 tcp dport 22 counter accept comment "accept incomming ssh connections"
		reject with icmp host-prohibited comment "RFC-friendly reject any other incomming connection"
		reject with icmpv6 admin-prohibited comment "RFC-friendly reject unwanted other incomming connection"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
	}
}

flush ruleset ip
table ip filter {
	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" ip saddr 127.0.0.0/8 ip daddr 127.0.0.0/8 accept comment "accept new local traffic"
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmp type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "accept incomming RELATED and ESTABLISHED connections"
		ct state invalid drop comment "drop invalid packets silently"
		ct state new tcp sport 1024-65535 tcp dport 22 counter accept comment "accept incomming ssh connections"
		reject with icmp host-prohibited comment "RFC-friendly reject any other incomming connection"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
	}
}

flush ruleset ip6
table ip6 filter {
	chain INPUT {
		type filter hook input priority filter; policy drop;
		iifname "lo" accept comment "accept all incomming traffic from local loopback if"
		icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert } ip6 hoplimit 255 accept comment "allow icmp6 message for NDP with hop limit 255"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmpv6 type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "accept incomming RELATED and ESTABLISHED connections"
		ct state invalid drop comment "drop invalid packets silently"
		ct state new tcp sport 1024-65535 tcp dport ssh counter packets 0 bytes 0 accept comment "accept and count incomming ssh connections"
		icmpv6 type { echo-request, nd-neighbor-advert, nd-neighbor-solicit, nd-router-advert } accept comment "allow icmp6 message for NDP"
		reject with icmpv6 admin-prohibited comment "RFC-friendly reject unwanted other incomming connection"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
		oifname "lo" accept comment "accept all outgoing traffic to local loopback if"
		ct state new counter accept comment "count new outgoing connections"
		ct state established,related accept comment "explicit allow established and related connections, not needed (default policy)"
	}
}

# Port scan detection

flush ruleset ip
table ip filter {
	set SCANNERS {
		type ipv4_addr
		size 128000
		flags dynamic
	}

	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" ip saddr 127.0.0.0/8 ip daddr 127.0.0.0/8 accept comment "accept new local traffic"
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmp type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "accept incomming RELATED and ESTABLISHED connections"
		ct state invalid,new tcp dport { 21, 23, 25, 80, 443, 587, 993, 995 } jump PSCAN comment "sniff on unused tcp .."
		ct state invalid,new udp dport { 53, 67, 69, 111, 123, 161 } jump PSCAN comment ".. and udp WKS ports to detect port scans"
		ip saddr @SCANNERS counter drop comment "drop packets from ip's in set SCANNERS"
		ct state invalid drop comment "drop invalid packets silently"
		tcp sport 1024-65535 tcp dport 22 ct state new counter accept comment "accept incomming ssh connections"
		counter reject with icmp host-prohibited comment "RFC-friendly reject any other incomming connection"
	}

	chain PSCAN {
		limit rate over 60/minute add @SCANNERS { ip saddr } counter log prefix "Port scan detected: " comment "if more then 60/min arrive to unused ports -> add to set SCANNERS and log"
	}
}
```


## Exercise network based packet filter (stateful)

```
flush ruleset inet
table inet filter {
	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" accept comment "allow local loopback traffic"
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmp type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert } ip6 hoplimit 255 accept comment "allow icmp6 message for NDP with hop limit 255"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmpv6 type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		tcp sport 1024-65535 tcp dport 22 ct state new counter accept comment "allow incomming SSH access"
		reject with icmp type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain FORWARD {
		type filter hook forward priority filter; policy accept;
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request, echo-reply } limit rate 15/second accept comment "rate limit echo-request/reply, accept packets below the limit"
		icmp type { echo-request, echo-reply } limit rate over 15/second drop comment "rate limit echo-request/reply, drop packets over the limit"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request, echo-reply } limit rate 15/second counter accept comment "rate limit echo-request/reply, accept packets below the limit"
		icmpv6 type { echo-request, echo-reply } limit rate over 15/second counter drop comment "rate limit echo-request/reply, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		ip saddr 147.87.86.112/28 ct state new accept comment "allow NEW outgoing connections from our net"
		ip daddr 147.87.86.112/28 tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH connections to our net"
		ip daddr 147.87.86.114 tcp sport 1024-65535 tcp dport 53 ct state new accept comment "allow incomming DNS queries over tcp to our nameserver"
		ip daddr 147.87.86.114 udp sport 1024-65535 udp dport 53 ct state new accept comment "allow incomming DNS queries over udp to our nameserver"
		ip daddr 147.87.86.115 tcp sport 1024-65535 tcp dport { 25, 587, 993, 995 } ct state new accept comment "allow incomming mail connections to our mailserver"
		ip daddr 147.87.86.115 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new accept comment "allow incomming Web connections to our webserver"
		ip6 saddr 2001:620:500:ffb0::/64 ct state new accept comment "allow NEW outgoing connections from our net"
		ip6 daddr 2001:620:500:ffb0::/64 tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH connections to our net"
		ip6 daddr 2001:620:500:ffb0::20 tcp sport 1024-65535 tcp dport 53 ct state new accept comment "allow incomming DNS queries over tcp to our nameserver"
		ip6 daddr 2001:620:500:ffb0::20 udp sport 1024-65535 udp dport 53 ct state new accept comment "allow incomming DNS queries over udp to our nameserver"
		ip6 daddr 2001:620:500:ffb0::30 tcp sport 1024-65535 tcp dport { 25, 587, 993, 995 } ct state new accept comment "allow incomming mail connections to our mailserver"
		ip6 daddr 2001:620:500:ffb0::30 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new accept comment "allow incomming Web connections to our webserver"
		reject with icmp type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
		reject with icmpv6 type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
	}
}

flush ruleset ip
table ip filter {
	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" accept comment "allow local loopback traffic"
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmp type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		tcp sport 1024-65535 tcp dport 22 ct state new counter accept comment "allow incomming SSH access"
		reject with icmp type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain FORWARD {
		type filter hook forward priority filter; policy accept;
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request, echo-reply } limit rate 15/second accept comment "rate limit echo-request/reply, accept packets below the limit"
		icmp type { echo-request, echo-reply } limit rate over 15/second drop comment "rate limit echo-request/reply, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		ip saddr 147.87.86.112/28 ct state new accept comment "allow NEW outgoing connections from our net"
		ip daddr 147.87.86.112/28 tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH connections to our net"
		ip daddr 147.87.86.114 tcp sport 1024-65535 tcp dport 53 ct state new accept comment "allow incomming DNS queries over tcp to our nameserver"
		ip daddr 147.87.86.114 udp sport 1024-65535 udp dport 53 ct state new accept comment "allow incomming DNS queries over udp to our nameserver"
		ip daddr 147.87.86.115 tcp sport 1024-65535 tcp dport { 25, 587, 993, 995 } ct state new accept comment "allow incomming mail connections to our mailserver"
		ip daddr 147.87.86.115 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new accept comment "allow incomming Web connections to our webserver"
		reject with icmp type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
	}
}

flush ruleset ip6
table ip6 filter {
	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" accept comment "allow local loopback traffic"
		icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert } ip6 hoplimit 255 accept comment "allow icmp6 message for NDP with hop limit 255"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmpv6 type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH access"
		reject with icmpv6 type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain FORWARD {
		type filter hook forward priority filter; policy accept;
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request, echo-reply } limit rate 15/second counter accept comment "rate limit echo-request/reply, accept packets below the limit"
		icmpv6 type { echo-request, echo-reply } limit rate over 15/second counter drop comment "rate limit echo-request/reply, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		ip6 saddr 2001:620:500:ffb0::/64 ct state new accept comment "allow NEW outgoing connections from our net"
		ip6 daddr 2001:620:500:ffb0::/64 tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH connections to our net"
		ip6 daddr 2001:620:500:ffb0::20 tcp sport 1024-65535 tcp dport 53 ct state new accept comment "allow incomming DNS queries over tcp to our nameserver"
		ip6 daddr 2001:620:500:ffb0::20 udp sport 1024-65535 udp dport 53 ct state new accept comment "allow incomming DNS queries over udp to our nameserver"
		ip6 daddr 2001:620:500:ffb0::30 tcp sport 1024-65535 tcp dport { 25, 587, 993, 995 } ct state new accept comment "allow incomming mail connections to our mailserver"
		ip6 daddr 2001:620:500:ffb0::30 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new accept comment "allow incomming Web connections to our webserver"
		reject with icmpv6 type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
	}
}
```

## Exercise Network Address Port Translation using network based packet filter

On the `router` VM, assign a private IP address from the RFC1918 range to the internal network interface:

```
ip address add 192.168.70.1/24 dev ens224

# Enable IP forwarding
vim /etc/sysctl.conf (Set net.ipv4.ip_forward=1)

# Enable NAT with nftables
nft add table ip nat
nft add chain ip nat POSTROUTING { type nat hook postrouting priority 100 \; }
nft add rule ip nat POSTROUTING oifname "ens224" ip saddr 192.168.70.0/24 masquerade

# Use a private address on one of the clients to test
```

## Exercise Host IDS/IPS

1. Configuration

* For Snort:
    * Configure snort.conf: Edit the Snort configuration file to set up network variables, preprocessor settings, and output options.
    * Rule Management: Download and manage Snort rules. You can use pulledpork or similar tools to automate rule management.
    * Testing Configuration: Run Snort in test mode to ensure it's correctly configured.
* For Suricata:
    * Configure suricata.yaml: Edit the main configuration file for Suricata, setting up network, logging, and processing options.
    * Rule Management: Obtain and manage Suricata rulesets. Suricata supports ET Open rules and other formats.
    * Testing Configuration: Run Suricata to verify the setup.

2. Running the IDS/IPS

* For Both Snort and Suricata:
    * Start in IDS Mode: Initially start the system in IDS mode to monitor and log network traffic without blocking.
    * Review Logs: Check logs for false positives and necessary adjustments.
    * Switch to IPS Mode: Optionally, switch to inline mode for active intrusion prevention.

## Exercise transparent web proxy using squid

```
flush ruleset inet
table inet mangle {
	chain PREROUTING {
		type filter hook prerouting priority mangle; policy accept;
		tcp sport 80 socket transparent 1 socket wildcard 0 meta mark set 1 counter accept comment "mark response packet and accept it"
		ip saddr 147.87.86.112/28 tcp dport 80 tproxy ip to :3129 meta mark set 1 counter comment "redirect matching packets to local squid port using fwmark and policy routing"
		ip6 saddr 2001:620:500:ffb0::/64 tcp dport 80 tproxy ip6 to :3129 meta mark set 1 counter comment "redirect matching packets to local squid port using fwmark and policy routing"
	}        
}

table inet filter {
	chain INPUT {
		type filter hook input priority filter; policy accept;
		iifname "lo" accept comment "allow local loopback traffic"
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmp type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		icmpv6 type { nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert } ip6 hoplimit 255 accept comment "allow icmp6 message for NDP with hop limit 255"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request } limit rate 15/second accept comment "rate limit echo-requests, accept packets below the limit"
		icmpv6 type { echo-request } limit rate over 15/second drop comment "rate limit echo-requests, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		tcp sport 1024-65535 tcp dport 22 ct state new counter accept comment "allow incomming SSH access"
		ip saddr 147.87.86.112/28 tcp dport { 80, 3128, 3129 } ct state new counter packets 0 bytes 0 counter accept comment "allow incomming access to Squid proxy"
		ip6 saddr 2001:620:500:ffb0::/64 tcp dport { 80, 3128, 3129 } ct state new counter packets 0 bytes 0 counter accept comment "allow incomming access to Squid proxy"
		reject with icmp type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
		reject with icmpv6 type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain FORWARD {
		type filter hook forward priority filter; policy accept;
		icmp type { destination-unreachable, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmp type { echo-request, echo-reply } limit rate 15/second accept comment "rate limit echo-request/reply, accept packets below the limit"
		icmp type { echo-request, echo-reply } limit rate over 15/second drop comment "rate limit echo-request/reply, drop packets over the limit"
		icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem } accept comment "allow needed icmp6 messages"
		icmpv6 type { echo-request, echo-reply } limit rate 15/second counter accept comment "rate limit echo-request/reply, accept packets below the limit"
		icmpv6 type { echo-request, echo-reply } limit rate over 15/second counter drop comment "rate limit echo-request/reply, drop packets over the limit"
		ct state established,related accept comment "allow ESTABLISHED and RELATED connections first (better performance)"
		ct state invalid drop comment "drop invalid packets silently"
		ip saddr 147.87.86.112/28 ct state new accept comment "allow NEW outgoing connections from our net"
		ip daddr 147.87.86.112/28 tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH connections to our net"
		ip daddr 147.87.86.114 tcp sport 1024-65535 tcp dport 53 ct state new comment "allow incomming DNS queries over tcp to our nameserver"
		ip daddr 147.87.86.114 udp sport 1024-65535 udp dport 53 ct state new comment "allow incomming DNS queries over udp to our nameserver"
		ip daddr 147.87.86.115 tcp sport 1024-65535 tcp dport { 25, 587, 993, 995 } ct state new accept comment "allow incomming mail connections to our mailserver"
		ip daddr 147.87.86.115 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new counter accept comment "allow incomming Web connections to our webserver"
		ip6 saddr 2001:620:500:ffb0::/64 ct state new accept comment "allow NEW outgoing connections from our net"
		ip6 daddr 2001:620:500:ffb0::/64 tcp sport 1024-65535 tcp dport 22 ct state new accept comment "allow incomming SSH connections to our net"
		ip6 daddr 2001:620:500:ffb0::20 tcp sport 1024-65535 tcp dport 53 ct state new accept comment "allow incomming DNS queries over tcp to our nameserver"
		ip6 daddr 2001:620:500:ffb0::20 udp sport 1024-65535 udp dport 53 ct state new accept comment "allow incomming DNS queries over udp to our nameserver"
		ip6 daddr 2001:620:500:ffb0::30 tcp sport 1024-65535 tcp dport { 25, 587, 993, 995 } ct state new accept comment "allow incomming mail connections to our mailserver"
		ip6 daddr 2001:620:500:ffb0::30 tcp sport 1024-65535 tcp dport { 80, 443 } ct state new accept comment "allow incomming Web connections to our webserver"
		reject with icmp type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
		reject with icmpv6 type admin-prohibited comment "reject any other packet and send back ICMP admin prohibited"
	}

	chain OUTPUT {
		type filter hook output priority filter; policy accept;
	}
}
```

---
links: [[609 SPA TOC - Lab|SPA TOC - Lab]] - [[themes/000 Index|Index]]