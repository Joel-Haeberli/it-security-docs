tags: #DNS #network #name-system

# DNSSEC

links: [[607 SPA TOC - DNS Security|SPA TOC - DNS Security]] - [[themes/000 Index|Index]]

---
## Overview

More information can be found in this [blog](https://www.cloudflare.com/dns/dnssec/how-dnssec-works/) by Cloudflare.
Get an overview [[X.509 CA Alternatives#DNSSEC|here]].
### Features

* Protects the Internet from attacks against the Domain Name System.
* Origin authentication of DNS data
* Integrity protection of DNS data
* Authenticated name and type non-existence (denial of existence)
* Means of public key distribution
* Prevents DNS cache poisoning (or DNS spoofing)
### Limitations

- No protection against DDoS
- Does not provide confidentiality
- DNSSEC only addresses the question of data integrity and authenticity, but does not in any way concern itself with the aspects of confidentiality.

## Key hierarchy

- hierarchical digital signing policy across all layers of DNS (a root DNS server would sign a key for `.com` nameserver, `.com` nameserver would then sign a key for `google.com`)
- To close the chain of trust, the root zone itself needs to be validated (proven to be free of tampering or fraud), and this is actually done using human intervention.

## Record types

DNS record types

- **RRSIG**: contains a cryptographic signature
- **DNSKEY**: contains a public signing key
- **DS**: contains the hash of a DNSKEY record
- **NSEC** and NSEC3: for explicit denial-of-existence of a DNS record
- **CDNSKEY** and CDS: for a child zone requesting updates to DS record(s) in the parent zone

## Procedure

1. group all the records with the same type into a resource record set (**RRset**)
2. the full RRset gets digitally signed with the *zone-signing-key pair* (**ZSK**) $\rightarrow$ this means that you must request and validate all of the "type of records" from a zone instead of validating only one of them
3. The RRset is signed using the private ZSK and stores them in a **RRSIG** record
4. The public ZSK is published in a **DNSKEY** record
5. a resolver can use the RRset, RRSIG and public ZSK to validate a response

![[RRsets.png]]

## Key-Signing-Key

- a key-signing key (KSK) validates the DNSKEY record $\rightarrow$ it signs the public ZSK (which is stored in a DNSKEY record), creating an RRSIG for the DNSKEY
- it is difficult to swap out an old or compromised KSK, changing the ZSK is much easier on the other hand

![[KSK_ZSK.png]]
### More about ZSK and KSK

- ZSK's should be replaced often eq. every 3 months otherwise the zone will become vulnerable against attacks using cryptanalysis.
- KSK's are valid for a longer period (eq. 1 year). An attack using cryptanalysis against the KSK takes longer, because there is fewer crypto-material in the Zone (only the RRSIG record of the DNSKEY RR set).
- Key exchange must be done in a safe way with an overlapping use of the old key (ZSK and KSK) and the new key (ZSK and KSK) and must respect the TTL of RRs.
- If the KSK must be changed, be aware that also his DS record in the parent zone must be replaced. Otherwise, the verification process will no longer work.

## Delegation Signer Records

- a delegation signer (DS) record allow the transfer of trust from a parent zone to a child zone.
- a zone operator hashes the DNSKEY record containing the public KSK and gives it to the parent zone to publish a DS record $\rightarrow$ a change in the KSK also requires a change in the parent zone's DS record

![[DS.png]]

## Explicit Denial of Existence

- If you ask DNS for the IP address of a domain that doesn't exist, it returns an empty answer $\rightarrow$ this is a problem if you want to authenticate the response.
- NSEC and NSEC3 record types works by returning the "next secure" record (e.g. if alphabetically sorted, respond with the next record in the zone) $\rightarrow$ this solution allows anybody to walk through the zone and gather every single record without knowing which ones they're looking for. 
- NSEC3 uses hashed names to reduce zone walking. But because hashing is cheap, zone privacy is only slightly improved when using NSEC3 as designed; the amount of protection a name gets is proportional to its unguessability. In short, NSEC is like revealing plaintext passwords, and NSEC3 is like revealing a Unix-style passwords file. Neither technique is very secure. With NSEC3 a subdomain is only as private as it is hard to guess. There is even a [script](https://nmap.org/nsedoc/scripts/dns-nsec3-enum.html) for nmap.

## Authentication Chain

**Island of Security**

This term refers to a securely signed and delegated DNS zone that lacks a direct authentication chain from its delegating parent. It is served by security-aware name servers and can offer authentication chains to any child zones it delegates. To authenticate responses from an Island of Security or its descendants, external trust methods are needed, as they aren't authenticated through the DNS protocol alone.

**DNSSEC Lookaside Validation (DLV)**

Previously, before the root zone was signed, DLV (as described in RFC 5074 and now considered historic) was used. It was a mechanism to validate DNSSEC information without needing multiple trust anchors, essentially acting as a workaround to validate DNS data before the root zone signing. With the signing of the root zone, the need for DLV has greatly diminished.

**CDS and CDNSKEY Records**

Building the chain of trust involves sending a DS or DNSKEY record of the Key Signing Key (KSK) to the parent zone's operator for publication, a process known for its complexity, especially during key rollovers. To streamline this, RFC 7344 proposes automating DNSSEC delegation trust maintenance through new resource records: Child DS (CDS) and Child DNSKEY (CDNSKEY). These records allow child zones to securely report key changes to the parent zone using previously established keys. Additionally, this approach enables easier key rollovers and the use of Combined Signing Keys (CSK), offering a more efficient alternative to the traditional KSK/ZSK pairs.

Later this was extended to allow automatic management:

- inserting a DS Record for the first time $\rightarrow$ enabling DNSSEC via CDS/CDNSKEY
- updating a DS Record $\rightarrow$ roll over of the KSK or CSK (add, delete or replace DS records at parent)
- removing a DS record $\rightarrow$ turn off DNSSEC validation (delete all the DS records at parent) 
### Changes to the DNS Protocol

**Checking Disabled CD**

The CD-bit is set in a query to indicate, that no DNS authentication should be made by the inquired name server i.e., the questioner is able, to do the authentication itself.  
The CD-bit is controlled by the resolver.

**Authenticated Data AD**

An inquired name server can indicate the successful authentication of the DNS data using the AD-bit. The AD-bit is controlled by a name server.

**DNSSEC OK (DO) EDNS header bit**

If the DNSSEC OK (DO) EDNS header bit is set in a query, the querying resolver indicates, that it is able, to get DNSSEC RRs in the corresponding response. The DO-bit is controlled by the resolver.
### Resolver Behaviour

When DNSSEC signatures cannot be validated, the response containing the Resource Records (RRs) should be deemed invalid. In cases where a name server is performing validation for a recursive query and none of the RRSIGs (Resource Record Signatures) validate successfully, it must return an RCODE 2 (server failure) to the client that initiated the query. However, if the original query had the Checking Disabled (CD) bit set, the name server should return the full response, including RRs that couldn't be validated. In practice, actual resolvers often validate RRs using DNSSEC but still send back all RRs, regardless of whether they could be validated or not. To differentiate between validated and non-validated RRs, the Authentic Data (AD) flag is used in the DNS response.

Advanced error codes and policies are still needed in the future.

## Use Cases

* DNSSEC signed zones can be used to "Securely Publish Secure Shell (SSH) Key Fingerprints"
	* Add SSHFP records to the zone and validate on connection
* DNS-based Authentication of Named Entities ([[X.509 CA Alternatives#DANE (DNS-based Authentication of Named Entities)|DANE]])
	* DANE provides a way to reduce the dependence on CAs. It allows the domain owner to specify the TLS certificates or public keys that should be accepted by users directly within the DNS records of the domain, using a new type of DNS record called TLSA.
	* DNSSEC Requirement: For DANE to work securely, it requires that the DNS records be secured using DNSSEC. DNSSEC prevents tampering with DNS records, ensuring that the TLSA records retrieved are authentic and haven't been altered in transit.

---
links: [[607 SPA TOC - DNS Security|SPA TOC - DNS Security]] - [[themes/000 Index|Index]]