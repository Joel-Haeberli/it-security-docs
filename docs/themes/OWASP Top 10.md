tags: #web-security

# OWASP Top 10

links: [[506 WS TOC - OWASP & CSRF|WS TOC - OWASP & CSRF]] - [[themes/000 Index|Index]]

---

The **Open Web Application Security Project** lists the 10 most critical security risks for web applications. It's goal is to raise awareness about those risks.

## Overview 

Those risks with links are already covered in other places. Only a brief description is given for those in this document.

1. [[502 WS TOC - Broken Access Control|Broken Access Control]]
2. [[504 WS TOC - Crypto Failures|Cryptographic Failures]]
3. [[501 WS TOC - Injections|Injection]]
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. [[503 WS TOC - Broken Authentication|Identification and Authentication Failures]]
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery (SSRF)

## Broken Access Control

This occurs when users can access data or perform actions outside of their intended permissions. For example, viewing other users' data or changing someone else's account details.

## Cryptographic Failures 

Previously known as "Sensitive Data Exposure", this focuses on failures in cryptography that lead to exposure of sensitive data, like personal information or business secrets.

## Injection

This includes various forms of injection attacks, most notably SQL injection, where an attacker can send malicious data to be processed by an interpreter as part of a command or query.

## Identification and Authentication Failures

This was previously known as "Broken Authentication". It covers weaknesses in authentication and session management.

---
## Insecure Design

This is a new category focusing on risks related to design flaws in software. It emphasises the importance of secure design principles and practices.

### Overview

- Risks related to design and architectural flaws
	- Calls for more use of threat modelling
	- Usage of secure design patterns
- Build applications "Secure by Design"
- An insecure implementation can be fixed if it relies on a secure design
- An insecure design is a hopelessly lost cause

### Examples

1. **Password Recovery:** Using easily guessable or publicly known information for password recovery is a security risk due to potential identity exposure.
2. **Cinema Booking:** Lack of rate limiting or deposit requirements for bulk bookings can lead to financial losses due to fraudulent mass reservations.
3. **Retail Scalping:** Absence of anti-bot mechanisms on an e-commerce platform allows scalpers to exploit inventory, preventing genuine customers from making purchases.

**CWEs**

- CWE-209: Generation of Error Message Containing Sensitive Information, 
- CWE-256: Unprotected Storage of Credentials,  
- CWE-501: Trust Boundary Violation, and  
- CWE-522: Insufficiently Protected Credentials.

### Prevention

- Secure development lifecycle with AppSec professionals
- Use secure design patterns
- Use threat modelling
- Integrate security topics into user stories
- Defense in depth
- Automated tests for security stuff
- Segregate layers of your system. Need to know principle
- Limit resource consumption by one user or service

## Security Misconfiguration

This is about insecure default configurations, incomplete or ad-hoc configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information.

### Overview

With more shifts into highly configurable software this risk becomes more important.

- Missing security hardening
- Improperly configured permissions on cloud services
- Unnecessary features are enabled
- Default accounts remain in place unchanged
- Error messages reveal sensitive information
- Security settings not properly configured in frameworks

### Examples

1. **Compromised Application Server:** Unremoved sample applications with known flaws and unchanged default admin accounts allow attackers to easily gain control over the server.
2. **Directory Listing Exposure:** Enabled directory listing leads to unauthorized access and downloading of Java classes, enabling attackers to find and exploit security flaws.
3. **Revealing Error Messages:** Detailed error messages, including stack traces, inadvertently reveal sensitive information or vulnerabilities in the application server.
4. **Insecure Cloud Storage Permissions:** Default open sharing settings in a cloud service provider expose sensitive data to unauthorized internet access.

**CWEs**

- CWE-16 Configuration,  
- CWE-611 Improper Restriction of XML External Entity Reference.

### Prevention

- Implement an automated, repeatable hardening process for fast and secure deployment across development, QA, and production environments, using distinct credentials for each. 
- Employ a minimal platform approach, eliminating unnecessary features and components.
- Regularly review and update configurations in line with security advisories and patch management processes, including cloud storage permissions. 
- Use segmented application architecture for secure separation between components or tenants, utilising techniques like segmentation, containerisation, or cloud security groups. 
- Implement client-side security directives through security headers. 
- Establish an automated process to regularly verify the effectiveness of configurations and settings across all environments.

## Vulnerable and Outdated Components

Using components with known vulnerabilities, including libraries, frameworks, and other software modules.

### Overview

How does this happen:

- Not knowing the versions of used components and their nested dependencies
- Usage of vulnerable, unsupported or out of date OS, database, applications etc.
- When no automatic scanning is in place
- Not regularly upgrading all components in the DevOps chain
- When those upgrades are not properly tested

### Examples

