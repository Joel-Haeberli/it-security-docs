tags: #SPA #VPN 
 
# OpenVPN

links: [[616 SPA TOC - VPN|SPA TOC - VPN]] - [[themes/000 Index|Index]]

---

**Network Configurations**: Facilitates the establishment of secure point-to-point or site-to-site VPN connections, supporting both routed and bridged network configurations, as well as remote access capabilities.

**TLS for Encryption**: Utilizes the OpenSSL library for TLS/SSL to create encrypted tunnels over the internet.
    
**Authentication via PKI**: Implements a PKI scheme with X.509 certificates for node authentication.
    
   - **CA Management**: A Certificate Authority signs each node's certificate.
   - **Bidirectional Authentication**: Both client and server authenticate each other's certificates.
   
   **IP Addressing**: Adheres to RFC 1918 for private network addressing within VPN.
    
**Platform Support**: Compatible with Windows, Linux, macOS, Android, and iOS systems.
    
**Protocol Handling**: Encapsulates IP packets inside TCP/UDP layers for transmission.
    
**VPN Protocol Compatibility**: Functions in conjunction with other VPN protocols like IPsec and PPTP for integrated network setups.

---
links: [[616 SPA TOC - VPN|SPA TOC - VPN]] - [[themes/000 Index|Index]]