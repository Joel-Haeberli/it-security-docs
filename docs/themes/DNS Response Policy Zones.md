tags:  #DNS #network #name-system 

# DNS Response Policy Zones

links: [[607 SPA TOC - DNS Security|SPA TOC - DNS Security]] - [[themes/000 Index|Index]]

---

## RPZ Firewalls

A Response Policy Zone (RPZ) is a DNS firewall feature that allows DNS server administrators to overlay custom information on top of the traditional DNS hierarchy, primarily to enforce security policies. By using RPZs, administrators can create rules that alter the responses provided by their DNS servers based on specific criteria.

**How Does RPZ Work?**

RPZ works by using specially crafted DNS zone files. These files contain policy rules that the DNS server checks against when resolving DNS queries. When a DNS request matches a rule in the RPZ, the DNS server can modify the response according to the policy defined. This modification can include blocking, redirecting, or altering the response in other ways.

RPZs are primarily used for security and content filtering purposes. Common uses include:

- Blocking access to malicious domains involved in phishing, malware distribution, or botnet control.
- Preventing access to inappropriate or unwanted content.
- Enforcing regulatory compliance by restricting access to certain types of websites.
- Mitigating the impact of DNS-based attacks by overriding the responses for known bad domains.

### How to update the rules

- Subscription to threat intelligence feeds that provide regularly updated lists of malicious or undesirable domains.
- Collaborating with industry groups or cybersecurity organizations that share information about threats.
- Utilizing open-source lists or community-contributed RPZ data.
- Monitoring network traffic and analyzing DNS logs to identify and add custom rules based on observed malicious activity.

### Triggers

Triggers are chosen in a specific order not mentioned here.

- **RPZ-CLIENT-IP:** This trigger is activated based on the IP address of the client making the DNS request. It allows the policy to be applied selectively based on client address.
- **QNAME:** This trigger is activated by the query names of requests and the targets of CNAME records resolved to generate the response. It's used to match the domain names being queried.
- **RPZ-IP:** This trigger uses IP addresses specified in A or AAAA records in the answer section of a DNS response to activate the policy.
- **RPZ-NSDNAME:** This trigger matches names of authoritative servers for the queried domain, including a parent of the queried name, or a parent of a CNAME record associated with the queried name.
- **RPZ-NSIP:** This trigger is used for matching IP addresses in A or AAAA Resource Records for domains that are checked against NSDNAME policy records.

### Record Sets

When a resolving name server encounters a query that matches a trigger in the RPZ, it can respond in several ways, including:

- **PASSTHRU:** This policy is a whitelist policy, specified by a CNAME to a target "rpz-passthru.", indicating that answer records are not rewritten.
- **DROP:** This blacklist policy is specified by a CNAME to target "rpz-drop.", meaning that the response is discarded, and nothing is sent to the DNS client.
- **TCP-Only:** This policy, specified by a CNAME to "rpz-tcp-only.", forces the querying DNS client to try again using TCP, which is a method used to mitigate certain types of DNS reflection attacks.
- **NXDOMAIN:** This response, indicating that the domain does not exist, is encoded by a CNAME to the root domain and is sent to the DNS client to block access.
- **NODATA:** This response is encoded by a CNAME with a wildcard top-level domain, resulting in an empty set of Resource Records sent to the DNS client.
- **Local Data:** An ordinary DNS record set that can be used to answer queries, often for redirections to a safer page or information site (walled garden).

### Policy Overrides

- **GIVEN:** The action specified in the zone file is carried out without overriding.
- **DISABLED:** This option logs the activity but does not take any action.
- **PASSTHRU, DROP, TCP-Only, NXDOMAIN, NODATA:** These actions override with the corresponding per-record policy.
- **CNAME domain:** This causes all RPZ policy records to act as if they were "cname domain" records.

### Enable RPZ list in BIND

![[dns_rpz_enable.png]]

### Example for `badlist`

![[dns_rpz_list.png]]
### Example

To block or redirect access to "badhost.baddom.com" using RPZ:

- **Blocking:** Add a QNAME trigger in the RPZ zone file that specifies "badhost.baddom.com". Set the action to NXDOMAIN or DROP to block access.
- **Redirecting:** Specify "badhost.baddom.com" in the RPZ zone file and associate it with the IP address of a safe server or a warning page. When a DNS query matches this rule, the DNS server will respond with the IP address of the redirect target instead of the actual IP address of "badhost.baddom.com".

---
links: [[607 SPA TOC - DNS Security|SPA TOC - DNS Security]] - [[themes/000 Index|Index]]