1. **Component Vulnerabilities**: Applications are only as secure as their weakest component. Vulnerabilities in components, whether due to coding errors or intentional backdoors, can have severe consequences. The CVE-2017-5638 vulnerability in Struts 2 is a notable example, where a flaw in a widely used web framework led to significant breaches by allowing remote code execution.
2. **Challenges in IoT Security**: IoT devices pose unique security challenges. Due to their often limited capabilities and the complexity of updating them, patching vulnerabilities can be difficult or impossible. This is particularly concerning in critical applications like biomedical devices, where security flaws can have dire implications.
3. **Tools for Identifying Vulnerabilities**: Automated tools exist that make it easier for attackers to identify and exploit vulnerabilities. Shodan, for instance, is a search engine that can find IoT devices still affected by old vulnerabilities like Heartbleed, which was patched in 2014.

**CWEs**

- CWE-1104 Use of Unmaintained Third Party Components  
- CWE-937 OWASP Top 10 2013: Using Components with Known Vulnerabilities 
- CWE-1035 2017 Top 10 A9: Using Components with Known Vulnerabilities

### Prevention

-  **Removing Unnecessary Components**: Regularly eliminate unused dependencies, features, and documentation to minimize potential attack surfaces.
-  **Inventory Management**: Continuously track versions of all components (client-side and server-side) and their dependencies using tools like versions, OWASP Dependency Check, and retire.js.
-  **Vulnerability Monitoring**: Stay informed about vulnerabilities by monitoring sources like CVE and NVD, which provide information about known security issues in software components.
-  **Software Composition Analysis Tools**: Employ these tools to automate the process of identifying vulnerabilities within the software’s components.
-  **Email Alerts Subscription**: Stay updated on new vulnerabilities by subscribing to email alerts related to the components used in your software.
-  **Secure and Official Sources**: Ensure components are downloaded from official sources via secure links to avoid malicious modifications.
-  **Preference for Signed Packages**: Favor signed packages to lessen the risk of incorporating altered or malicious components.
-  **Monitoring Component Maintenance**: Keep an eye on libraries and components that are no longer maintained or don’t offer security patches for older versions, as they can pose significant security risks.
-  **Alternative Measures when Patching Isn’t Feasible**: If immediate patching isn’t possible, consider virtual patches to monitor, detect, or protect against identified issues.

## Software and Data Integrity Failures

A new category that focuses on making sure software and data are free from unauthorised modifications.

### Overview

Software and data integrity failures relate to code and infrastructure that do not protect against integrity violations. This can happen through modules from untrusted sources, automatic updates without integrity check and insecure CI/CD pipelines.

### Examples

- **Update Without Signing**: Devices like routers not verifying updates via signed firmware.
- **SolarWinds Malicious Update**: A targeted attack compromised update mechanisms.
- **Insecure Deserialization**: A React application's serialization process was exploited for remote code execution​​.

**CWEs**

- CWE-829: Inclusion of Functionality from Untrusted Control Sphere, 
- CWE-494: Download of Code Without Integrity Check, and 
- CWE-502: Deserialization of Untrusted Data.

### Prevention

- Use digital signatures for verification.
- Consume trusted repositories for libraries and dependencies.
- Employ software supply chain security tools like OWASP Dependency Check.
- Review processes for code and configuration changes.
- Ensure CI/CD pipeline integrity with proper segregation, configuration, and access control.
- Avoid sending unsigned or unencrypted serialized data to untrusted clients without integrity checks​​.

## Security Logging and Monitoring Failures

Insufficient logging, monitoring, and alerting can prevent or delay the detection of a security breach.

### Prevention

- Ensuring that all login, access control, and server-side input validation failures are logged with sufficient context. This aids in identifying suspicious activities and allows for delayed forensic analysis.
- Logs should be in a format easily consumed by centralized log management solutions.
- High-value transactions should have an audit trail with integrity controls to prevent tampering or deletion.
- Establish effective monitoring and alerting systems to detect and respond to suspicious activities in a timely manner​​.
## Server-Side Request Forgery (SSRF)

This is about attacks where the server is tricked into making unintended network requests to internal resources.

### Overview

SSRF occurs when a web application fetches a remote resource without validating the user-supplied URL, allowing attackers to coerce the application to send requests to unintended destinations.

### Examples

- **Port Scanning Internal Servers**: Mapping out internal networks through SSRF.
- **Sensitive Data Exposure**: Accessing local files or internal services for sensitive information.
- **Access Metadata Storage of Cloud Service**: Reading metadata from cloud providers.
- **Compromise Internal Services**: Abusing internal services for attacks like RCE or DoS​​.

### Prevention

- **Network Layer**: Segment remote resource access and enforce strict firewall policies.
- **Application Layer**: Sanitise and validate all client-supplied input data, enforce URL schema, port, and destination with an allow list, disable HTTP redirections, and be aware of URL consistency to prevent DNS rebinding and “time of check, time of use” (TOCTOU) attacks​​.
- Don't deploy security relevant services on the same systems where the rest is running.
- Consider using a VPN if the user group is small.

---
links: [[506 WS TOC - OWASP & CSRF|WS TOC - OWASP & CSRF]] - [[themes/000 Index|Index]]