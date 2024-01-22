tags: #zta

# Zero Trust Architecture

links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]

---

## Overview

- **Zero Trust (ZT)**: term for an evolving set of cybersecurity paradigms
- Goals of ZT: move defenses from static, network-based perimeters to focus on **user, assets, and resources**
- **Zero Trust Architecture (ZTA)**: uses zero trust principles to plan infrastructure and workflows
- **ZT assumes there is no implicit trust granted** to assets or user accounts based on:
	- their physical or network location (e.g. no access to devices in the same subnet)
	- asset ownership (enterprise or personally owned)
- authentication and authorization **must always be performed before a session to an enterprise resource is established**

### Focus

- Zero trust **focuses on protecting resources** (assets, services, workflows, network accounts, ...), not network segments
- the network location is no longer considered the most important component for the security of a resource
- should be expanded to include all:
	- **enterprise assets**: devices, infrastructure components, applications, virtual and cloud components
	- **subjects** that request information from resources: end users, applications, ...

### Security Model

- Zero trust security model assume:
	- that **an attacker is present in the environment**
	- that an enterprise-owned environment is no more trustworthy than any other public environment
- an enterprise must:
	- **assume no implicit trust**
	- continually analyze and evaluate the risks to its assets and business functions
	- minimize access to resources
	- continually authenticating and authorizing the identity and security status of each access request

## Zero Trust Architecture

- is an enterprise cybersecurity architecture
- based on zero trust principles
- designed to prevent data breaches
- is not a single architecture but a **set of guiding principles** for workflow, system design and operations

**Transition to ZTA**

- most enterprises are already in a hybrid zero trust mode with some elements of ZTA
- a enterprise should incrementally implement zero trust principles by use case
- is an ongoing process

## Zero Trust Access

A subject needs access to an enterprise resource:

- access is granted through a **policy decision point (PDP)** and corresponding **policy enforcement point (PEP)**

**ZT basic principles**

- All data sources and services are considered **resources**
- All communication is secured (e.g. transport layer encryption)
- Acccess to individual enterprise resources is granted on a per-session basis
- Access to resources is determined by **dynamic policy**
- The enterprise **monitors and measures** the integrity and security status of all assets
- All resource **authentication and authorization are dynamic** and strictly enforced before access is allowed
- The enterprise **collects as much information as possible**

**Logical Components of Zero Trust Architecture**

![[zero-trust.png]]

- **Policy engine (PE)**: ultimate decision to grant access to a resource for a given subject
- **Policy administrator (PA)**: establishing and/or shutting down the communication path between a subject and a resource. Generate session specific authentication.
- **Policy enforcement point (PEP)**: enabling, monitoring and eventually terminating connections between a subject and an enterprise resource

---

links: [[605 SPA TOC - Host & Network Security|SPA TPC - Host & Network Security]] - [[themes/000 Index|Index]]