tags:  #DNS #network #name-system 

# DNS Privacy

links: [[607 SPA TOC - DNS Security|SPA TOC - DNS Security]] - [[themes/000 Index|Index]]

---

Even with DNSSEC the DNS queries are still visible in plain text. To address this, new solutions were proposed to encrypt the traffic. But they also come with some down sights. 

**DNS over TLS (DoT)**

- **Functionality**: Encrypts DNS queries using the TLS. It operates on its own port (port 853).
- **Security**: Provides confidentiality and integrity between the client and the DNS resolver, preventing eavesdropping and manipulation of DNS data.
- **Downsides**: Its use of a distinct port can make DoT traffic easy to block or filter by network administrators or ISPs. Also, it doesn't hide the fact that DNS traffic is occurring, which could be a concern in some censorship scenarios.

**DNS over HTTPS (DoH)**

- **Functionality**: Encrypts DNS queries within regular HTTPS traffic. It operates over port 443, the same port used for HTTPS web traffic.
- **Security**: Offers the same level of encryption as DoT but is harder to block or filter since it blends in with regular HTTPS traffic.
- **Privacy**: Can prevent ISPs from easily monitoring DNS queries, as they appear as standard HTTPS traffic.
- **Downsides**: Its ability to blend in with regular traffic can be a double-edged sword; it's more challenging to monitor and manage within corporate networks, potentially bypassing traditional security controls. Additionally, it centralizes DNS queries to a few major providers (like those offering DoH services), which could raise concerns about privacy and control.

---
links: [[607 SPA TOC - DNS Security|SPA TOC - DNS Security]] - [[themes/000 Index|Index]]