tags: #web-security #crypto-failures

# PCI Data Security Standard (PCI DSS)

links: [[504 WS TOC - Crypto Failures]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]

---

## PCI DSS

The [PCI Data Security Standard (DSS)](https://www.pcisecuritystandards.org/) is a standard maintained and governed by the payment card industry. It must be implemented by any merchant using credit cards. The compliance of the implementation must be validated periodically. While big organisations are assessed by auditors, smaller companies just fill a self-assessment questionnaire.

### Requirements

To run a PCI DSS compliant implementation, an organisation must meet following base line requirements:

- Build and maintain a secure network 
	- firewalls, no vendor-supplied passwords or security parameters
- Data of card holders is protected 
	- Encryption during the transmission of such data through public and open networks
- Maintain a vulnerability management program
- Strong access control measures
- Monitor the network
- Regularly test the network
- Maintain an information security policy

### Storage of data

PCI DSS implementations store a massive amount of sensitive data including card holder data.

Data that is **never** to be stored includes 

- representation of cards magnetic stripe
- CVC2 / CVV2 / CID
- PIN

A data retention and disposal policy must be implemented which handles the process of deleting stored data after a defined amount of time.

---
links: [[504 WS TOC - Crypto Failures]] - [[500 WS MOC|WS MOC]] - [[themes/000 Index|Index]]