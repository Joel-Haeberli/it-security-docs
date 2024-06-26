tags: #auth 

# Kerberos Introduction

links: [[620 SPA TOC - Kerberos|SPA TOC - Kerberos]] - [[themes/000 Index|Index]]

---

## Kerberos Introduction

- Authentication protocol over untrusted networks
- Authentication is performed by a trusted third party
- Ticket based
- Uses symmetric crypto

### Microsoft

- Kerberos implementation name: MS-KILE
- Kerberos is default authentication
- Replaces [NTLM](https://en.wikipedia.org/wiki/NTLM), however NTLM is still widely used
- Used for single sign on (SSO) $\rightarrow$ show credentials to kerberos once and receive TGT to prove identity
- Services need to register a SPN (Service Principal Name)
- Only works with FQDN / NetBIOS names, not with IPs
- Uses port 88
- Typically only used in internal networks

![[kerberos-1.png]]

- **Key Distribution Center (KDC)**: Manages key and ticket distribution
- **Authentication Server (AS)**: Verifies identities, when a user logs in, the AS provides a **Ticket Granting Ticket (TGT)** if the user is authenticated successfully
- **Ticket Granting Server (TGS)**: Users with a TGT can request Service Tickets from the TGS using the TGT. TGS checks the TGT and if valid, issues a Service Ticket
- **Ticket Granting Ticket (TGT)**: Issued by the AS, used to request Service Tickets from the TGS
- **Service Ticket (ST)**: Issued by the TGS, used to authenticate the user to the service

### Service Principal Name (SPN)

- Unique identifier of a service instance in the domain
- Used by kerberos to associate a service instance with an actual logon account
- In Windows, some SPNs are create automatically, others need to be registered manually

![[kerberos-2.png]]

### Secret & Session Keys

**Secret keys**

- Long-term shared secret between users / services and the KDC
- Used to authenticate parties
- Derived from the party's password using string-to-key function (user or SPN/service account)

**Session keys**

- Short-term shared secret between users and services
- Used to secure communication
- Generated randomly by the involved parties

### Basic Working Principle

1. Users authenticate themselves to domain
2. Authenticated users request a TGT from the AS
3. User requests an ST by presenting TGT to the TGS
4. User presents ST to the target service
5. Service grants / denies access

- Step 3 - 5 are repeated for each service
- Authorization only happens at the last step

![[kerberos-3.png]]

### Pre-Authentication

To request a TGT the user must pre-authenticate

1. User encrypts current timestamp using a key derived from the password hash and send it to the KDC (AS-REQ)
2. KDC decrypts and verifies the timestamp to confirm that the user has used the correct password and the message is not a replay attack
3. KDC responds with a TGT + encrypted part with session keys and details to communicate with TGS

Pre-authentication is enabled by default but can be disabled. This way an attacker could request a TGT from the TGS without first having to prove that he knows the password. This would allow an attacker to try to brute force the password ([[ASREP Roasting]])

#### How can the AS verify the Pre-auth data

In Kerberos pre-authentication, the Authentication Server (AS) does not directly have your password, but it does have a key derived from your password. Here's how it works:

1. **Password Key Derivation**: When you set or change your password, a key is derived from this password (using a cryptographic hash function and possibly a salt). This key is stored securely on the Kerberos server, specifically within the Kerberos database on the Authentication Server.
2. **Pre-Authentication Process**:
    - When you attempt to authenticate, your client (usually your computer or another device you are logging in from) also generates this same key from the password you enter.
    - The client then uses this key to encrypt a timestamp and sends this encrypted timestamp to the Authentication Server as part of the pre-authentication data.
    - The Authentication Server then attempts to decrypt this timestamp using the key it has stored (derived from your password when it was set or changed).
    - If the server can successfully decrypt the timestamp and the timestamp is within an allowed time skew, it confirms that the client knows the correct password, thus verifying your identity.
3. **Security**: This process ensures that the actual password is never sent over the network. Only the derived key is used, and the actual password remains known only to you.

### Complete process in detail

![[kerberos-4.png]]

![[kerberos-5.png]]

![[kerberos-6.png]]

![[kerberos-7.png]]

![[kerberos-8.png]]

![[kerberos-9.png]]

AP-REQ / AP-REP is not performed via kerberos protocol, but instead wrapped into the respective application protocol

Corresponding Wireshark screenshots are in the slides

### Wireshark

- Some parts of the Kerberos messages are encrypted with session or long-term keys
- Wireshark can decrypt those parts, if the correct keytab file is provided in the config (edit > prefs > protocols > KRB5 > Kerberos keytab file)
- **Keytab file**: Contains the SPN of a user / service and corresponding password

### Authorization Data

- TGT and ST contain authorization information about the user $\rightarrow$ Privileged Attribute Certificate (PAC)
- PAC contains
	- User information (name, profile, home dir, etc.)
	- Account information (bad password count, last logo, last password change, etc)
	- Group information (membership of AD groups)
- Services use the PAC information to perform authorization without having to contact the domain controller
- PAC is signed by the KDC
- Services can still send PAC checksum to the KDC for validation (KERB_VERIFY_PAC), most services don't do this

### krbtgt Account

- Built-in account for the KDC service
- Its password is used to encrypt TGTs
- Disabled by default can't be activated
- Since 2003, the account's password is generated randomly by the domain
- **Compromise of krbtgt account**
	- Normally happens with DCSync where an attacker with domain admin privileges acts as a domain controller and requests data from other domain controllers including the NTLM hash of krbtgt
	- Grants full control over the domain
	- Attacker can craft their own TGTs for any service and user using the NTLM hash of krbtgt $\rightarrow$ Golden Ticket Attack
	- Tickets can have arbitrary lifetime since the attacker can set the lifetime himself
- **Compromise of a service account**
	- Allows attacker to forge service tickets to any user for this specific service only $\rightarrow$ Silver Ticket Attack
- ktbtgt account password should be changed regularly

---
links: [[620 SPA TOC - Kerberos|SPA TOC - Kerberos]] - [[themes/000 Index|Index]]